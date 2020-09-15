### 1.面向对象编程

#### 6.1什么是面向对象编程

Java ,JavaScript,C#...面向对象；JavaScript有些区别！

- 类：模板
- 对象：具体的实例

在JavaScript这个需要大家换一下思考

### 定义class与继承：

> class继承
>
> **class继承是ES6引入的。**

以前：



```javascript
      function Student(name) {
            this.name=name;
      }

      //给Student新添加一个方法
    Student.prototype.hello=function () {
          alert('你好')
    };
```

ES6之后:

#### 1.定义一个类，属性，方法

```JavaScript
    //ES之后========
    //定义一个学生类
     class Student{
         //构造方法
         constructor(name) {
             this.name=name;
         }

         //定义一个方法
         helle(){
             alert('你好！')
         }


     }

     var xiaoming =new Student("小明");
    var xiaohong =new Student("小红");

xiaoming.name
"小明"
xiaoming.helle()
undefined
xiaohong.name
"小红"
xiaohong.helle()
```

#### 2.继承

```JavaScript
    //ES之后========
    //定义一个学生类
    class Student{
        //构造方法
        constructor(name) {
            this.name=name;
        }

        //定义一个方法
        helle(){
            alert('你好！')
        }


    }

    class xiaoStdent extends  Student{
        //构造方法参数是名字和年级
        constructor(name,grade) {
            super(name);
            this.grade=grade;
        }

        Mygrade(){
            alert(this.name+'是小学生');
        }

    }

    var xiaoming =new Student("小明");
    var xiaohong =new Student("小红");
     var xiaoxing=new xiaoStdent("小星",1);

```

> 本质原型对象





> 原型链



一、prototype

在JavaScript中，每个函数都有一个prototype属性，这个属性指向函数的原型对象。

二、__proto__

这是每个对象(除null外)都会有的属性，叫做__proto__，这个属性会指向该对象的原型。

关系图：

![850375-20190708151322530-1608157973](javascript面向对象编程2.assets/850375-20190708151322530-1608157973.png)

补充说明：

绝大部分浏览器都支持这个非标准的方法访问原型，然而它并不存在于 Person.prototype 中，实际上，它是来自于  Object.prototype ，与其说是一个属性，不如说是一个 getter/setter，当使用 obj.__proto__  时，可以理解成返回了 Object.getPrototypeOf(obj)。

三、constructor

每个原型都有一个constructor属性，指向该关联的构造函数。

```javascript


function Person() {

}
console.log(Person===Person.prototype.constructor)  //true


```

![850375-20190708151615691-1017611190](javascript面向对象编程2.assets/850375-20190708151615691-1017611190.png)

```JavaScript
function Person() {

}

var person = new Person();

console.log(person.__proto__ == Person.prototype) // true
console.log(Person.prototype.constructor == Person) // true
// 顺便学习一个ES5的方法,可以获得对象的原型
console.log(Object.getPrototypeOf(person) === Person.prototype) // true
```

 补充说明： 

```javascript


function Person() {

}
var person = new Person();
console.log(person.constructor === Person); // true


```

 当获取 person.constructor 时，其实 person 中并没有 constructor 属性,当不能读取到constructor 属性时，会从 person 的原型也就是 Person.prototype 中读取，正好原型中有该属性，所以： 

```
person.constructor === Person.prototype.constructor
```

 **实例与原型** 

 当读取实例的属性时，如果找不到，就会查找与对象关联的原型中的属性，如果还查不到，就去找原型的原型，一直找到最顶层为止。 

```JavaScript
function Person() {

}

Person.prototype.name = 'Kevin';

var person = new Person();

person.name = 'Daisy';
console.log(person.name) // Daisy

delete person.name;
console.log(person.name) // Kevin
```

 **原型链** 

 简单的回顾一下构造函数、原型和实例的关系：每个构造函数都有一个原型对象，原型对象都包含一个指向构造函数的指针，而实例都包含一个指向原型对象的内部指针。那么假如我们让原型对象等于另一个类型的实例，结果会怎样？显然，此时的原型对象将包含一个指向另一个原型的指针，相应地，另一个原型中也包含着一个指向另一个构造函数的指针。假如另一个原型又是另一个类型的实例，那么上述关系依然成立。如此层层递进，就构成了实例与原型的链条。这就是所谓的原型链的基本概念。——摘自《javascript高级程序设计》

其实简单来说，就是上述四-五的过程。