# 二、javascript基础

+ js数据类型：{**引用类型: Object, Array, Function**},{值类型: Number, String, undefined, Boolean};

+ typeof只能准确区分值类型和Function，引用类型会返回Object;

+ instanceof是用于判断**引用类型**属于那个构造函数的方法；

+ JSON是一种数据格式，同时也是js的内置对象，拥有JSON.stringfy,JSON.parse两个API;

+ 如非必要，始终使用var(let、const)来声明变量，以尽量避免生成全局变量

+ 只有obj.a == null 使用“==”，其余都是用 “===”，避免强制类型转换造成混乱；

+ 整个程序生命周期中都不会改变的变量采用全部单词大写的规范来命名，such as: PI = 3.14;