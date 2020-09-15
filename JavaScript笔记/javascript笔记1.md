### 1.什么是JavaScript？

JavaScript是世界上最流行的一门脚本语言

JavaScript （十天开发出来）--

### 一个合格的后端人员，必须要精通JavaScript

#### 1.2历史

 https://blog.csdn.net/kese7952/article/details/79357868 

**ECMAScript**它可以理解为JavaScript的一个标准

目前（2020/3/25）最新版已经到了ES6

但是大部分浏览器还只停留在支持es5代码上！

开发环境----线上环境，版本不一致

### 2.JavaScript入门

#### 2.1引入JavaScript

1.内部标签

```javascript
<stcript>
    //js代码
<stcript>
```

2.外部引入

abc.js文件

```
//.......
```

test.html

```javascript
 <script src="js/abc.js"></script>
```

测试代码：

```JavaScript
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>

<!--    script标签内，写JavaScript代码-->

<!--    <script>-->
<!--        alert("你好JavaScript");-->
<!--    </script>-->

<!--    使用方式二，外部引入-->
<!--   注意：script标签必须成对出现 这样写（ <script src="js/qj.js"/>）会出问题-->
    <script src="js/qj.js"></script>

<!--    不用显示定义type，也默认就是JavaScript-->
    <script type="text/javascript">

    </script>

</head>
<body>

<!--也可以在这里存放-->
</body>
</html>
```

**注意：**

> 注意：script标签必须成对出现 这样写（ <script src="js/qj.js"/>）会出问题

```
//console.log(score) 在浏览器的控制台打印变量！System.out.println();
```

### 2.3数据类型

数值，文本，图形，音频，视频......

#### 变量：

```
var a=1
```

打印变量：

```
console.log(a)
>>1
```

#### **number:**

js不区分小数和整数,Number

```JavaScript
123//整数123
123.1//浮点数123.1
1.123e3//科学计数法
-99 //复数
NaN //not a number
Infinity //表示无限大
```

#### 字符串

‘abc’ “abc”

#### 布尔值：

true    false

#### 逻辑运算

```
&& 两个为真，结果为真
|| 一个为真结果为真
! 真为假   假为真
```

#### 比较运算符（重要）

```
= 赋值运算符
== 等于（类型不一样，值一样，也会判断true）
=== 绝对等于（类型一样，值一样，结果true）

```

 这是JavaScript的缺陷，坚持不要使用==比较

须知：

- NaN===NaN  false   NaN跟所有数值都不相等，包括自己
- 只能通过isNaN（NaN）来判断这个数是否相等NaN

#### 浮点数问题

```
console.log((1/3)===(1-2/3))
```

尽量避免使用浮点数进行运算，存在精度问题

```
Math.abs(1/3-(1-2/3))<0.00000001
```

#### 数组：

Java中的数组必须是相同类型的对象~，**js中不需要这样比如**：

```javascript
//保证代码可读性，尽量使用[]
 var arr=[1,2,3,4,'abc',null,true]
 new Array("fdfd",1,2,45,47,43)
```

 **打印数组下标方法：**console.log(arr[4]) 

如果取数组下标，越界了，就会报： **undefined** 未定义的意思

#### 对象

对象是大括号，数组是中括号~~

> 每个属性之间用逗号隔开，最后一个不需要添加

```javascript
        //Java定义对象：Perpson person=new Person(1,2,3,5,6);
          var person={
            name:"jinronga",
            age:3,
            tags:['js','java','web']
        }
```

取对象的属性值：

```
person.name
>>"jinronga"
person.age
>>3
person.tags
>>Array(3) [ "js", "java", "web" ]
```

#### 2.4严格检查模式

 'use strict'; 

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>

<!--
    前提：IDA 需要设置支持ES6语法
  'use strict';  严格检查模式，预防JavaScript的随意性导致产生的问题
  （必须写在JavaScript的第一行）
   局部变量建议都使用let 去定义~
-->
    <script>
     'use strict';
        //全局变量
      let i=1;
    //ES6  let
    </script>
</head>
<body>

</body>
</html>
```



### 3.数据类型

#### **3.1字符串：**

1.正常字符串我们使用单引号 ' ' 或者双引号 " "包裹起来

2.注意转义\

```
\`
\n
\t
\u4e2d   \u####  Unicode字符
\x41        Ascll字符
```

3.多行字符串编写

**多行字符串  使用``包裹起来  Tab上面 Esc下面**

```
      //多行字符串  使用``包裹起来  Tab上面 Esc下面
        var msg=`
          你好
          你是谁
          我是Java小菜鸡
          哦！
          回去等通知
           `;
```

4.模板字符串

```javascript
 let name="金融啊";

  let msg1=`"你好!",${name}`;  //使用`` Tab上面的包裹起来
```

5.字符串长度

```
str.length
console.log(msg1.length)
```

6.字符串的可变性，不可变

JavaScript的字符串也是不可变的

7.大小写转换

```
//注意这里是方法不是属性
txt.toUpperCase()//把字符串转为大写
txt.toLocaleLowerCase()//把字符串转为小写
```

8.获取指定元素的下标：

```
txt.indexOf('t')
```

9.截取第几个到第几个元素

subsring（）

```
txt.substring(1)//从第一个字符串截取到最后一个
txt.substring(1,4)//从第一个字符串截取到第四个字符串
```

#### 3.2数组

**Array可以包含任意数据类型的数据**

```JavaScript
var  arr=[1,5,4,74,null,"egegeggg","哦"];//通过下标取值和赋值
arr[0]
arr[0]=1
```

1.长度

```JavaScript
arr.length
```

**注意：**假如给arr.length赋值，数组大小就会发生变化~（arr.length=10:数组长度就是10了），如果赋值变小元素丢失！

字符串"1"与数字1是不同的

3.**slice()** 截取Array的一部分，返回一个新的数组，类似与string中subsring

4.push(),pop() 尾部 很像栈出入（stack）先进后出，后进先出

```JavaScript
push:压入到尾部 --追加元素到尾部
pop:弹出尾部的一个元素
```

5.unshift(),shift()头部

```javascript
unshift()：压入到头部--往头部追加元素
shift():弹出头部第一个元素
```

6.排序sort()

```
let arrar=['C','D','A','B','K']

 arrar.sort();//排序
 
 Array(5) [ "A", "B", "C", "D", "K" ]
```

7.元素反转reverse()

```
[ "A", "B", "C", "D", "K" ]
arrar.reverse();//反转
[ "K", "D", "C", "B", "A" ]
```

8.concat()

```
arrar.concat(1,1,2,1,4)
[ "K", "D", "C", "B", "A", 1, 1, 2, 1, 4 ]
arrar
[ "K", "D", "C", "B", "A" ]
```

注意：concat()并没有修改数组，只会返回一个新的数组

9.连接符 join

打印拼接数组，使用特定的字符串连接

```
[ "K", "D", "C", "B", "A" ]
arrar.join('*')
"K*D*C*B*A"
```

10.多维数组

```
arrar1=[[1,2],[3,4],[4,8]]
arrar1=[1][1]
4
```

 

**数组：存储数据（如何存，如何取，方法都可以自己实现！）**

### 3.3对象

若干个键值对

```javascript
var 对象名={
   属性名：属性值,
   属性名：属性值,
   属性名：属性值
}

        //对象
        var person={
            name:'金融啊',
            age:20,
            email:'1460595002@qq.com',
            score:80

     }
```

js对象中，{......}表示一个对象，键值对描述属性xxx:xxx，多个属性逗号隔开，最后一个属性不加逗号！1.

**javascript中的键是字符串，值是任意的对象！**

1.对象赋值

```javascript
person.name="张三"
"张三"
person.name
"张三"
```

2.使用一个不存在的对象属性，不会报错！undefined

```javascript
person.agege
undefined
```

3.动态的删减属性，通过delete删除对象的属性

```javascript
delete person.name
true
person
{ age: 20, email: "1460595002@qq.com", score: 80 }
```

4.动态添加，直接给新的属性添加值即可

```javascript
person.haha="haha"
"haha"
person
{ age: 20, email: "1460595002@qq.com", score: 80, haha: "haha" }
```

5.判断属性值是否在这个对象中！ xxx in xxx

```javascript
'age' in person //键一定要用引号包裹因为键是字符串
true
//继承
'toString' in person
true
```

6.判断属性是否是这个对象自身拥有的hasOwnProperty()

```javascript
person.hasOwnProperty('toString')
false

person.hasOwnProperty('age')
true
```

### 3.4流程控制

if判断

```javascript
        var score=90;

        // 2.条件控制
        if(score>=80){ //第一个判断
            alert("成绩优秀");
        }else if(score>=70){//第二个判断
            alert("成绩及格");
        }else { //否则
            alert("不及格")
        }
```

while循环，避免程序死循环

```javascript
     var age=1;
     while(age<100){
         age+=1;
            console.log(age);
     }


    do{
        age+=1;
            console.log(age);
    }while(age<100)
    
```

for循环

```
    for (let j = 0; j <100 ; j++) {
            console.log(j);

     }
```

遍历数组：

```javascript
     var arr=new Array('df',null,12,56,"你好啊");
     //遍历数组
     for (let j = 0; j < arr.length; j++) {
         console.log(arr[j]);

     }
```

forEach循环：5.1引入

```javascript
       var age=[1,5,4,4,558,8,8888888,545,45];

          age.forEach(function (value) {
                 console.log(value)
          })
```

for...in..

```
          index:索引    age:数组 
     //for(let index in object){}
     var age=[1,5,4,4,558,8,8888888,545,45];
     for(let num in age){
            console.log("存在的");
           console.log(age[num])

        }
```

###  3.5Map和Set

> ES6的新特性~

Map：

```javascript
        //ES6 Map
        //学生的姓名，学生的名字
        //  var names=['tom','jack,','nnn'];
        //  var scores[100,80,80];

var map=new Map([['tom',100],['jack',90],['hhh',90]]);

console.log( map.get('tom')); //通过key获取var

  map.set('ggg',89); //往map后面追加值或者修改
  map.delete('tom');//删除
```

Set：无序不重复的集合

```
set.delete(1);//删除！
set.add(10);//添加！
console.log(set.has(3));//集合是否包含某个元素！
```

### 3.6 iterator

作业：使用iteratos来遍历迭代Map，Set！

**for  of 遍历数组所有的元素 ，for in遍历数组的下标**

遍历数组：

```javascript
    let array=[15,45,579,798,486];

    //通过for of  遍历数组中每个元素    for in遍历数组的下标
     for (let num of array){
          console.log(num);
       }
```

遍历Map

```javascript
      var map=new Map([["tom",100],["jack",90],["hhhaha",80]]);
        //for of遍历
        for (let x of map){

            console.log(x);
        }
```

 

遍历Set

```javascript
      var set=new Set([1,4,7,58,87,42,3]);

        for (let x of set){
            console.log(x)

        }
```

### 4.函数

方法：对象（属性，方法）

函数：

#### 4.1定义函数

> 方式一：

```javascript
        
        function f(x) {
            if (x>=0){
                return x;
            }else {
                return -x;
            }

        }
```

一旦执行return代表函数结束，返回结果！

如果没有执行return，函数执行也会返回结果，结果就是undefined

> 定义方式二：

```javascript
     var abs =function(x){

         if (x>=0){
                return x;
            }else {
                return -x;
            }
        }
```

function(x){.....}这是一个一个匿名函数，但是可以把结果赋值给abs，通过abs就可以调用韩式！

方式一和方式二等价！

> 调用函数

```
abs(10)//10
abs(-10)//-10
```

参数问题：javascript可以传任意个参数，也可以不传参数~

参数是否存在的问题？

假设进来是否存在的问题？

假设不存在参数，如何规避？抛异常

```
        var abs =function(x){

            if ( typeof x!= 'number') {
                throw '不是一个数字';
            }
            if(x=>0){
                
                return x;
            }else {
                return -x;
            }
        }
```

> **arguments**

arguments是js免费赠送的关键字；代表，传递进来的所有的参数，是一个数组！通过它可以获取所有获取参数

```javascript
        var abs =function(x){

            console.log("x="+x);
            for (let i = 0; i <arguments.length ; i++) {
                console.log(arguments[i]);

            }


            if(x=>0){

                return x;
            }else {
                return -x;
            }
        }
```

问题：arguments包含所有的参数，我们有时候使用多余的参数来进行附加操作。需要排除已有参数~

> rest

以前：

```javascript

     if (arguments.length>2){
              for (let i=2;i<arguments.length;i++){
                  console.log(arguments[i]);
              }
          }
```

> ES6:

ES6引入的新特性，获取除了已经定义的参数之外的所有参数~。。。

```javascript
      function a(a,b,c,...rest) {
          console.log("a="+a);
          console.log("b"+b);
          console.log("rest"+rest);

      }
```

rest参数只能写在最后面，必须用...标识。

#### 4.2变量的作用域

在javascript中，var定义实际变量是有作用域的。

在函数体中定义，则在函数体外不可以使用~（想实现函数体外使用后面要研究闭包）

```javascript
        function f() {
           var x=1;
           x=x+1;
        }
        x=x+2; //ReferenceError: x is not defined
```

```

```

如果两个函数定义了相同名字的变量名，在函数内部不会冲突（局部变量）

```javascript
       function f() {
            var x=1;
            x=x+1;
       }
       function f1() {
            var x='A';
            x=x+1;
       }
```

内部函数可以访问外部函数的成员，反之则不行

```javascript
      function f() {
         var x=1;
         function f1() {
              var z=x+2;//3

         }
var b=z+1;//Unacught ReferenceError: b is not defined

      }
```

假设，内部函数变量和外部函数的变量重名！

```javascript

      function f() {
         var x=1;

         function f1() {
             var x=2;
             console.log('内部'+x)//内部2

         }

         console.log('外部'+x);//外部1

          f1();

      }
       f();
```

假设javascript中函数查找变量从内往外查找自身函数开始~，由“内”向”外“查找，假设外部存在这个同名的函数变量，则内部函数会屏蔽外部函数的变量。

> 提升变量的作用域

```javascript
       function f() {
          var x='x'+y;
          console.log(x);
          var y='y';
       }
```

结果： xundefined 

说明；js执行引擎，自动提升了y的声明，但是不会提升变量y的赋值；

```javascript
       function f() {
           var y;
          var x='x'+y;
          console.log(x);
            y='y';
       }
```

这个是javascript建立之初就存在的特性。养成规范：所有的变量定义都放在函数的头部不要乱放，便于代码的维护；

```javascript
       function f() {
           var x=1;
           y=x+1;
           z,i,a;//undefined

           //之后随意用

       }
```

> 全局函数

```javascript
        //全局变量
    var x=1;
      function f() {
        console.log(x)
        
     }
        f();
        console.log(x)
```

> 全局对象window

```javascript
   var x='xxx';
      alert(x);
      alert(window.x); //默认所有的全局对象都是默认window的
```

alert本事是一个window对象

```javascript
       var x =1111;
       window.alert(x);

       var old_alert=window.alert;

       window.alert=function () {

       }
       //发现alert失效了
       window.alert(123)
       //恢复
      window.alert=old_alert;
      window.alert(456);
```

javascript实际上只有一个全局作用域，任何变量（函数也可以视为一个变量）假设没有在函数作用范围内，就会向外查找，如果在全局作用域都没有找到，就会报错RefrenceError

> 规范

由于我们的所有的全局变量都会绑定到window上。如果不同的js文件，使用了相同的全局变量如何减少冲突？

```
       //唯一的全局变量
        var jinrongaPP={};

        //定义全局变量
        jinrongaPP.name='jinrogna';

        jinrongaPP.add=function (a,d) {

             return a+d;
        }

```

把自己的代码全部放入自己定义的唯一空间名字中，降低全局命名冲突的问题~

jquery

> 局部作用域let

```javascript
       var f=function () {
     for (var i = 0; i <100 ; i++) {

           console.log(i);

       }
         console.log(i+1);//101  问题： i出了作用域还能使用
       }
```

**ES6关键字，解决局部作用域冲突的问题！**

```
      var f=function () {


       for (let i = 0; i <100 ; i++) {

           console.log(i);

       }
         console.log(i+1);//ReferenceError: i is not defined
      }
```

建议使用let去定义局部作用定义作用域变量；

> 常量const

在ES6之前，怎么定义常量的：只要用全部大写命名的变量就是常量，建议不要修改的值

```javascript
     var PI=3.14;
      console.log(PI);//3.14
      PI=3.15;
      console.log(PI);//3.15 可以被改变
```

**在ES6引入了常量的关键字const**

```javascript
  const PI=3.14; //只读变量不能被改变
      console.log(PI);//3.14
      PI=3.15; //报错  TypeError: invalid assignment to const `PI'
```

### 4.3方法

> 定义方法

方法就是把函数放在对象里面，对象只有两个东西：**属性和方法**

```javascript
      //方法：
        var fa={

            name:'jinronga',
            bren: 2000,
            age : function () {
                //当前的日期
             var year=   new Date().getFullYear();

             return year-this.bren; //年龄
            }

        }
        //属性调用
        fa.name
        //方法调用
        fa.age()
```

this代表什么？拆开上面的代码看看~

```javascript
   var getAge=function () {
       //当前的日期
       var year=   new Date().getFullYear();

       return year-this.bren; //年龄


   }
      //方法：
        var fa={

            name:'jinronga',
            bren: 2000,
            age : getAge()

        }
        
        //fa.age() ok
        //getAge() NaN  window
```

我们 知道this是无法指向的，是默认调用它的那个对象；

> apply

在javascript中可以控制this指向！

```javascript

   var getAge=function () {
       //当前的日期
       var year=   new Date().getFullYear();

       return year-this.bren; //年龄


   }
      //方法：
        var fa={

            name:'jinronga',
            bren: 2000,
            age : getAge()

        }

       // fa.age(); ok
    getAge().apply(fa,[]);//this执行了fa，参数为空
```

### 5.内部对象

> 标准对象

```javascript
typeof 123
"number"
typeof '1212'
"string"
typeof Date
"function"
typeof NaN
"number"
typeof []
"object"
typeof {}
"object"
typeof Math.abs
"function"
typeof undefined
"undefined"
```

#### 5.1 :Date基本使用

```javascript
       var now=new Date();  //"Thu Mar 26 2020 22:43:28 GMT+0800 (中国标准时间)"
         now.getFullYear();//年
          now.getMonth();//月  0~11代表月
          now.getDate();//日
           now.getDay();//星期几
           now.getHours();//时
           now.getMinutes();//分
           now.getSeconds();//秒

          now.getTime();//时间戳  全时间统一 1970 1.1 0:00:00 毫秒数
               console.log(new Date(1585233788063));//时间戳转换为时间格式
       

```

转换

```
new Date(1585233788063)
Date Thu Mar 26 2020 22:43:08 GMT+0800 (中国标准时间)
now.toLocaleString()//注意，调用是一个方法，不是一个属性
"2020/3/26 下午10:43:08"
now.toLocaleDateString()
"2020/3/26"
now.toGMTString()
"Thu, 26 Mar 2020 14:43:08 GMT"
```

