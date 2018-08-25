# this

>关于this的规则

1.全局对象中，this指向ta自身；

2.this的指向，是在函数被调用的时候确定的（函数被调用 => 创建函数上下文 => 确定this指向）；

3.被调用函数上下文中的this的指向由调用函数的方式决定：

    + 函数独立调用时，函数内的this指向undefined，但在非严格模式时会自动指向全局对象。

    + 函数的调用者是一个对象，那么函数内的this指向该对象。

>使用场景

```javascript
"use strict"
const fn = function() {
  console.log(this)
}
fn() // undefined
```

```javascript
cosnt obj = {
  fn: function() {
    console.log(this)
  }
}
obj.fn() // obj
```

```javascript
"use strict"
const fn = function() {
  function fn1() {
    console.log(this)
  }
  fn1()
}
fn() // undefined
```

```javascript
var obj = {
  fn: function () {
    return this;
  }
}
console.log(obj.fn()); // obj

let test = obj.fn;
console.log(test());  // window
```