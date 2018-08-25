# 用js实现模态弹框

>要求：

```bash
1.使用构造函数方式实现；
2.使用单例模式，并且多个实例间互不影响，相互独立；
3.弹框标题和内容采用传参的方式获得；
4.存在show()、close()、on()、off()方法，并可链式调用；
5.on方法绑定可事件，并成功调用回调函数；
6.off方法取消事件绑定，并成功调用回调函数；
```

这是一道机试题，感觉考得挺全面的，原型、架构、事件机制等等，当时状态比较差，没做好，只好回来撸一遍，需要改善的地方还有很多，有空再优化一下。

```javascript
function Dialog(options) {
  if (!(this instanceof Dialog)) return new Dialog(options);
  this.options = this.extend(this.options, options);
  this.init();
}

Dialog.prototype = {
  constructor: Dialog,
  init: function() {
    this.el = document.getElementById(this.options.el)
    this.switchs = this.options.switchs
    this.type = this.options.type
    this.data = this.options.data
    this.matchTypes()
  },
  extend: function(obj, obj2) {
    for(var k in obj2) {
      obj[k] = obj2[k];
    }
    return obj;
  },
  changeSwitchs: function(bool) {
    this.switchs = !!bool
    this.renders()
  },
  eventHandels(element, type, fn) {
    var element = element instanceof Object ? element : document
    if(this.switchs) {
      element.addEventListener(type, fn)
      element.dispatchEvent(new Event(type))
    } else {
      fn()
      element.removeEventListener(type, fn)
    }
    this.renders()
  },
  show: function() {
    this.changeSwitchs(true)
    return this
  },
  close: function() {
    this.changeSwitchs(false)
    return this
  },
  on: function(element, type, fn) {
    this.changeSwitchs(true)
    this.eventHandels(element, type, fn)
    return this
  },
  off: function(element, type, fn) {
    this.changeSwitchs(false)
    this.eventHandels(element, type, fn)
    return this
  },
  onIsOk: function() {
    alert('click ok')
  },
  matchTypes: function(){
    var title = this.data.title
    var body = this.data.content
    switch(this.type) {
      case 'maskLog':
        this.maskLog()
        break
      default:
        this.logs(title, body)
    }
  },
  logs: function(title, body) {
    var warp = document.createElement('div');
    warp.innerHTML += "<div>"+ title +"</div>\
    <div>"+ body +"</div>\
    <button id='isOk'>确定</button>\
    <button id='isCancel'>取消</button>";
    this.el.appendChild(warp);

    var isOk = document.getElementById('isOk')
    var isCancel = document.getElementById('isCancel')
    var self = this
    var _list = [isOk, isCancel]
    _list.forEach(function(item){
      item.addEventListener('click', function(){
        if(this.id === 'isOk') self.onIsOk()
        self.close()
      },false)
    })
  },
  renders: function() {
    if(this.switchs) {
      this.el.style.visibility = 'visible'
    } else {
      this.el.style.visibility = 'hidden'
    }
  },
  options: {
    title: 'title',
    context: 'context',
    theme: '',
    type: 'normal',
    switchs: false,
  }
}
```