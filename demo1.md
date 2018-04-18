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
 
![此处输入图片的描述][1]
用示例图来描述：在上图中绿色3D边框的椎体称为视锥体，也就是相机可以拍摄到的区域，用于裁剪视图，zNear和zFar分别定义了最近裁剪面和最远裁剪面的距离。

（2）接着是渲染器（renderer）,在本文中使用了WebGLRenderer渲染器，除此之外，threejs为了支持老版本浏览器，也提供了其他各式各样的渲染器。

在创建渲染的例子时，需要制定渲染区域的高度和宽度，在本文的例子中用浏览器的宽度和高度来指定渲染区域的宽高：

    renderer.setSize( window.innerWidth, window.innerHeight );
    
当然也可以指定宽高为window宽高的一半：

     window.innerWidth/2，window.innerHeight/2

此时的渲染区域变为一半大小，此外也可以保持渲染区域的大小，使得在一个更低分辨率下渲染：

     renderer.setSize( window.innerWidth/2, window.innerHeight/2,false );

对比高低分辨率下的渲染结果，首先是高分辨率下：

![此处输入图片的描述][2]

接着是低分辨率下：

![此处输入图片的描述][3]

（3）最后，我们将renderer渲染的元素，添加进HTML的document中。

（4）构建完场景之后，接着来看如何创建本文的例子——一个立方体。

    // cube
    var geometry = new THREE.BoxGeometry( 1, 1, 1 );
    var material = new THREE.MeshBasicMaterial( { color: 0x00ff00 } );
    var cube = new THREE.Mesh( geometry, material );

首先，确定几何模型，这里采用盒式几何模型（BoxGeometry）,接着需要材料（material）去确定填充颜色，这里使用网格填充材料（MeshBasicMaterial），所有的材料接收一个对象属性作为参数，为了方便本文的例子中，该对象只包含了color属性，0x00ff00也就是绿色，这里的色值表示的方法和CSS以及photoshop中是相同的。第三件事，需要构建一个网格，在计算机中，所有的立体模型都是由线组成网格，用网格来表示物体，在threejs中的网格中，网格(mesh)接受一个对象参数，该对象由几何模型和材料组成。由网格组成渲染的物体，可以添加到场景中，并且可以在场景中自由的移动。

    var cube = new THREE.Mesh( geometry, material );

上述代码就添加了一个cube立方体物体。

## 3.渲染场景

如果仅仅通过上述的代码，你是无法得到任何渲染结果的。因为我们事实上没有渲染任何东西，为了实现成功渲染，需要新增一个渲染或者说是循环驱动。

    function animate() {
      requestAnimationFrame( animate );
      renderer.render( scene, camera );
    }
    animate();
上述的函数，会在屏幕刷新的时候重复渲染，那么这种重复渲染的事件为什么不通过setTimeInterval来实现呢？requestAnimationFrame（RAF）的优点很明显，首先它跟显示器的刷新频率保持一致，且不会收同步事件的影响，不会造成丢帧等现象。更为重要的一点，就是RAF在页面跳转后，保持在后台运行时，会暂停执行，因此不会浪费资源。

## 4.驱动立方体

上述的效果仅仅是在场景中显示一个静止不动的立方体，下面我们来使这个立方体可以实现一定意义上的旋转，可以在渲染的renderer.render方程中：

    cube.rotation.x += 0.1;
    cube.rotation.y += 0.1;

我们在每一帧中实现渲染，RAF的频率通常是60帧，也就是在1秒内渲染60次。

## 5.完整代码

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
    var scene = new THREE.Scene();
    var camera = new THREE.PerspectiveCamera( 75, window.innerWidth / window.innerHeight, 0.1, 1000 );
    var renderer = new THREE.WebGLRenderer();
    renderer.setSize( window.innerWidth/2, window.innerHeight/2,false);
    document.body.appendChild( renderer.domElement );
    // cube
    var geometry = new THREE.BoxGeometry( 1, 1, 1 );
    var material = new THREE.MeshBasicMaterial( { color: 0x00ff00 } );
    var cube = new THREE.Mesh( geometry, material );
    scene.add( cube );
    
    camera.position.z = 5;
    var animate = function () {
    				requestAnimationFrame( animate );
    
    				cube.rotation.x += 0.1;
    				cube.rotation.y += 0.1;
    
    				renderer.render(scene, camera);
    			};
    animate();
    </script>
    </html>


  [1]: https://github.com/forthealllight/learn-threejs/blob/master/images/demo1-1.png
  [2]: https://github.com/forthealllight/learn-threejs/blob/master/images/demo1-2.gif
  [3]: https://github.com/forthealllight/learn-threejs/blob/master/images/demo1-3.gif
