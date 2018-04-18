# Threejs官方文档-入门-（1）创建一个场景

------

这一章的主要目的是通过一个简短的例子来介绍一下threejs,我们用一个包含了旋转立方体的场景来开始介绍threejs。如果你在过程中遇到问题，需要查看帮助，那么可以参考本文最后面的例子。


## 1.开始之前

在使用threejs之前，我们需要在html文件中引入，然后可以在浏览器中打开html文件，本文通过cdn文件的方式引入。

    <!DOCTYPE html>
    <html lang="en">
    <head>
      <meta charset="UTF-8">
      <meta name="viewport" content="width=device-width, initial-scale=1.0">
      <meta http-equiv="X-UA-Compatible" content="ie=edge">
      <title>My first three.js app</title>
    		<style>
    			body { margin: 0; }
    			canvas { width: 100%; height: 100% }
    		</style>
    </head>
    <body>

    </body>
    <script src="https://cdn.bootcss.com/three.js/91/three.js"></script>
    <script>
       //写你的具体使用threejs的过程
    </script>

在script中可以写你自己调用threejs的API的代码。

## 2.创建场景

想要使用threejs展示任何模型，需要3个必不可少的因素：场景（scene）、相机（camera）、渲染器（renderer）。通过相机在场景中可以渲染出模型。

    var scene = new THREE.Scene();
    var camera = new THREE.PerspectiveCamera( 75, window.innerWidth /     window.innerHeight, 0.1, 1000 );
    var renderer = new THREE.WebGLRenderer();
    renderer.setSize( window.innerWidth, window.innerHeight );
    document.body.appendChild( renderer.domElement );

下面我们来解释一下，上述代码是如何建立场景（scene）、相机（camera）和渲染器（renderer）的。

（1）首先是相机（camera）,在threejs中提供了很多种相机类，在本文中使用的相机类为PerspectiveCamera。这个相机类可以接受4个参数

 - 第一个参数 : 视角大小,因为相机拍摄具有一定的角度，因此以角度为单位
 - 第二个参数 : 横纵比
 - 第三个参数：最近裁剪面（near clipping plane），太近的距离的不会被渲染
 - 第四个参数：最远裁剪面（far clipping plane），太远距离的也不会被渲染
 
用示例图来描述：![此处输入图片的描述][1]

（2）接着是渲染器（renderer）,在本文中使用了WebGLRenderer渲染器，除此之外，threejs为了支持老版本浏览器，也提供了其他各式各样的渲染器


  [1]: https://github.com/forthealllight/learn-threejs/blob/master/images/demo1-1.png