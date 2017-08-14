# 你不知道的JavaScript（中卷）

## 第一部分 类型和语法
### 第一章 类型
JavaScript并非没有类型，对于语言引擎和开发人员来说，类型是值的内部特征，它定义了值的行为，以使其区别于其他值。

#### 1.1 类型
强制类型转换是JavaScript开发人员最头疼的问题之一，它常被诟病为语言上的一个设计缺陷，应该束之高阁。

#### 1.2 内置类型
说出来你可能不信，JavaScript内置类型之一的null，它的`typeof`运算竟是
```js
typeof null === "object";   //ture
```

函数拥有一个[call]属性，使其可以被调用。

#### 1.3 值和类型
JavaScript中变量是没有类型的，只有变量才有，变量可以随时持有任何类型的值。
##### undefined和undeclared
变量在未持有值的时候为undefined，在未声明时为undeclared。
但使用`typeof`运算一个并没有声明的变量时，返回的结果却是undefined。
##### typeof undeclared
可以使用`typeof 变量名 === undefined`来检查一个变量有没有被声明。

### 第2章 值
#### 2.1 数组
使用`delete`运算符可以将单元从数组中删除，但数组的length属性不会变化。

使用es6中的`Array.form()`函数可以将类数组转化为数组。

#### 2.2 字符串
字符串是不可变的，而数组是可变的。

#### 2.3 数字
JavaScript中的number类型均为浮点数，没有真正意义上的整数。

##### 较小的数值
由于number均为浮点数，所以JavaScript在处理小数运算时需要设置一个机器精度，对JavaScript来说，这个值通常是2^-52。

从es6开始，这个值定义在`Number.EPSILON`中。可以使用这个值来比较两个浮点数。(在机器精度之内)
```js
function numbersEqual(a,b){
    return Math.abs(a-b) < Number.EPSILON;
}
```

#### 2.4 特殊数值
`undefined`和`null`既是类型也是值。

##### void运算符
表达式`void`没有返回值，也就是说，它返回的值为`undefined`。
```js
var a = 4;
console.log(void a);  // undefined
```
##### NaN
NaN是一个特殊值，也是唯一一个和自身不相等的值。

要判断NaN，只能使用JavaScript内置的方法`Number.isNaN()`。

##### 特殊等式
要对付上面的一些特殊情况，es6引入了`Object.is()`函数，可以准确的对两个数值做出是否相等的判断。

#### 2.5 值和引用
简单值（`null`,`undefined`,字符串，数字，布尔和`symbol`）都是通过值复制。

复合值（对象，数组，函数）是通过复制引用的方式传值。

### 第三章 原生函数
通过构造函数（如`new String('abc')`）创建出来的是封装了基本类型值的封装对象。也就是说，它们的`typeof`运算结果是`object`。

#### 3.1 内部属性[[Class]]
所有typeof返回值为Object的对象都有一个内部属性[[Class]]，你可以使用`Object.prototype.toSting()`来查看。

#### 3.2 封装对象包装

#### 3.3 拆封
如果想要得到封装对象中的基本类型值，可以使用`valueOf()`函数。

#### 3.4 原生函数作为构造函数
应该尽量避免使用构造函数，除非十分必要，因为它们经常会产生意想不到的结果。

永远不要创建和使用空单元数组。

除非万不得已，尽量不要使用`Object()`/`Function()`/`RegExp()`。

### 第4章 强制类型转换

#### 4.1 值类型转换
#### 4.2 抽象值操作
##### JSON字符串化
不安全的JSON值有：有defined，function，symbol和包含循环引用的对象。JSON将无法处理它们。
##### 假值列表
- undefined
- null
- false
- +0、-0和NaN
- ""

除此以外均为真值。

#### 4.3 显式强制类型转换
`Number()`和`parseInt()`具有相同的功能：将字符串转换为数字，但是，`Number()`不允许在字符串中出现非数字字符，否则转换结果为`NaN`，所以要根据具体需求选择函数。

#### 4.4 隐式强制类型转换
JavaScript中`| |`和`&&`运算符并不总是返回布尔值，而是两个操作数中的一个值。

#### 4.5 宽松相等和严格相等
千万不要使用`==true`和`==false`，这样的运算有时会产生意想不到的结果。

#### 4.6 抽象关系比较

### 第五章 语法
#### 5.1 语句和表达式
`else if`并不是JavaScript里面的语法，只是大家习惯了这样使用，但是这个语句没有语法错误。

#### 5.2 运算符优先级
#### 5.3 自动分号
#### 5.4 错误
`let`没有变量提升，所以不要在声明之前使用这个变量。

#### 5.5 函数参数
#### 5.6 try...finally
`finally`中的`return`会覆盖`try`和`catch`中`return`的值。

#### 5.7 awitch
