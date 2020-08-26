[toc]

## 构造函数

构造函数的作用是创建一个自定义的类及其实例。实例与实例之间是相互独立的。构造函数就是一个普通的函数，只是调用其需要``new``关键字。

```javascript
function Person(name, age, gender) {
  this.name = name
  this.age = age
  this.gender = gender
  this.sayName = function () {
    alert(this.name);
  }
}
var per = new Person("孙悟空", 18, "男");//构造函数创建一个实例per
function Dog(name, age, gender) {
  this.name = name
  this.age = age
  this.gender = gender
}
var dog = new Dog("旺财", 4, "雄")
console.log(per);//当我们直接在页面中打印一个对象时，事件上是输出的对象的toString()方法的返回值
console.log(dog);
```

​	上面Person构造函数每创建一个Person对象，都会创建一个sayName的方法，那么可以把共有的方法单独放到一个地方，并让所有的实例都可以访问到呢?这就需要原型(`prototype`)。

## 原型

在JavaScript中，每当定义一个函数数据类型(普通函数、类)时候，都会天生自带一个`prototype`属性，这个属性指向函数的原型对象，并且这个属性是一个对象数据类型的值。

<img src="https://img2018.cnblogs.com/blog/850375/201907/850375-20190708151024134-512558007.png"/>

上图表示的就是Person的构造函数会自带一个prototype属性，指向Person.prototype这个原型对象。（这个原型也是一个对象）

原型对象就相当于一个公共的区域，所有同一个类的实例都可以访问到这个原型对象，我们可以将对象中共有的内容，统一设置到原型对象中。

## 原型链

### \_\_proto__和constructor

每一个对象数据类型(普通的对象、实例、`prototype`......)也天生自带一个属性`__proto__`，属性值是当前实例所属类的原型(`prototype`)。原型对象中有一个属性`constructor`, 它指向函数对象。

```javascript
function Person() {}
var person = new Person()
console.log(person.__proto__ === Person.prototype)//true
console.log(Person.prototype.constructor===Person)//true
//顺便学习一个ES5的方法,可以获得对象的原型
console.log(Object.getPrototypeOf(person) === Person.prototype) // true
```

<img src="https://img2018.cnblogs.com/blog/850375/201907/850375-20190708151615691-1017611190.png"/>

### 何为原型链

**在JavaScript中万物都是对象，对象和对象之间也有关系，并不是孤立存在的。对象之间的继承关系，在JavaScript中是通过prototype对象指向父类对象，直到指向Object对象为止，这样就形成了一个原型指向的链条，专业术语称之为原型链**。

举例说明:person → Person → Object   ，普通人继承人类，人类继承对象类

**当我们访问对象的一个属性或方法时，它会先在对象自身中寻找，如果有则直接使用，如果没有则会去原型对象中寻找，如果找到则直接使用。如果没有则去原型的原型中寻找,直到找到Object对象的原型，Object对象的原型没有原型，如果在Object原型中依然没有找到，则返回undefined。**

我们可以使用对象的`hasOwnProperty()`来检查对象自身中是否含有该属性；使用`in`检查对象中是否含有某个属性时，如果对象中没有但是原型中有，也会返回true。

```javascript
function Person() {}
Person.prototype.a = 123;
Person.prototype.sayHello = function () {
  alert("hello");
};
var person = new Person()
console.log(person.a)//123
console.log(person.hasOwnProperty('a'));//false
console.log('a'in person)//true
```

person实例中没有a这个属性，从 person 对象中找不到 a 属性就会从 person 的原型也就是 `person.__proto__` ，也就是 Person.prototype中查找，很幸运地得到a的值为123。那假如 `person.__proto__`中也没有该属性，又该如何查找？

当读取实例的属性时，如果找不到，就会查找与对象关联的原型中的属性，如果还查不到，就去找原型的原型，一直找到最顶层Object为止。**Object是JS中所有对象数据类型的基类(最顶层的类)在Object.prototype上没有`__proto__`这个属性。**

```javascript
console.log(Object.prototype.__proto__ === null) // true
```

<img src="https://img2018.cnblogs.com/blog/850375/201907/850375-20190708153139577-2105652554.png"/>

图中由相互关联的原型组成的链状结构就是原型链，也就是蓝色的这条线。