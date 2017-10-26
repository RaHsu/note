title: ES6学习笔记-箭头函数
---
箭头函数是ES6中一个新增的特性，今天我们就来看看它是如何使用的。
<!--more-->

### 基本用法

ES6 允许使用“箭头”（=>）定义函数。
```js
var f = v => v;
```
等同于
```js
var f = function(v) {
  return v;
};
```
我们可以看到箭头前面的 v 是作为函数的参数，箭头后面的 v 是作为函数的返回值，那么箭头函数的结构差不多就明了了。

如果你不需要参数，或需要多个参数，就使用一个圆括号在参数部分，也就是箭头的前面：
```js
var sum = (num1, num2) => num1 + num2;
// 等同于
var sum = function(num1, num2) {
  return num1 + num2;
};
```

通过之前的例子我们可以知道，箭头后面的内容就是函数要返回的内容，但这仅限于函数体用一句语句就可以解决的情况，如果函数体拥有一句以上的语句，你需要将函数体中的语句用大括号括起来，并仍然需要使用`return`语句将返回值返回：
```js
var sum = (num1, num2) => { return num1 + num2; }
```

如果你想要返回一个对象，必须用括号将这个对象括起来：
```js
var id = x =>({ id : x , name : 'name' })
```

箭头函数可以与变量解构结合使用。
```js
const full = ({ first, last }) => first + ' ' + last;

// 等同于
function full(person) {
  return person.first + ' ' + person.last;
}
```

### 箭头函数的作用

对于箭头函数的作用，个人认为有三点：

1. 箭头函数使函数的表达更为简洁。
    对于简单的一些功能函数，箭头函数相比于传统函数的表达更为简洁，并且代码量也更少，通常只需要一行。

2. 简化回调函数：

    ```js
        // 正常函数写法
    [1,2,3].map(function (x) {
      return x * x;
    });

    // 箭头函数写法
    [1,2,3].map(x => x * x);
    ```
    这样使代码更加简洁也更加易读。

3. 箭头函数可以将this对象绑定在定义时的作用域中，这种特性非常利于封装回调函数：
```js
var handler = {
  id: '123456',

  init: function() {
    document.addEventListener('click',
      event => this.doSomething(event.type), false);
  },

  doSomething: function(type) {
    console.log('Handling ' + type  + ' for ' + this.id);
  }
};
```
上面代码的`init`方法中，使用了箭头函数，这导致这个箭头函数里面的`this`，总是指向`handler`对象。否则，回调函数运行时，`this.doSomething`这一行会报错，因为此时`this`指向`document`对象。

### 使用箭头函数时要注意
1. 函数体内的`this`对象，就是定义时所在的对象，而不是使用时所在的对象。
2. 不可以当作构造函数，也就是说，不可以使用`new`命令，否则会抛出一个错误。
3. 不可以使用`arguments`对象，该对象在函数体内不存在。如果要用，可以用 `rest`参数代替。
4. 不可以使用`yield`命令，因此箭头函数不能用作 Generator 函数。

这大概就是对箭头函数的大致介绍了，其他的还要小伙伴们自己去探索，祝大家学习愉快哦。
