# Nodejs如何安装

#### 首先下载安装包
官网：[点我](http://nodejs.cn/)

#### 双击安装完成后，检查是否安装成功
命令行输入
```
node -v         //返回nodejs的版本
npm -v          //返回npm包管理器的版本
```
**注意** 如果之前已经安装过nodejs的话，想卸载干净，最好全局搜索**.npmrc**并删除,这个文件是记录了之前的`cache`和`prefix`的记录。

#修改环境变量
因为通常nodejs默认都会安装在C盘(window用户)或/usr/local(类linux用户)下，都涉及到管理员权限。有时候使用会不方便，这个时候就需要修改nodejs的环境变量。   
类linux用户的方法
```
//首先修改nodejs默认配置
npm config set cache "/Users/ouxiaobao/node_cache/"  //改变默认cache位置
npm config set prefix "/Users/ouxiaobao/node_global/" //改变默认全局node_module位置

export PATH=$PATH:/Users/ouxiaobao/node_global/
```
而windows用户请参考本链接
```
//首先修改nodejs默认配置
npm config set cache "C:\nodejs\node_cache\"  //改变默认cache位置
npm config set prefix "C:\nodejs\node_global" //改变默认全局node_module位置

//然后记得修改环境变量Path,把C:\nodejs\node_global/node_modules添加进去

```
[windows用户更多可参考这里](http://blog.csdn.net/pengpegv5yaya/article/details/51885829)

## 如果发现npm命令无法安装，或全局命令找不到
全局搜索**.npmrc**并删除,这个文件是记录了之前的`cache`和`prefix`的记录。就是它搞得鬼，通常是放在**C:\Users（用户）\你的用户名\.npmrc**

## 首次安装
假设你的电脑是干干净净的，首次安装后，其实nodejs只做了一件事情
1. 把nodejs的核心文件，默认放到你的安装目录中
    默认的全局插件是放在
    **c:\Users\用户名\AppData\Roaming\npm\node_modules**
    默认的缓存目录是放在
    **c:\Users\用户名\AppData\Roaming\npm-cache**

    可以通过下面命令获取
    ```
    npm config get prefix    #获取到nodejs的全局基础目录
    npm config get cache     #获取到nodejs的缓存目录
    npm root -g              #获取到nodejs的全局node_modules目录
    ```


## 关于常常说的NODE_PATH环境变量
我们在网上，总是看到很多教程说要加什么NODE_PATH环境变量，其实**不一定需要的**,**它主要是用在引入模块时使用，对全局命令行并无卵用。**

NODE_PATH中的路径被遍历是发生在
当我们需要使用或引入某个全局模块的时候(也就是在代码中使用require的时候)，它会先从项目的根位置递归搜寻 node_modules 目录，直到文件系统根目录的 node_modules，如果还没有查找到指定模块的话，就会去 NODE_PATH中注册的路径中查找。所以，通常咱们只需要把NODE_PATH设置为你的**全局node_modules文件夹路径**即可。

## 如果想修改上面所说路径
首先改配置
```
    npm config set prefix "c:\nodejs\node_global"   #设置到nodejs的全局基础目录
    npm config set cache  "c:\nodejs\node_cache"    #设置到nodejs的缓存目录
```
然后添加新的路径**c:\nodejs\node_global\node_modules**到环境变量PATH中


