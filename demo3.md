# Threejs官方文档-入门-（3）浏览器支持

------

## 1.概述

Threejs可以使用webGl，在现代浏览器中来渲染场景，对于老式的浏览器，特比是IE10以一下，为了支持Threejs，我们需要使用threejs中的其他渲染器（比如CSS2DRenderer, CSS3DRenderer, SVGRenderer, CanvasRenderer），此外，你可能需要额外的引入一些插件。


## 2.支持webgl的浏览器

Chrome 9+, Firefox 4+, Opera 15+, Safari 5.1+, Internet Explorer 11是支持webgl的

## 3.webgl使用了javascript中的一些新特性

Typed Arrays、Web Audio API、WebVR API、Blob、Promise、Fetch、File API、URL API、Pointer Lock API

如果浏览器不支持这些特性，那么需要额外的polyfill插件。推荐的插件有：

 - core-js
 - typedarray.js
 - ES6-promise
 - Blob.js
 - fetch
