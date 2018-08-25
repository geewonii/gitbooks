
# 自定义事件

事件是可以被 JavaScript 侦测到的行为（事件通常与函数配合使用，当事件发生时函数才会执行）。

事件本质是一种消息，事件模式本质上是观察者模式的实现，那我们先来了解一下观察者模式。

## 观察者模式

这是一种创建松散耦合代码的技术。它定义对象间一种一对多的依赖关系，当一个对象的状态发生改变时，所有依赖于它的对象都将得到通知。

由主体和观察者组成，主体负责发布事件，同时观察者通过订阅这些事件来观察该主体。主体并不知道观察者的任何事情，观察者知道主体并能注册事件的回调函数。

>观察者模式示例

```javascript
function EventTarget(){
  this.handlers = {};
}

EventTarget.prototype = {
  constructor: EventTarget,
  addHandler: function(type, handler){
    if (typeof this.handlers[type] == "undefined"){
      this.handlers[type] = [];
    }
    this.handlers[type].push(handler);
  },
  fire: function(event){
    if (!event.target){
      event.target = this;
    }
    if (this.handlers[event.type] instanceof Array){
      var handlers = this.handlers[event.type];
      for (var i=0, len=handlers.length; i < len; i++){
        handlers[i](event);
      }
    }
  },
  removeHandler: function(type, handler){
    if (this.handlers[type] instanceof Array){
      var handlers = this.handlers[type];
      for (var i=0, len=handlers.length; i < len; i++){
        if (handlers[i] === handler){
          break;
        }
      }
      handlers.splice(i, 1);
    }
  }
};

const events = new EventTarget()
events.addHandler('show', callback1).addHandler('show', callback2)
events.fire({type: 'show'}) //测试用参数
events.removeHandler('show', callback1).fire({type: 'show'})

function callback1() {
  console.log('我是回调函数1')
}

function callback2() {
  console.log('我是回调函数2')
}

```

>大概功能就是：

创建一个事件管理器。handlers是存储事件处理函数的对象。

addHandler：是添加事件的方法，该方法接收两个参数，一个是要添加的事件的类型，一个是这个事件的回调函数名。调用的时候会首先遍历handlers这个对象，看看这个类型的方法是否已经存在，如果已经存在则添加到该数组，如果不存在则先创建一个数组然后添加。

fire：是执行handlers这个对象里面的某个类型的每一个方法。

removeHandler：是相应的删除事件执行函数的方法。

>大致了解过观察者模式后，回头看js中自定义事件的写法

```javascript
var event = new Event('build');

// Listen for the event.
elem.addEventListener('build', function (e) { /* ... */ }, false);

// Dispatch the event.
elem.dispatchEvent(event);
```

这样的话，elem上通过dispatchEvent方法触发的事件build，只有在elem上注册的监听器能够监听到。

实际情况多数是在一个公共对象如document对象上进行事件的监听和触发。

需要注意的是，当一个事件触发的时候，如果相应的elem及其上级元素没有对应的EventListener，就不会有任何回调操作。

对于子元素的监听，可以对父元素添加事件托管，让事件在事件冒泡阶段被监听器捕获并执行。这时候，使用event.target就可以获取到具体触发事件的元素。

详细例子可以进入[传送门](https://blog.csdn.net/ruangong1203/article/details/52474452#commentBox)了解。

## 自定义事件的增加和移除

>示例：

```javascript
const btn = document.getElementById("btn")
let switchs = true

function handeler() {
  console.log('logs event trigger')
}

btn.addEventListener('click', function(){
  btn.addEventListener('logs', handeler, false) //监听btn的logs事件
  if(switchs) {
    btn.dispatchEvent(new Event('logs')) //触发btn的logs事件
    switchs = !switchs
  } else {
    console.log('remove event')
    btn.removeEventListener('logs', handeler, false) //移除btn的logs事件
    switchs = !switchs
  }
}, false)
//注意：匿名函数无法通过removeEventListener消除监听事件，实名函数可以
```