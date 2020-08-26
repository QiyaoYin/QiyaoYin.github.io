# 类型

​	JS变量有两种数据类型：基本类型和引用类型（也有其他叫法：原始类型和对象类型，拥有方法的类型和不能拥有方法的类型，可变类型和不可变类型）

## 基本类型

​	基本数据类型有6种：Nndefined、Null、Boolean、Number、String，ES6引入了第6种基本类型 Symbol，说是独一无二的，两个Symbol用``===``比较返回false。一个引用类型Object。

​	目前，null和undefined基本是同义的，只有一些细微的差别。**null表示"没有对象"，即该处不应该有值。**典型用法是：

（1） 作为函数的参数，表示该函数的参数不是对象。

（2） 作为对象原型链的终点。

**undefined表示"缺少值"，就是此处应该有一个值，但是还没有定义。**典型用法是：

（1）变量被声明了，但没有赋值时，就等于undefined。

（2) 调用函数时，应该提供的参数没有提供，该参数等于undefined。

（3）对象没有赋值的属性，该属性的值为undefined。

（4）函数没有返回值时，默认返回undefined。

```javascript
var i;
i // undefined

function f(x){console.log(x)}
f() // undefined

var  o = new Object();
o.p // undefined

var x = f();
x // undefined
```

基本数据类型是按值访问：

1. 基本数据类型值不可变

```javascript
let a = '11aa';
a.toUpperCase();//11AA
console.log(a);//11aa
```

2. 基本类型的比较是值的比较

```javascript
let a = 1;
let b = true;
console.log(a == b);//true
console.log(a === b);//false
```

3. 基本数据类型的变量是放在栈里的

```javascript
let a = 'yqy';
b = a;
a = 'hehe';
console.log(a);//hehe
console.log(b);//yqy
```



<img src="https://segmentfault.com/img/bVCunf"/>

## 引用类型

​	除过上面的 6 种基本数据类型外，剩下的就是引用类型了，统称为 <code>Object 类型</code>。细分的话，有：<code>Object 类型</code>、<code>Array 类型</code>、<code>Date 类型</code>、<code>RegExp 类型</code>、<code>Function 类型</code> 等。

<strong>引用类型的值是按引用访问的。</strong>

1. 引用类型的值是可变的：

```javascript
let obj = {lastname:'yqy'};
obj.lastname = 'hehe';
obj.firstname = 'yqy';
obj.fullname = ()=>{
  return `${this.lastname}${this.firstname}`;
}
```

2. 引用类型的比较是引用的比较

```javascript
let obj1 = {}
let obj2 = {}
console.log(obj1 == obj2);//false
console.log(obj1 === obj2);//false
```

因为 obj1 和 obj2 分别引用的是存放在堆内存中的2个不同的对象，故变量 obj1 和 obj2 的值（引用地址）也是不一样的！

引用类型的值是保存在堆内存（Heap）中的对象（Object）。 与其他编程语言不同，JavaScript 不能直接操作对象的内存空间（堆内存）。

```javascript
var a = {name: "percy"};
var b;
b = a;
a.name = "zyj";
console.log(b.name);// zyj
b.age = 22;
console.log(a.age);// 22
var c = {
  name: "zyj",
  age: 22
};
```

图解如下：

+ 栈内存中保存了变量标识符和指向堆内存中该对象的指针
+ 堆内存中保存了对象的内容

<img src='https://segmentfault.com/img/bVCuGx'/>

## 检测类型

### typeof

​	经常用来检测一个变量是不是最基本的数据类型。

```javascript
typeof a;//undefined

let a = null;
typeof a;//object

a = '123';
typeof a;//String

a = true;
typeof a;//Boolean

a = 123;
typeof a;//Number

a = {}
typeof a;//Object

a = []
typeof a;//Object

a = /aaa/g;
typeof a;//Object
```



### instanceof

​	用来判断某个构造函数的 prototype 属性所指向的对象是否存在于另外一个要检测对象的原型链上。

+ 简单说就是判断一个引用类型的变量具体是不是某种类型的对象

```javascript
({}) instanceof Object //true
([]) instanceof Array//true
(/aa/g) instanceof RegExp//true
(function(){}) instanceof Function//true
```

