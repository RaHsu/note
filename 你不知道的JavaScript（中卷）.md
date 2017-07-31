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
