# 文字形状和自定义形状

------

在上节中了解了基本的几何形状以及其构造方法，下面我们来看看文字形状和自定义形状

------

### 1. 文字形状

首先来了解一下，在threejs中如何构造文字形状，加载字体需要引入额外的字体库，threejs提供了很多字体库：

 - gentilis_bold.typeface.js
 - gentilis_regular.typeface.js
 - helvetiker_bold.typeface.js
 - helvetiker_regular.typeface.js
 - optimer_bold.typeface.js
 - optimer_regular.typeface.js

我们将字体下载到了本地，这里有个然后通过loader方法去加载字体：

    var loader = new THREE.FontLoader();
    loader.load( 'fonts/helvetiker_regular.typeface.js', function( font ) {
         var cube = new THREE.Mesh(new THREE.TextGeometry('Hello',
         {size: 1, height: 1,font:font}),
                new THREE.MeshBasicMaterial({
                    color: 0xffffff,
                    wireframe: true
                })
            );
          scene.add(cube);
          renderer.render(scene, camera);
      } );

为了显示一个hello文字。注意因为加载字体相当于一个异步的请求，因此renderer.render渲染方法应该在回调中执行。否则你看不到任何的渲染效果。

最后的渲染结果为：

![此处输入图片的描述][1]

### 2.自定义形状

自定义形状是指，我们通过指定所需形状的顶点，由顶点构成面，从而组成我们所需的具体形状。自定义形状的构造函数为：

    THREE.Geometry()

我们以构建一个三棱锥为例（最新版的threejs使用face3，我们以棱锥为例更容易说明问题）：

      var geometry = new THREE.Geometry();
      //设置自定义形状的顶点
      geometry.vertices.push(new THREE.Vector3(0,2,0));
      // 底部4顶点
      geometry.vertices.push(new THREE.Vector3(-2, 0, -2));
      geometry.vertices.push(new THREE.Vector3(2, 0, -2));
      geometry.vertices.push(new THREE.Vector3(2, 0, 2));
      geometry.vertices.push(new THREE.Vector3(-2, 0, 2));

      // 设置顶点连接情况
      // 底面
      geometry.faces.push(new THREE.Face3(1, 2, 3, 4));
      // 四个侧面
      geometry.faces.push(new THREE.Face3(0,1,2));
      geometry.faces.push(new THREE.Face3(0,2,3));
      geometry.faces.push(new THREE.Face3(0,3,4));
      geometry.faces.push(new THREE.Face3(0,1,4));

上述就是创建一个三棱锥的例子，具体的效果为：

![此处输入图片的描述][2]


  [1]: https://github.com/forthealllight/learn-threejs/blob/master/images/geo7.png
  [2]: https://github.com/forthealllight/learn-threejs/blob/master/images/geo6.png
