tilte: fun fact about null
---
最近在看《你不知道的JavaScript》这本书，发现了一些关于null的有趣事实。
<!-- more -->

众所周知，JavaScript有7种基本类型：null,undefined,object,number,string,boolean,symbol(es6新增)，这7种数据类型中，null表示空值，它也是比较特殊的一个数据类型。

说出来你可能不信，对null进行`typeof`的结果竟然是。。。
```js
typeof null === "object"  // true
```
欸！！？？（黑人问号脸）

这应该算是JavaScript的一个bug，但是书上说这个bug由来已久，在JavaScript里存在了近20年，也许永远的不会修复，因为这牵涉到太多的web系统，要是修复的话可能会产生更多的bug。

那么问题来了，如何判定一个变量的类型是null呢？（如果typeof运算对其返回object的话）

答案是：需要使用符合条件对齐进行判定：
```js
var a = null;
(!a && typeof a ==="object");  // true
```

null是所有基本类型中唯一的一个假值（也就是说`!null===true`)，但typeof对它的返回值是object。

还有一个有趣的事实是，虽然`function`是`object`的一个子类型，但`typeof`对其的返回值是`function`而不是`object`，至于其他`object`的子类型，例如`Array`，就没有这么特殊的待遇了，`typeof`对它们的返回一律是`object`。

尽管null是不常使用的一个基本类型，但是一旦用上了，要是不熟悉这个特点的话，调bug可是一件非常痛苦的事情啦。

最后想大家安利这本书[你不知道的JavaScript](http://www.ituring.com.cn/book/1488)，里面讲了好多关于JavaScript的细节问题，如果想要学好JavaScript的话，这些细节可是不容忽视的哦！
