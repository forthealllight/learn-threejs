# 渲染器、场景和照相机简介

------

本章简单介绍一下threejs中，关于渲染器（Renderer）、场景（Scene）和照相机（Camera）


------

### 1. 渲染器（Renderer）

渲染器主要功能是与HTML中的，Canvas元素进行绑定，以提供渲染的容器。如果在HTML中显式声明了Canvas元素：

    <canvas id="mainCanvas" width="400px" height="300px"></canvas>

那么显示的构建渲染器的方式为：

    var renderer=new THREE.WebGLRenderer({
      canvas:document.getElementById('mainCanvas')
    })

当然如果没有显式的声明，那么threejs也提供了默认添加渲染器的方式：

    var renderer=new THREE.WebGLRenderer();
    renderer.setSize(400,300);
    document.getElementById('body')[0].appendChild(renderer.domElement)

上述通过隐式声明的方式，同样也添加了一个渲染容器。renderer可以通过setColor方法设置渲染容器的背景色。

### 2. 场景（Scene）

我理解的场景，其实一个抽象的概念，就是存在于渲染容器中。渲染器渲染的是场景中的物体。对于场景，在场景初始化后，往场景中添加物体即可。

大致的过程为：***物体——>添加到场景中——>场景——>渲染器渲染***

Scene的初始化为：

    var scene=new THREE.Scene();

场景中添加：

    scene.add('一些物体')

### 3. 照相机（Camera）

物体在场景中是呈现在什么位置的，这与照相机有关，照相机的拍摄位置和拍摄角度，一定程度上决定了物体的表现形式。

介绍照相机之前，首先要明确在threejs中，所遵循的坐标系为右手坐标系：

![右手坐标系][1]


最后，先介绍一个在场景中添加一个长方体，并渲染的实验结果。

（1）定义照相机

    var camera = new THREE.PerspectiveCamera(45, 4 / 3, 1, 1000);
    camera.position.set(0, 0, 5);
    scene.add(camera);

（2）创建一个长方体添加到场景中

    var cube = new THREE.Mesh(new THREE.CubeGeometry(1, 2, 3),
        new THREE.MeshBasicMaterial({
            color: 0xff0000
        })
);
scene.add(cube);

构建的结果：

![此处输入图片的描述][2]


完整的代码：

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
          #info {
          	position: absolute;
          	top: 10px;
          	width: 100%;
          	text-align: center;
          	z-index: 100;
          	display:block;
        }
    </style>
    </head>
    <body>
       <canvas id="mainCanvas" width="400px" height="300px"></canvas>
    </body>
    <script src="https://cdn.bootcss.com/three.js/91/three.js"></script>
    <script>
    function init(){
      var renderer=new THREE.WebGLRenderer({
        canvas:document.getElementById('mainCanvas')
      });
      renderer.setClearColor(0x000000);
      //scene
      var scene=new THREE.Scene();
      //camera
      var camera=new THREE.PerspectiveCamera(45,4/3,1,1000);
      camera.position.set(0,0,5);
      scene.add(camera);
      //a cube
      var cube = new THREE.Mesh(new THREE.CubeGeometry(1, 2, 3),
               new THREE.MeshBasicMaterial({
                   color: 0xff0000
               })
       );
       scene.add(cube);

       // render
       renderer.render(scene, camera);
    }
    init();
    </script>
</html>


  [1]: https://github.com/forthealllight/learn-threejs/blob/master/images/location.png
  [2]: https://github.com/forthealllight/learn-threejs/blob/master/images/demo6.png
