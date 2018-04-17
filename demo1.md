# Threejs官方文档——（1）创建一个场景

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
