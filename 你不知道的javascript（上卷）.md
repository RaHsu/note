## 第一章 作用域是什么
### 1.1 编译原理
javascript实际上是一门编译语言。  

在传统的编译语言流程中，编译的三个步骤：
* 分词/词法分析
* 解析/语法分析
* 代码生成   


javascript的编译过程比一般的编译语言要复杂得多。

### 1.2 理解作用域
#### 1.2.1 演员表
* 引擎：负责javascript的编译及执行过程。
* 编译器：负责语法分析及代码生成。
* 作用域： 负责收集并维护由所有声明的标识符组成的一系列查询，确定代码对标识符的访问权限。
#### 1.2.2 对话
对于`var a=2;`这段代码，编译器会先将a声明，然后查找变量并赋值。
#### 1.2.3 编译器有话说
* **LHS** 从左侧开始查找---赋值操作的目标是谁（找容器）
* **RHS** 从非左侧开始查找---谁是赋值操作的源头 （找到容器中的值）
#### 1.2.4 引擎和作用域的对话

### 1.3 作用域嵌套
**作用域** 是根据名称查找变量的一套规则。 

遍历作用域规则：总是从当前作用域开始查找变量，如果找不到，就继续向上一级继续查找，直到最全局作用域。

### 1.4 异常
如果RHS查询在所有嵌套的作用域中寻遍不到所需变量，引擎就会抛出`ReferenceError`异常。  

>在严格模式中，进行LHS查询也会发生这样的事情。    

## 第二章 词法作用域
### 2.1 词法阶段
词法作用域就是定义在词法阶段的作用域。

>作用域查找会在找到第一个匹配的作用域后停止。

词法作用域查找只会查找一级标识符。

### 2.2 欺骗词法

欺骗词法会导致性能下降，所以并不推荐使用。

#### 2.2.1 eval

# 第五章 作用域闭包
### 5.4 循环和闭包
看下面一段代码：
```
for(var i=1;i<=5;i++){
	(function(j){
		setTimeout(function timer(){
			console.log(j);
		},j*1000);
	})(i);
}
```
这是一个经典的闭包循环，这里的i作为参数，它的作用域被j引入了，所以并不会出现输出5个6的情况。
但是有了`let`之后，情况变得大不一样，你大可以这样写：
```
for(let i=1;i<=5;i++){
	setTimeout(function timer(){
		console.log(i);
	},i*1000);
}
```
### 5.5 模块
模块模式需要具备的两个条件：
1. 必须有外部的封装函数。
2. 封闭函数必须返回至少一个内部函数。
#### 5.5.1 现代的模块机制
下面是一个模块创建器：
```
var myModules=(function Manager(){
	var modules={} //创建一个对象

	function define(name,deps,impl){  // 这里的参数分别是模块名，继承的模块名和具体的函数
		for(var i=0;i<deps.length;i++){
			deps[i]=modules[deps[i]];
		}
		modules[name]=impl.apply(impl,deps);
	}

	function get(name){
		return modules[name];
	}

	return{
		define:define,
		get:get
	};
})();
```
#### 5.5.2未来的模块机制
es6的模块没有行内机制，必须被定义在独立的文件中（一个文件一个模块）。
# 第二部分 this和对象原型
***
# 第一章 关于this
### 1.1 为什么要使用this
this提供了一种更优雅的方式来隐式传递了一个对象引用，因为当模式越来越复杂时，显式的传递上下文对象会让代码变得混乱。
### 1.2 误解
#### 1.2.1 指向自身
this并不像我们想的那样指向函数自身。
匿名函数无法通过名称标识符引用自身，所以最好使用具名函数。
可以使用call方法强制让作用域指向一个对象。
#### 1.2.2 它的作用域
第二种常见的误解是：this指向函数的作用域。我们要明确，this在任何情况下都不指向函数的词法作用域。
### 1.3 this到底是什么
当一个函数被调用时，会创建一个活动记录，这个记录会包含函数在哪里被调用（调用栈），函数的调用方式，传入的参数等信息，this就是这个记录的一个属性，会在函数的执行过程中用到。
# 第二章 this全面解析
### 2.1 调用位置
调用位置就是函数在代码中被调用的位置（而不是声明的位置）。
调用栈决定了this的绑定。
### 2.2 绑定规则
#### 2.2.1 默认绑定
当一个函数直接使用不带任何修饰的函数引用进行调用时，使用默认绑定的规则，这时this指向全局对象。
如果使用严格模式，则不可以将this绑定到全局对象。
#### 2.2.2 隐式绑定
```
function foo(){
	console.log(this.a);
}
var obj={
	a:2,
	foo:foo
};
obj.foo();
```
像这样函数前面有修饰词的，调用foo时，this则被绑定给了obj。
**回调函数会丢失this绑定**。
### 2.3.3 显式绑定
显式绑定即使用`call`和`apply`方法。
```
function foo(){
	console.log(this,a);
}
var obj={
	a:2
};
foo.call(obj);
```
那么如何解决绑定丢失的问题呢？
1. 硬绑定
即在一个函数中为另一个函数绑定作用域，这样这个函数的作用域一旦绑定，就不可以再更改了。
```
function foo(){
        console.log(this.a);
    }
    var obj = {
        a:2
    }
    var bar = function(){
        foo.call(obj);  //在另一个函数中绑定对象，将foo绑定在obj这个对象上。
    }
    bar();
    setTimeout(bar,100);

    bar.call(window);  // 则这个绑定无效
```
由于硬绑定十分常用，所以硬绑定有它的专属函数：`bind()`
```
function foo(something){
	console.log(this.a,something);
	return this.a+something;
}
var obj={
	a:2
}
var bar = foo.bind(obj);  // 将foo与obj函数绑定，并返回一个新函数
var b = bar(3);
console.log(b)  // 5 
```
2. API调用的上下文
许多第三方库的`getContext()`函数，实际上就是这样的硬绑定。
#### 2.4.2 new绑定
使用new来调用函数，会自动执行以下操作：
1. 创建一个全新的对象。
2. 这个新对象会被执行[[Prototype]]连接。
3. 这个新对象会绑定到函数调用的this。
4. 如果函数没有返回其他对象，那么new表达式中的函数调用会自动返回这个新对象。

### 2.3 优先级
new绑定>显式绑定>隐式绑定>默认绑定。

### 2.4 绑定例外
#### 2.4.1 被忽略的this
如果你将null或undefined作为this的绑定对象并传入call，apply或bind，比如`foo.call(null);`，实际应用的是默认绑定规则。
那么哪些情况下你会传入null呢？
1. 使用apply展开数组
```
foo.apply(null,[2,3]);
```
2. 使用bind进行函数柯里化
```
var bar = foo.bind(null,2);
```
显而易见，这些方法会导致很多难以分析和追踪的bug。
##### 更安全的this
解决这个问题的方法是：将this绑定到一个你自己创建的空对象上。
#### 2.4.2 间接引用
你可能会有意无意的使用间接引用，在这种情况下，调用这个函数会应用默认绑定规则。
间接引用最容易在赋值时发生：
```
function foo(){
	console.log(this,a);
}
var a = 2;
var o = {a: 3,foo:foo};
var p = {a: 4};
o.foo(); // 这里的输出是3，也就是说this此时是指向o对象的
(p.foo=o.foo)() //这里的输出是2，由于o.foo返回的是目标函数的引用，所以此时的this指向window。
```
#### 2.4.3 软绑定
通过前面的章节，我们知道了硬绑定一旦绑定了就不可以再修改绑定，这样会降低函数的灵活度。

软绑定可以被隐式绑定或显式绑定修改：

```
if(!Function.prototype.softBind){
	Function.prototype.softBind = function(obj){
	var fn = this;
	// 捕获所有柯里参数
	var curried = [].slice.call(argument,1);
	var bound = function(){
	return fn.apply(
		(!this||this===(window||global))?obj:this,
		curried.concat.apply(curried,argument)
	);
};
bound.prototype = Object.create(fn.prototype);
return bound;
};
}
```
### this词法
es6中引入了一中无法使用这些规则的特殊函数类型：函数箭头`=>`.

箭头函数不使用以上的函数规则，而是根据外层作用域来决定this。

```
function foo(){
	return (a)=>{
	console.log(this.a);
};
}
var obj1={a:2};
var obj2={a:3};
var bar=foo.call(obj1); //这里使用了显式绑定
bar.call(obj2); //结果为2，箭头函数的绑定无法被修改，即使是new也不行。
```

# 第三章 对象
### 3.1 语法
对象的两种定义方式：
1. 声明形式
2. 构造形式

### 3.2 类型
javascript的六种主要类型：
* srting
* boolean
* number
* undefine
* null
* object

函数是对象的一个子类型，它本质上和普通的对象一样，只是可以调用，所以可以像操作其他对象一样操作函数。

函数也是对象的一个子类型。

#### javascript中的内置对象
* String
* Number
* Boolean
* Object
* Function
* Array
* Date
* RegExp
* Error
在javascript中，它们实际上是一些内置函数。这些内置函数可以当作构造函数来使用。

### 3.3 内容
可以使用两种方法访问对象的属性：
1. `obj.property`
2. `obj["property"]`

在对象中，属性名永远是字符串。

#### 3.3.1 可计算属性名
es6引入可计算属性名，可以在文字形式中使用[]包裹一个表达式：
```
var foo="wo";
var obj={
	[foo+'hh']:1
};
console.log(obj["wohh"]); // 1
```

#### 3.3.2 属性与方法
严格来说，一个函数不会属于一个对象，只有当函数中包含this引用时，这个引用会绑定到一个对象上。

即使你在对象的文字形式中声明一个函数，这个函数也不会属于这个对象，它们只是对相同函数对象的多个引用。

#### 3.3.3 数组
数组也是对象，所以你可以给它添加属性。

最好使用对象储存键值对，用数组储存索引/值对。

#### 3.3.4 复制对象
es6定义了object.assign()方法来实现浅复制，第一个参数为目标对象，后面的参数为可选多个源对象。
```
var newObj = object.assign({},oldObj);
```

#### 3.3.5 属性描述符
```
var myObj = {
	a:2
};

Object.getOwnPropertyDescriptor(myObj,"a");
Object.defineProperty(myObj,"a",{
	value:2,
	writable:true,  // 属性值是否可修改
	configurable:true, // 属性配置是否可以通过defineProperty函数来改变
	enumerable:true  // 是否出现在对象的属性枚举中，比如for in 循环
});
```
#### 3.3.6 不变性

1. 对象常量
结合`writable：false`和`configurable:false`就可以创建一个真正的常量属性（不可修改，重定义和删除）。

2. 禁止扩展
使用`Object.preventExtensions()`可以禁止一个对象添加新属性

3. 密封
`Object.seal()`，密封之后不能添加新属性，也不能重新配置和删除属性。

4. 冻结
`Object.freeze()`, 代表着最高级别的不可变性，它会禁止对对象属性的任意修改。

#### 3.3.7 [[Get]]

当进行`obj.a`这样的属性访问时，实际上是在obj上实现了`[[Get]]`操作，它首先在对象中查找是否有名称相同的属性，如果找到就返回这个属性的值，如果没有找到，就会遍历可能存在的原型链。

#### 3.3.8 [[Put]]

#### 3.3.9 Getter和Setter
getter是一个隐藏函数，会在获取属性值时调用，setter也是一个隐藏函数，会在设置属性值时调用。

你可以定义它们，但是不要只定义一个，它们应该是成对出现的。

#### 3.3.10 存在性

`in`操作符检查属性是否在对象及其原型链中，`hasOwnProperty()`只检查属性是否存在于对象中。

##### 枚举

通过`enumerable`属性可以设置某个属性是否可以被枚举。

> 不要在数组上使用for in 枚举，会产生意想不到的结果，应该使用传统for循环来遍历数组。

`object.keys()`会返回一个数组，包含所有可枚举的属性。（不查找原型链）

### 3.4 遍历

es6新增for of循环，可以直接遍历数组中的值。
```
var array=[1,2,3];

for(var v of array){
	console.log(v);
}
```

# 第四章 混合对象‘类’

### 4.1 类理论

面向对象编程强调的是数据和操作数据的行为本质上是相互关联的。因此好的设计是把数据以及和它相关的行为打包。

类的另一个核心概念是多态，就是说父类的通用行为可以被子类用更特殊的行为重写。

#### 4.1.1 ‘类’设计模式

#### 4.1.2 javascript中的‘类’

javascript实际上并没有类，只是通过一些方法实现了类的功能。

### 4.2 类的机制

#### 4.2.1 建造

类通过复制操作被实例化为对象形式。

#### 4.2.2 构造函数

类构造函数属于类，而且通常和类同名。此外，构造函数大多需要new来调用，这样引擎才知道你想要构造一个新实例。

### 4.3 类的继承

#### 4.3.1 多态

在javascript中，多态并不表示子类和父类有关联，子类得到的只是父类的一个副本，类的继承其实就是复制。

#### 4.3.2 多重继承

javascript本身并不提供“多重继承”功能，不过一些方法可以实现类似的效果。

### 4.4 混入
javascript想出的一个方法来模拟类的行为，这个方法就是混入。

#### 4.4.1 显式混入
通过mixin()函数显示的复制对象中的属性：
```
function mixin(sourceObj,targetObj){
	for(var key in sourceObj){
	if(!(key in targetObj)){
		targetObj[key]=sourceObj[key];
}
}
return targetObj;
}
```
##### 再说多态
使用伪多态会导致代码难以维护，所以应该尽量避免使用显式伪多态。

##### 混合复制
javascript中的函数无法真正的复制，所以你只能复制对共享函数的引用。如果你修改了共享函数对象，就会对所有引用它的对象产生影响。

##### 寄生继承
寄生继承指的是，先先复制一份父类对象的定义，然后混入子类对象的定义，然后用这个复合对象构造实例。

#### 4.4.2 隐式混入

# 第五章 原型
### 5.1 [[Prototype]]
javascript中的对象有一个特殊的[[Prototype]]内置属性，其实就是对于其他对象的引用，当要查找的属性在这个对象中不存在时，引擎就会沿着这个引用（也就是原型链）继续向上查找。

当你使用for in函数遍历对象时，for in函数也会查找整个原型链。

#### 5.1.1 object.prototype
所有普通的[[prototype]]链最终都会指向内置的object.prototype对象，它包含很多javascript里通用的功能。

#### 5.1.2 属性设置和屏蔽
尽量在设置属性时避免属性覆盖，（就是说原型链上层拥有与这个对象同名的属性）。

### 5.2 “类”
javascript中只有对象，没有类。

#### 5.2.1 “类”函数

模仿类利用了函数的一个特殊性质，所有的函数都会默认拥有一个名为prototype的公有但不可枚举的属性。

当使用new运算符创建一个对象时，就将那个对象的[[prototype]]链接到了这个函数的prototype指向的对象上。

#### 5.2.2 “构造函数”
看下面的一段代码：
```
function Foo(){
	//....
}
Foo.prototype.constructor === Foo // true

var a = new Foo();
a.constructor === Foo; // true
```

Foo.prototype默认有一个公有且不可枚举的属性`.constructor`,这个属性引用的是对象关联的函数。同时，我们看到使用“构造函数”创建的对象也有一个.constructor属性，指向“创建这个对象的函数”。

##### 构造函数还是调用
new会劫持所有普通函数并用构造对象的形式调用它。

javascript中对“构造函数”最准确的解释是，所有带new的函数调用。

函数不是构造函数，但是当且仅当使用new时，函数调用会变成“构造函数调用”。

#### 5.2.3 技术
constructor属性是一个非常不可靠和不安全的引用，所以要尽量避免使用这个引用。

### 5.3 （原型）继承
##### instanceof函数的用法
`a instanceof Foo`  
instanceof操作符的左操作数是一个普通的对象，右操作数是一个函数，instanceof回答的问题是：在a的整条[[Prototype]]链中是否有指向Foo.prototype的对象。

### 5.4 对象关联

现在我们知道了，[[Prototype]]机制就是存在于对象中的一个内部链接，它会引用其他对象。

#### 5.4.1 创建关联
最好使用`object.create()`来创建一个新对象，比起new函数，它会避免一些不必要的麻烦。

# 第六章 行为委托

### 6.1 面向委托的设计
