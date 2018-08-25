# [Vue](https://cn.vuejs.org "vue")

鉴于国内vue火热的现状无法冷却，准备面试的我重新抱起vue的大腿...

vue之所以如此火热也是有原因的：

```bash
1.压缩后代码量少

2.采用MVVM模式，实现双向绑定

3.组件耦合度低，使用更灵活

4.优秀的官方文档

5.官方提供脚手架，如vue-cli，构建项目方便简单
```

按照国际惯例：先看一遍[官方文档](https://cn.vuejs.org "vue")吧。

嗯，囫囵吞枣地复习一遍，就迫不及待地上github找项目去了。

这个star好多，就[他](https://github.com/bailicangdu/vue2-elm "vue2-elm")了。

半晌，稍微地掀了下ta的面纱，已感觉眼花缭乱的。

好在，作者的remake里有曙光，我翻译了一下：吾项目甚吊，汝若蠢，以[此径](https://github.com/bailicangdu/vue2-happyfri "vue2-happyfri")观，何如？

曰： 可。

```bash
git clone https://github.com/bailicangdu/vue2-happyfri.git  

cd vue2-happyfri

yarn install

npm run dev
```

嗯..先找入口文件，看看都有些啥：

```javascript
import Vue from 'vue'
import VueRouter from 'vue-router'
import routes from './router/router' //路由集
import store from './store/' //状态集
import ajax from './config/ajax'
import './style/common'
import './config/rem'

Vue.use(VueRouter)
const router = new VueRouter({
  routes
})

new Vue({
  router,
  store,
}).$mount('#app')
```

下一步便看看routes里面有啥:

>router.js

```javascript
import App from '../App'

export default [{ //仅有3个路由，require.ensure是webpack的按需加载语法
    path: '/',
    component: App,
    children: [{
        path: '',
        component: r => require.ensure([], () => r(require('../page/home')), 'home')
    }, {
        path: '/item',
        component: r => require.ensure([], () => r(require('../page/item')), 'item')
    }, {
        path: '/score',
        component: r => require.ensure([], () => r(require('../page/score')), 'score')
    }]
}]
```

看完路由顺便看看对应组件：
>home组件

```html
<template>
  <div class="home_container">
    <!-- 嗯，给itemcontainer组件定义了一个属性，值为home -->
    <itemcontainer father-component="home"></itemcontainer>
  </div>
</template>

<script>
import itemcontainer from '../../components/itemcontainer'

export default {
  name: 'home', //类似命名空间，用name属性来分配组件名称，应该是这样
  components: { //声明或注册子组件？
    itemcontainer
  },
  created(){}
}
</script>
```

**为节省篇幅，以下组件内类似的内容又不重要的就过滤掉**

>item组件

```javascript
  created(){
    this.$store.commit('REMBER_TIME'); //类似redux的dispatch(action)方法，Vuex.Store()方法会侦听commit触发的事件，更新state;
    //$store属于Vue原型对象的属性（应该是vuex挂在在Vue原型上的）；
  }
```

>score组件

```javascript
import {mapState} from 'vuex';
export default {
  name: 'score',
  data() {
    ...
  },
  computed: mapState(['answerid']), //获取store.state.answerid并映射到this.answerid
  created(){
    ...
  },
}
```

>itemcontainer组件

```javascript
import { mapState, mapActions } from 'vuex'
export default {
  name: 'itemcontainer',
  data() {
  ...
  },
  props:['fatherComponent'], //注册子组件时，想从父组件获取数据，使用props属性
  methods: {
    ...mapActions([
      'addNum', 'initializeData', //将组件的 methods 映射为 store.dispatch 调用
    ]),
    nextItem(){
      if (this.choosedNum !== null) {
        ...
        this.addNum(this.choosedId) //跟踪一下this.$store.dispatch('addNum')
        ...
    },
    ...
  }
}
```

>store/action.js

```javascript
export default {
  addNum({ commit, state }, id) {
    commit('REMBER_ANSWER', id); //派发 REMBER_ANSWER, 带一个参数
    ...
  },
  ...
}
```

>store/mutations.js

```javascript
const REMBER_ANSWER = 'REMBER_ANSWER'
export default {
  [REMBER_ANSWER](state, id) {
    state.answerid.push(id); //更新state
  },
  ...
}
```

总结一哈：

用vue、vue-router、vuex走一遍流程的项目，麻雀虽小，五脏俱全。作者所言不虚。
