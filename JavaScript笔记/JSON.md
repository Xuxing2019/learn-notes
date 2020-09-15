### 1.json对象

> json是什么？

JSON：JavaScript 对象表示法（JavaScript Object Notation）。

JSON是 (JavaScript Object Notation, JS 对象标记)，它是一种数据交换格式。在JSON出现之前，大家一直用XML来传递数据。因为XML是一种纯文本格式，所以它适合在网络上交换数据。XML本身不算复杂，但是，加上DTD、XSD、XPath、XSLT等一大堆复杂的规范以后，任何正常的软件开发人员碰到XML都会感觉头大了，最后大家发现，即使你努力钻研几个月，也未必搞得清楚XML的规范。

终于，在2002年的一天，道格拉斯·克罗克福特（DouglasCrockford）同学为了拯救深陷水深火热同时又被某几个巨型软件企业长期愚弄的软件工程师，发明了JSON这种超轻量级的数据交换格式。

由于JSON非常简单，很快就风靡Web世界，并且成为ECMA标准。几乎所有编程语言都有解析JSON的库，而在JavaScript中，我们可以直接使用JSON，因为JavaScript内置了JSON的解析。把任何JavaScript对象变成JSON，就是把这个对象序列化成一个JSON格式的字符串，这样才能够通过网络传递给其他计算机。如果我们收到一个JSON格式的字符串，只需要把它反序列化成一个JavaScript对象，就可以在JavaScript中直接使用这个对象了。

##### 格式：

在JavaScript中一切皆为

- 对象都用{}
- 数组都用[]
- 所有的键值对都是用 key:values

其格式为{“key1”:value1,”key2”,value2….};key 必须是字符串。很像map对不对，一个key,一个value。
因为ajax请求不刷新页面，但配合js可以实现局部刷新，因此json常常被用来作为异步请求的返回对象使用。

#### json对象：

```JavaScript
    //这是一个json对象
    var  gareen={"name":"瞎子","hp":616};
    console.log(gareen);

```

#### 访问json对象（json对象名.key值）

```JavaScript
    var  gareen={"name":"瞎子","hp":616};
    // console.log(gareen);
    //对象名.key
    console.log(gareen.name);
    console.log(gareen.hp);
``` 
#### 将js对象转换json对象
```javascript
var user={
            name:"金融啊",
            age:3,
            gender:"男"
        }
        //将js对象转换为json对象
        var str=JSON.stringify(user);
        console.log(str);
```
#### 将json转换为js对象
```javascript
        //将json转换为js对象
        var user2=JSON.parse(str);
        console.log(user2.name,user2.age,user2.gender)
```

#### json对象转换为字符串
```javascript
   //这是一个json对象
    var  gareen={"name":"瞎子","hp":616};
    console.log(gareen);
   //json转化为字符串JSON.stringify()
console.log(JSON.stringify(gareen))
```

#### 字符串转为json对象

```javascript
       //字符串转换为json使用JSON.parse()
    var obj=JSON.parse('{"name":"瞎子","hp":616,"age":3,"gender":"男"}');
```





#### json和js对象的区别

```JavaScript
var json='{"name":"瞎子","hp":616,"age":3,"gender":"男"}'--json
var obj={name:"瞎子",hp:616,age:3,gender:"男"}-- js
```

### 5.3 Ajax对象：

原生js写法 xhr异步请求

jQuery封装好的方法$("#name").ajax("")

axios请求

