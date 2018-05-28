## 高性能JavaScript

### 第一章  加载和执行

#### 脚本位置

由于脚本阻塞的存在，建议将所有`<script>`标签尽可能放到 `<body>` 标签的底部，以减少对整个页面下载的影响。

#### 组织脚本

减少脚本的HTTP请求数量，你可以将脚本合并。文件合并的工作可以通过离线的打包工具或者类似Yahho!combo handler的实时在线服务来实现。

#### 无阻塞的脚本

在页面加载完成后再加载JavaScript代码，也就是在window对象的load事件触发后再下载脚本。

#### 延迟的脚本

将无需修改DOM的脚本加上async属性，用于异步加载脚本。

#### 动态脚本元素

你可以使用DOM对象来动态的加载一个脚本：

```js
var script = document.createElement("script");
script.src = "file.js";
```

使用动态脚本下载文件时，返回的代码通常会立即执行。如果你要动态加载多个脚本文件，一定要考虑清楚文件的加载顺序。并不是所有的浏览器都会保证以你添加脚本的顺序来执行代码，那取决于服务器的返回时间。

#### XMLHttpRequest脚本注入

也就是通过Ajax来加载脚本文件。这种方法的优点在于你可以下载JavaScript代码但不立即执行。

#### 推荐的无阻塞模式

向页面中添加大量JavaScript的推荐做法只需两步：

1. 添加动态加载所需代码。
2. 加载初始化页面所需代码。

```html
<script src="loader.js"></script>
<script>
    loadScript("the-rest.js",function(){
        Application.init();
    });
</script>
```



### 第二章  数据存取









