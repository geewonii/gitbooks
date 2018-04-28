# 一、gitbook的使用


##Gitbook介绍
Gitbook 是基于 Node.js 的命令行工具，用来创建漂亮的电子书，它使用 Markdown 或 AsciiDoc 语法来撰写内容，用 Git 进行版本控制，且可以托管在 Github 上。Gitbook 可以将作品编译成网站、 PDF、 ePub 和 MOBI 等多重格式。

如果你不擅长自己搭建 gitbook 环境，还可以使用 [gitbook.com](https://www.gitbook.com) 在线服务来创建和托管你的作品，他们还提供了基于桌面的 [编辑器](https://www.gitbook.com/editor) 。

##如何使用
1.首先在全局安装 gitbook 客户端工具：
<pre><code>npm install gitbook-cli -g</code></pre>
2.创建一个文件夹book，并在这个文件夹中创建一个book.json文件，并填入基本信息：
<pre><code>{
  "gitbook":"3.2.3",
  "title":"学习笔记",
  "author":"geewonii",
  "language": "zh-Hans",
  "plugins":[
      "sectionx",
      "expandable-chapters"
  ]
}</code></pre>
3.安装插件：
<pre><code>gitbook install</code></pre>
4.创建README.md 和 SUMMARY.md:
<pre><code>gitbook init</code></pre>
5.在你的作品目录中创建两个必需的文件 README.md 和 SUMMARY.md，README.md 是作品的介绍，SUMMARY.md 是作品的目录结构，里面要包含一个章节标题和文件索引的列表:
<pre><code></code></pre>
6.运行服务，在编辑内容保存后实时预览：
<pre><code>gitbook serve</code></pre>
7.撰写完后可以生成静态网站用来发布：
<pre><code>gitbook build</code></pre>
8.更多命令帮助:
<pre><code>gitbook help</code></pre>
9.自由切换版本:
<pre><code>gitbook ls-remote           //罗列出所有的版本号
gitbook fetch 2.1.0         //选择其中一个版本切换安装
</code></pre>
10.更多插件：[参考链接](https://blog.csdn.net/qq_37149933/article/details/64170653)
