# 禁用Firefox和Chrome的安全性检测

------

本地通过file文件打开html，如果在这个html文件中有ajax跨域请求，那么因为浏览器的安全性检测，会报错：

    Cross origin requests are only supported for HTTP....

但是我们在加载字体等文件，可能需要异步请求。当然如果启动一个本地server就不会有影响。这里有种懒人解决方案，就是通过禁用安全性检测的方法
------



### 1. 举例

我在本地通过file直接打开了一个html页面：

    file:///C:/Users/yuxl/Desktop/three/index2.html

我在这个Html中通过script有一段ajax跨域的请求，因为浏览器禁止本地file文件ajax跨域，因此会报错：

![此处输入图片的描述][1]

### 2. 禁用方案

我们以chrome为例，来看如何禁用浏览器安全检测，首先找到chrome的安装目录,我的chrome安装在以下目录：

    c/Program Files (x86)/Google/Chrome/Application
![此处输入图片的描述][2]

接着在此目录下我们执行，

    start chrome.exe --disable-web-security --user-data-dir="C:/Users/yuxl/Desktop/three"

通过--disable-web-security可以禁用安全性检测，后面的表示目录名称，其实也可以直接把本地文件拖到，通过上述命令打开的浏览器里面。


  [1]: https://github.com/forthealllight/learn-threejs/blob/master/images/security1.png
  [2]: https://github.com/forthealllight/learn-threejs/blob/master/images/security2.png
