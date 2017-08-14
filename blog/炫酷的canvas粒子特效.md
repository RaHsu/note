title: 炫酷的Canvas粒子特效
---
随着html5`Canvas`元素的推出呢，现在的浏览器具备了更强大的绘制图像的功能，甚至`canvas`已经可以用来制作大型网页游戏，关于`Canvas`的js库也越来越多，有动画库还有图表库比如Echart等等。今天我就要给大家推荐两款非常炫酷的`Canvas`粒子特效，let's hit the road!

### Particleground粒子背景
articleground是一款时髦的jquery粒子系统背景插件，PC端可通过鼠标控制视差效果，而移动端可用重力感应控制，Particleground可以运行在任何支持html5 canvas的浏览器上。

大家可以先[看看效果](http://jnicol.github.io/particleground/)。

怎么样是不是很炫酷！！那么要使用这个特效也是非常的简单。

首先放上项目的[github地址](https://github.com/jnicol/particleground)。把代码clone下来到本地。然后引入它。
```html
<script type='text/javascript' src='jquery-3.0.0.min.js'></script>
<script type='text/javascript' src='jquery.particleground.min.js'></script>
```
注意这个组件是基于jQuery的，所以在你也需要引入JQuery文件。

然后在html里面添加一个Canvas容器：
```html
<div id="particles"></div>
```
最后在js中将它初始化：
```js
$('#particles').particleground();
```
这样你的设置就完成了

当然你也可以设置参数：
```js
$('#particles').particleground({
dotColor: '#ff0000',    // 点的颜色
lineColor: '#ff0000'   //  线的颜色
});
```
更多具体的参数请参阅官方文档。

### canvas-nest.js粒子背景
接下来是另一款粒子背景，它和上面的 Particleground 有些不一样，粒子并不是随机分散的而是聚集在鼠标的周围，这样可以很清除的反应鼠标的位置。

[在这里](http://www.atool.org/)查看背景预览。

使用这款组件非常的容易，只需要在你的页面中加入这段代码即可（注意要放在body里面）
```html
<script src="//cdn.bootcss.com/canvas-nest.js/1.0.1/canvas-nest.min.js"></script>
```
是不是异常的简单！！

当然你也可以下载文件到本地，[这里](https://github.com/hustcc/canvas-nest.js)是项目的地址。

同样的你可以设置动画参数，只需要在script标签里面添加就行了，像这样：
```html
<script type="text/javascript" color="0,0,255" opacity='0.7' zIndex="-2" count="99" src="//cdn.bootcss.com/canvas-nest.js/1.0.1/canvas-nest.min.js"></script>
```
上面的参数分别是线条颜色、线条透明度、z轴值、以及粒子个数。

更多的参数请参阅项目文档。

要提醒一点的是，不管你使用哪个组件，不要将粒子的数量设置得太多，这样浏览器的性能会跟不上，毕竟图像绘制还是很吃性能的，浏览器甚至还会崩溃卡死。

好了，就介绍到这里了，祝各位小伙伴玩得愉快哦。
