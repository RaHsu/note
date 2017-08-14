title: casper快速入门指南
tags:
- JavaScript
- casperjs
---
最近在师兄的安利之下看了一下casperjs，发现它是一个不错的自动化工具，可惜官方并没有中文文档，所以在这里写个快速入门，方便大家快速的了解casperjs到底是个什么东西以及怎么样使用它。
<!--more-->

### 什么是casperjs？
caspersjs首页的官方介绍是：
> Navigation scripting & testing for PhantomJS and SlimerJS

也就是PhantomJs和SlimerJs的导航与测试脚本，有人可能就要问，那这个PhantomJs和SlimerJs又是什么东西呢？

PhantomJS 和 SlimerJS 都是服务器端的 JavaScript API 工具，可以理解为无界面的可编程操作的浏览器。 它们大部分的 API 接口都很相似，使用方法也很接近，最大的不同在于：PhantomJS 基于 Webkit 内核，不支持 Flash 的播放；SlimerJS 基于火狐的 Gecko 内核，支持 Flash播放，并且执行过程会有页面展示。

借助 PhantomJS 或 SlimerJS 所提供的 API，你几乎可以使用 javascript 模拟在浏览器上的任何操作：打开页面、前进/后退、页面点击、鼠标滚动、DOM 处理、CSS 选择器、Canvas 画布、SVG画图，如此等等。

那么casperjs和它们的关系是什么呢？就如同jqeury与js的关系一样，casperjs中封装了phantomJs和SlimerJs的常用操作，方便我们更简便快捷的调用api。

总的来说，casperjs可以帮助我们对页面进行测试和页面信息的抓取，虽然说它的正常用途是用来自动化测试的，但是用它来做爬虫也是一个不错的选择。

### 安装casperjs
在安装casperjs之前，你首先要确保你安装了[nodejs](https://nodejs.org/en/)和npm。（node.js里面自带npm，所以你只需要安装node.js就好了）

由于casperjs是基于phantomjs和Slimerjs的，所以你还需要先安装这两个组件。（建议你同时安装两个组件，这样的话你可以选择要不要看到页面过程的展示）

##### 安装phantomjs：
在npm的命令行中输入
```
$ npm install -g phamtomjs
```
（我个人偏向全局安装，这样你就可以在电脑任何地方运行这个程序了，当然你也可以选择在自己的工程目录里面安装，只需要去掉上面命令中的-g参数就行了）等待程序安装完成，在命名行中输入
```
$ phantomjs --version
```
如果出现了phantomjs的版本号信息，就说明你安装成功了。

##### 安装SlimerJs：
安装SlimerJS的流程和Phantomjs大同小异，同样在npm命令行中输入
```
$ npm install -g slimerjs
```
安装完成后，同样输入
```
$ slimerjs --version
```
看到版本号信息，说明你安装成功。
另外slimerjs是基于firefox内核的，所以需要你的电脑上安装有firefox浏览器。
##### 安装casperjs（需要python2.6以上支持）
```
$ npm install -g casperjs
```
同样的安装好以后查看它的版本信息
```
casperjs --version
```
这样所有的依赖我们都已经安装完毕，接下来看看如何使用casperjs。

### 使用casperjs
首先附上一段简短的代码：
```js
var casper = require('casper').create();
casper.start('http://www.baidu.com/');

casper.then(function() {
    this.echo('First Page: ' + this.getTitle());
});

casper.thenOpen('http://www.sina.com', function() {
    this.echo('Second Page: ' + this.getTitle());
});

casper.run();
```
这段简单的代码的功能是访问两个网站并打印出它们的首页标题。

将这段代码保存到test.js文件中，并在文件所在路径的命令行中输入：
```
$ casperjs test.js
```
你应该得到的输出是：
```
First Page: 百度一下，你就知道
Second Page: 新浪首页
```

值得注意的是，上面的命令行默认使用的引擎是phantomjs，如果你想使用slimerjs作为运行的引擎，像下面那样添加一个参数就可以了
```
$ casperjs tes.js  –engine=slimerjs
```
得到的输出结果与上面相同。

从上面的代码可以看出，casperjs的API非常的语言化，所以非常便于理解记忆和学习，更多的API选项可以去看casperjs的[官方文档](http://docs.casperjs.org/en/latest/)
当然文档只有英文的，所以我正在考虑要不要挖一个中文文档的坑。。。。。

好了，casper的入门就到这里，相信你已经安装好了casperjs并掌握了它的基本用法，要知道更多的信息，可以访问[casperjs的官网](http://casperjs.org/)，以及[casperjs的github](https://github.com/casperjs/casperjs)，祝大家学习愉快哦！
