# Threejs官方文档-入门-（5）画线

------

如果我们现在需要画一条线、一个圆，而不是一个通过网格构成的模型。同样我们需要建立渲染器（renderer）,场景（scene）和相机（camera）。

我们使用的代码如下所示：

      var renderer=new THREE.WebGLRenderer();
      renderer.setSize(window.innerWidth,window.innerHeight);
      var camera=new THREE.PerspectiveCamera(45,window.innerWidth/window.innerHeight,1,500);
      camera.position.set(0,0,100);
      camera.lookAt(new Three.Vector3(0,0,0));
      var scene=new Three.Scene();

接着，我们需要定义个材料（material），对于线条我们需要使用的material类型为： LineBasicMaterial和 LineDashedMaterial。

    //创建一个蓝色的LineBasicMaterial
    var material = new THREE.LineBasicMaterial( { color: 0x0000ff } );

使用了材料（material）之后，我们需要使用几何模型（Gemotry）,我们可以采用的几何模型有Gemotry或BufferGeometry.我们可以采用几何模型去构建边。

    var geometry = new THREE.Geometry();
    geometry.vertices.push(new THREE.Vector3( -10, 0, 0) );
    geometry.vertices.push(new THREE.Vector3( 0, 10, 0) );
    geometry.vertices.push(new THREE.Vector3( 10, 0, 0) );

线是通过连续的顶点对间相连组成的，但是不会连接起点和终点，从上述的代码中，我们有了两对顶点，这样就可以通过这两对顶点和材料（material）来生成边。

    var line = new THREE.Line( geometry, material );

最后，构建完这个线之后，我们接着做的就是在场景中添加这些线，并且通过renderer方式渲染：

    scene.add( line );
    renderer.render( scene, camera );

最后我们来看构建的结果：

![此处输入图片的描述][1]


  [1]: https://github.com/forthealllight/learn-threejs/blob/master/images/demo5.png
