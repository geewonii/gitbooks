# markdown介绍

markdown是一种纯文本格式的标记语言。通过简单的标记语法，它可以使普通文本内容具有一定的格式。

优点：纯文本,操作简单。

缺点：需要记一些语法,有些平台不支持markdown编辑模式。

## 如何使用

1.标题

在想要设置为标题的文字前面加#来表示,一个#是一级标题，二个#是二级标题，以此类推,支持六级标题。
注：标准语法一般在#后跟个空格再写文字。

>示例：

    # 这是一级标题
    ## 这是二级标题
    ### 这是三级标题
    #### 这是四级标题
    ##### 这是五级标题
    ###### 这是六级标题

2.字体

加粗：要加粗的文字左右分别用两个*号包起来

斜体：要倾斜的文字左右分别用一个*号包起来

斜体加粗：要倾斜和加粗的文字左右分别用三个*号包起来

删除线：要加删除线的文字左右分别用两个~~号包起来

>示例：

    **这是加粗的文字**
    *这是倾斜的文字*
    ***这是斜体加粗的文字***
    ~~这是加删除线的文字~~

3.引用

在引用的文字前加>即可。引用也可以嵌套，如加两个>>三个>>>，以此类推

>示例:

    >这是引用的内容
    >>这是引用的内容
    >>>>>>>>>>这是引用的内容

4.分割线

三个或者三个以上的 - 或者 * 都可以。

>示例：

    ---
    ***

5.图片

>语法：
`![alt](src "title")`

alt:对图片内容的解释

title:图片的标题，可加可不加

>示例：

    ![alt](https://gss0.bdstatic.com/94o3dSag_xI4khGkpoWK1HF6hhy/baike/w%3D268%3Bg%3D0/sign=fcc6191515d8bc3ec60801ccbab0c123/279759ee3d6d55fb22bcda0961224f4a20a4dda3.jpg "标题")

6.超链接

>语法：
`[name](src "title")`
title可加可不加

7.列表

    * 无序列表用 - + * 任何一种都可以
    * 有序列表，数字加点
    * 列表嵌套：上下级之间敲两个空格
>示例：

```bash
* 一级
  * 二级
    * 三级
```

8.表格

>语法：

```bash
|表头|表头|表头|
|-|:-:|-:|
|内容|内容|内容|
|内容|内容|内容|

第二行分割表头和内容。
文字默认居左
"-"两边加":"表示文字居中
"-"右边加":"表示文字居右
```

>示例：

|表头|表头|表头|
|-|:-:|-:|
|内容|内容|内容|
|内容|内容|内容|

9.代码

单行代码：代码之间分别用一个反引号包起来

代码块：代码之间分别用三个反引号包起来，且两边的反引号单独占一行