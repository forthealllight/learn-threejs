# Threejs官方文档-入门-（2）模块的方法引入

------

之前我们通过script标签的形式引入了threejs,这是一种方便的方法且以CDN的方式加载也较快，但是如果要实现代码的长寿性，通过script的方法有很多缺点：

 - 你必须手动获取或者拷贝插件的一部分作为你项目的源码

 - 你需要手动更新插件的版本

 - 比较插件的新旧版本时也不是很方便

通过使用依赖管理工具，类似于npm等，可以避免这些问题，使你可以很简单的下载和引入所需要的插件版本。


## 1.通过npm安装

threejs已经发布了相关的npm包，你可以通过npm install threejs的方式来安装

## 2.引入模块

如果通过webpack或者browserify来打包你的文件，在文件中，你可以使用require('modules')的方式，来引入模块，这不影响webpack的打包。

你现在就可以往你的源文件中引入模块，就想通过script脚本一样，可以使用它：

    var THREE = require('three');
    var scene = new THREE.Scene();

也可以通过ES6的语法糖来引入模块：

    import * as THREE from 'three';
    const scene = new THREE.Scene();

如果你仅仅想引入threejs插件的部分属性，比如说仅仅想引入Scene属性：

    import { Scene } from 'three';
    const scene = new Scene();

## 3.注意事项

一般来说，我们不能通过模块的方式，引入threejs文件目录下examples/js的模块。
