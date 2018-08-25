# zepto源码阅读

嗯...听说zepto源码量少质高，于是也来读读看：[Zepto v1.2.0](http://zeptojs.com/zepto.js?tid=341681cc430b)

>总体结构

```javascript
var Zepto = (function() {
    ...
    return $
})()

window.Zepto = Zepto
window.$ === undefined && (window.$ = Zepto)
```

这里面相当于将自执行函数的返回值$赋值给window对象的Zepto和$属性

```javascript
$ = function (selector, context) {
  return zepto.init(selector, context)
}

zepto.init = function (selector, context) {
  ...
  return zepto.Z(dom, selector)
}

zepto.Z = function (dom, selector) {
  return new Z(dom, selector)
}

function Z(dom, selector) {
  var i, len = dom ? dom.length : 0
  for (i = 0; i < len; i++) this[i] = dom[i]
  this.length = len
  this.selector = selector || ''
}

zepto.Z.prototype = Z.prototype = $.fn

```

初始化方法将传入的dom处理后得到数组，Z函数将这个数组转化成类数组对象，再将Z函数的显式原型赋值$.fn,$.fn则是存在多个处理dom对象方法的对象。
(未完待续)