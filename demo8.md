# Threejs入门指南-（3）几何形状

------

了解了照相机模型之后，我们来看几何形状（Geometry），因为在场景中的物体实际上都是由一定的几何形状构成的，几何形状有点和边等等，本节分别介绍一下不同的几何形状的构造函数

------


### 1. 基本几何形状的构造

（1）立方体

首先来看立方体的构造函数：

    THREE.CubeGeometry(width, height, depth, widthSegments, heightSegments, depthSegments)

参数解释，width，height,depth分别长高深，后面的widthSegments，heightSegments,depthSegments分别表示了在相应方向的切片的数目。几何形状的默认位置是原点，原点位于立方体的中心。

没有切片的情况下，如下所示：

![此处输入图片的描述][1]

存在切片的情况下：

![此处输入图片的描述][2]

（2）有限的平面

有限大小的平面的构造函数为：

    THREE.PlaneGeometry(width, height, widthSegments, heightSegments)

平面的参数比较简单，就不具体距离，参数width和height分别表示宽度和高度，而widthSegments和heightSegments分别表示两个方向上的切片的数目。

（3）球体

来看球体的构造函数：

    THREE.SphereGeometry(radius, segmentsWidth, segmentsHeight, phiStart, phiLength, thetaStart, thetaLength)

上面的参数中，radius表示的半径，segmentsWidth表示经度上的切片数，而segments表示纬度上的切片数，phiStart表示经度开始的弧度，phiLength表示经度所跨越的弧度，thetaStart表示纬度开始的弧度，thetaLength表示纬度所跨域的弧度。

来看效果：

![此处输入图片的描述][3]

接着来看切片更多的效果，比如有更多切片的情况：

    new THREE.SphereGeometry(1,20,20)

效果为：

![此处输入图片的描述][4]

经度和弧度的参数，我们来看修改经度和纬度的例子：

![此处输入图片的描述][5]

（4）圆形、圆形、圆台

这些的构造函数可以参考API，不具体描述。

  [1]: https://github.com/forthealllight/learn-threejs/blob/master/images/geo1.png
  [2]: https://github.com/forthealllight/learn-threejs/blob/master/images/geo2.png
  [3]: https://github.com/forthealllight/learn-threejs/blob/master/images/geo3.png
  [4]: https://github.com/forthealllight/learn-threejs/blob/master/images/geo4.png
  [5]: https://github.com/forthealllight/learn-threejs/blob/master/images/geo5.png
