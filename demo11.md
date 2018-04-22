# Threejs入门指南-（6）材质的纹理贴图

------

上一节中介绍了主要的几种材质（Material），本节介绍材质的纹理贴图

------

### 1. 单张图片的纹理贴图

首先给出贴图的图片：

![此处输入图片的描述][1]

接着将其导入到纹理图中：

    var texture = THREE.ImageUtils.loadTexture('../img/0.png');

我们前面介绍过材质有map属性，我们通过map属性将我们的贴图信息传入到材质中：

        var texture = THREE.ImageUtils.loadTexture('images/0.png',                        {}, function() {
                      renderer.render(scene, camera);
                 });

注意这样会提示：THREE.ImageUtils.loadTexture是一个过去版本的API已经被废除，我们这里使用的是91版本的threejs，提示我们使用THREE.TextureLoader()。

如何使用：

      var texture = new THREE.TextureLoader().load( 'images/0.png'                ,function(){
                  renderer.render(scene,camera);
                });

通过构造THREE.THREE.TextureLoader().load来调用，并且异步读取文件有一个回调函数，在回调函数中renderer.render。

最后的效果为：

![此处输入图片的描述][2]

### 2. 球体贴图

球体贴图也是单张贴图的形式，具体使用的方法与正方体大致相同，直接来看效果：

![此处输入图片的描述][3]

### 3. 多张图片的纹理贴图

还是以正方形为例，为每一个面贴不同的图，直接看代码：

      var materials = [];
      for (var i = 0; i < 6; ++i) {
           materials.push(new THREE.MeshBasicMaterial({
               map: new THREE.TextureLoader().load('images/' + i + '.png',
                       function() {
                           renderer.render(scene, camera);
                       }),
               overdraw: true
           }));
       }

      var cube = new THREE.Mesh(new THREE.CubeGeometry(5, 5, 5), materials);
      scene.add(cube);

贴图的效果为：

![此处输入图片的描述][4]

### 4. 重复式贴图

我们用一个棋盘格来描述这种重复式的贴图方式。

首先构建贴图平面：

    var cube = new THREE.Mesh(new THREE.PlaneGeometry(10,10), material);

然后设置横纵方向重复：

      texture.wrapS = texture.wrapT = THREE.RepeatWrapping;

同时设置横纵方向的重复次数：

     texture.repeat.set(4, 4);

横纵方向各重复4次，最后来看实际的效果：

![此处输入图片的描述][5]


  [1]: https://github.com/forthealllight/learn-threejs/blob/master/images/0.png
  [2]: https://github.com/forthealllight/learn-threejs/blob/master/images/met6.png
  [3]: https://github.com/forthealllight/learn-threejs/blob/master/images/met7.png
  [4]: https://github.com/forthealllight/learn-threejs/blob/master/images/met8.png
  [5]: https://github.com/forthealllight/learn-threejs/blob/master/images/met9.png
