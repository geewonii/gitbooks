# 闭包

**闭包是一种特殊的对象。**

**它由两部分组成：**
+ 执行上下文(A)
+ 该执行上下文中创建的函数(B)

**当B执行时，如果访问了A中变量对象中的值，就会形成闭包。**

**使用场景：**

+ 函数作为返回值
+ 函数作为参数来传递

```javascript
let fn = null
function foo() {
  let a = 2
  function innnerFoo() {
    console.log(a)
  }
  fn = innnerFoo // 将 innnerFoo的引用，赋值给全局变量中的fn
}

function bar() {
  fn() // 在innnerFoo的变量对象中没有a变量，往foo的变量对象中查找，层层往上，实在找不到则赋值undefined
}

foo()
bar() // 2
```
