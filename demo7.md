# threejs入门指南-（2）照相机详细介绍

------
我们知道同一个物体在场景中的展示效果，与照相机拍摄的角度有关，在threejs中提供了几种不同的照相机模型，本章具体分析一下正交投影模型和透视投影模型。

------

### 1. 照相机模型简单介绍

照相机模型常见的有两类，一类是正交投影模型，类似于平行光构建的模型，另一类是透视投影模型，类似于点光源构建的模型。

![两种不同的照相机模型][1]

上述就是两种照相机模型，（a）表示的是透视投影模型，而（b）表示的是正交投影模型。


### 2. 正交投影模型

（1）构造函数

我们先来了解一下正交投影模型，首先来看构造函数：

    THREE.OrthographicCamera(left, right, top, bottom, near, far)

这6个参数决定了照相机的渲染空间，在照相机渲染空间内的部分，称视景体，
只有视景体内的部分才能被渲染。

![正交投影模型][2]

在上述的图片中，灰色部分表示视景体，只有灰色的部分中的物体才能被观测到。在视景体的长方体中，长度表示为（right-left）,高表示为（top-bottom）,而宽表示为（far-near）。near表示照相机正向观测的最近距离，而far表示的是照相机正向观测的最远距离。

（2）正交模型举例

用一个场景中渲染一个正方体来举例说明照相机的正交投影模型，设置照相机为：

    var camera = new THREE.OrthographicCamera(-2, 2, 1.5, -1.5, 1, 10);
    camera.position.set(0, 0, 5);
    scene.add(camera);

创建一个边长为1的正方体：

    var cube = new THREE.Mesh(new THREE.CubeGeometry(1, 1, 1),
        new THREE.MeshBasicMaterial({
            color: 0xff0000,
            wireframe: true
        })
    );
    scene.add(cube);

得到的效果为：

![此处输入图片的描述][3]

看到的值一个类似于平面的正方形。如果长高比例不为4:3，比如为2:3那么得到的长方体被拉长了，效果为：

![此处输入图片的描述][4]

改变照相机的位置，会使得照相机发生平移：

    var camera = new THREE.OrthographicCamera(-2, 2, 1.5, -1.5, 1, 100);
    camera.position.set(1, 0, 5);

照相机向右，相当于观测到的物体，朝向为左边，具体效果为：


![此处输入图片的描述][5]

此外，我们也可以指定照相机在同一地点的不同的观测旋向，通过camera.lookAt方法来指定。

    camera.position.set(4, -3, 5);
    camera.lookAt(new THREE.Vector3(0, 0, 0));

我们将照相机移动到了位置（4,3,5）然后让其旋度指向观测（0,0,0）的方向。具体的效果为：

![此处输入图片的描述][6]

### 2. 透视投影模型

（1）构造函数

透视投影模型照相机的构造函数为：

    THREE.PerspectiveCamera(fov, aspect, near, far)

只包含了4个参数，这4个参数分别为张角和横纵比例。

![此处输入图片的描述][7]

在上图中，灰色部分就是表示的视景体，同样只有视景体内的物体才能够被渲染，fov表示张角，而aspect表示渲染器的横纵比。near和far同样表示的是最近观测距离和最远观测距离。

（2）透视投影模型举例

构造透视投影模型照相机：

    var camera = new THREE.PerspectiveCamera(45, 400 / 300, 1, 10);
    camera.position.set(0, 0, 5);
    scene.add(camera);

构建一个长度为1的正方体：

![此处输入图片的描述][8]

下面我们来看，改变张角之后的大小，将张角从45度变为60度则：

![此处输入图片的描述][9]

我们发现相对而言，正方体的大小变小了。实际上，增大张角，使得照相机看到的区域变大，也就是说增大了视景体的大小，而正方体的大小不变，所以看上去正方体显得变小了。

![此处输入图片的描述][10]

从上图中我们发现增大了张角之后，扩大了视景体。

  [1]: https://github.com/forthealllight/learn-threejs/blob/master/images/camera1.png
  [2]: https://github.com/forthealllight/learn-threejs/blob/master/images/camera2.png
  [3]: https://github.com/forthealllight/learn-threejs/blob/master/images/camera4.png
  [4]: https://github.com/forthealllight/learn-threejs/blob/master/images/camera5.png
  [5]: https://github.com/forthealllight/learn-threejs/blob/master/images/camera3.png
  [6]: https://github.com/forthealllight/learn-threejs/blob/master/images/camera7.png
  [7]: https://github.com/forthealllight/learn-threejs/blob/master/images/camera6.png
  [8]: https://github.com/forthealllight/learn-threejs/blob/master/images/camera8.png
  [9]: https://github.com/forthealllight/learn-threejs/blob/master/images/camera9.png
  [10]: https://github.com/forthealllight/learn-threejs/blob/master/images/camera10.png
