# Threejs官方文档-入门-（4）webgl兼容性检测

------

虽然大多数浏览器已经开始支持webgl，但是始终有一些浏览器对webgl的支持性不好，我们提供了下列的方法，用于检测浏览器是否支持webgl，如果不支持则给出提示。

首先，在我们的js文件中引入https://github.com/mrdoob/three.js/blob/master/examples/js/Detector.js，执行下面的代码观察输出情况。

    if (Detector.webgl) {
    // Initiate function or other initializations here
    animate();
    } else {
        var warning = Detector.getWebGLErrorMessage();
        document.getElementById('container').appendChild(warning);
    }

其中animate方法是（1）中的demo样例。
