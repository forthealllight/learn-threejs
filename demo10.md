# 材质

------

通过几何（Geomety）构建了物体之后，实现完整的渲染，必须要提供材质，我们要可以通过材质（Material）来给物体增加颜色、纹理和光照等等。threejs提供了很多种材质，本节简要介绍一下基本材质、Lambert和Phong材质等

------



### 1. 基本材质

基本材质很简单，类似于我们的2D绘图，不会有任何的光照、阴暗等变化，指定了渲染颜色之后，就直接展示出来，比较单一。

同样以填充一个正方体为例，基本材质的构造方法为：

    THREE.MeshBasicMaterial(opt)

构造一个正方体：

      var cube = new THREE.Mesh(new THREE.CubeGeometry(1,1,1),
        new THREE.MeshBasicMaterial({
          color: 0xffff00,
          opacity: 0.75
        })
    );

填充的颜色为黄色，且设置了透明度，结果为：

![此处输入图片的描述][1]

构造函数opt对象里的常用参数:

 - value:是否可见，默认为可见
 - side:确定是正片渲染还是反片渲染
 - wireframe：是否为渲染线，默认为false，是面渲染
 - color:确定渲染的材质颜色
 - map：纹理贴图


### 2. Lambert材质

（1）反射的概念

Lambert材质就跟基础材质不同，存在着光照等情况，这里我们明确一下两个反射的概率，不同的物体对光的反射不同，也就对应不同的材质修饰的物体，决定了物体对光照的反射性质。

反射分为：漫反射和镜面反射

 - 漫反射：入射光入射到粗糙物体的表面，反射光会想不同的方向反射，反射光的无规则性，也称为漫反射或者慢射，常见的会发生漫反射的物体有衣物、墙壁、植物等等。
 - 镜面反射：入射光入射到光滑的物体表面，反射光会在另一个平行的方向反射出来，反射方向是一直的，因此光强比较集中，常见的镜面反射的例子有镜子、金属表面、玻璃等等。

Lambert材质只考虑了漫反射而不考虑镜面反射，因此比较适合修饰的物体是具有粗糙表面的物体。

 （2）Lambert材质举例

 指定光源后，我们这里用的是点光源，关于光源将在以后介绍，首先引入点光源：


      var light = new THREE.PointLight(0xffffff, 2, 100);
      light.position.set(0, 1.5, 2);
      scene.add(light);

然后添加一个Lambert材质的物体，并进行渲染：

    var cube = new THREE.Mesh(new THREE.CubeGeometry(2, 2, 2),
      new THREE.MeshLambertMaterial({ color: 0xffff00})
  );

 渲染结果：

 ![此处输入图片的描述][2]

Lambert材质的参数：

 - color:颜色
 - ambient：对环境光的反射能力
 - emissive：自发光颜色。

（3）emissive参数举例

可以通过emissive设置自发光属性：

    var cube = new THREE.Mesh(new THREE.CubeGeometry(2, 2, 2),
          new THREE.MeshLambertMaterial({ color: 0xffff00,emissive:0xff0000})
      );
效果为：

![此处输入图片的描述][3]

### 3. Phong材质

Phong材质和Lambert材质不同，Phong材质考虑了镜面反射效果，因此可以用于修饰存在镜面反射的物体。如果不设置反射系数的情况下，Phong材质和Lambert材质是相同的。

（1）Phong材质举例

可以通过设置反射系数等，设置Phong材质的反射效果，我们以球体为例，首先指定材质，通过specular指定反射系数：

    var material = new THREE.MeshPhongMaterial({
        color: 0xffffff,
        specular: 0xffff00,
        shininess: 100
    });

效果为：

![此处输入图片的描述][4]

shininess用于指定光斑的大小，且值越大光斑越小，比如当shininess的值为1000时：

        var material = new THREE.MeshPhongMaterial({
            color: 0xffffff,
            specular: 0xffff00,
            shininess: 1000
        });
效果为：

![此处输入图片的描述][5]

### 4. 法向材质

法向材质用于将材质颜色设置成其法向方向。用于调试，这里简单概括，其构造函数为：

    new THREE.MeshNormalMaterial()



  [1]: https://github.com/forthealllight/learn-threejs/blob/master/images/met1.png
  [2]: https://github.com/forthealllight/learn-threejs/blob/master/images/met2.png
  [3]: https://github.com/forthealllight/learn-threejs/blob/master/images/met3.png
  [4]: https://github.com/forthealllight/learn-threejs/blob/master/images/met4.png
  [5]: https://github.com/forthealllight/learn-threejs/blob/master/images/met5.png
