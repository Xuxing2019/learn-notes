### 1.操作DOM对象（重点）

DOM：文档对象模型

浏览器网页就是Dom树形结构!

- **更新：**更新Dom节点
- **遍历dom节点：**得到dom节点
- **删除：**删除一个Dom节点
- **添加：**添加一个新的节点

#### 获取节点

要操作一个Dom节点，就必须获得这个Dom节点

> 获取Dom节点

```JavaScript
    //对应css选择器
    var h1=document.getElementsByTagName('h1');//根据标签名获取节点
    var p1=document.getElementById('p1');//根据id获取节点
    var p2=document.getElementsByClassName('p2');//根据类名获取节点
    var father=document.getElementById('father');//根据id获取节点
    var childrens=  father.children[index];//获取父节点下的所有的子节点

      // father.firstChild;//获取第一个节点
        //father.lastChild;//获取最后一个节点
```

这是原生代码之后我们尽量使用jQuery

#### 更新节点

- id1.innerText='1212'  修改文本的值，id1是某个标签的值 
-  id1.innerHTML='<strong/>123</strong>' 可以解析HTML文本标签

操作css

```JavaScript
id1.style.color='blue' --id1代表标签的id   属性使用字符串包裹起来
id1.style.fontSize='200px' 
id1.style.padding='2em'
```



### 删除节点

删除节点的步骤：先获取父节点，在通过父节点删除自己

```HTML
<div id="father">
<h1>标题一</h1>
<p id="p1">p1</p>
<p class="p2">p2</p>
</div>
<script>
  var self=document.getElementById('p1');
    var father=p1.parentElement //获取id标签的父节点
   father.removeChild(self) //通过父节点删除p1
    
    
    //删除是一个动态的过程；
father.removeChild(father.children[0])
father.removeChild(father.children[1])
father.removeChild(father.children[2])
    
</script>

```

注意:删除多个节点的时候，children是在时刻变化的，删除节点的时候一定要注意：

#### 插入节点

我们获取Dom节点，假设这个dom节点是空的，我们通过innerHTML就可以添加一个元素，但是这个DOM节点已经存在元素，我们就不能怎么干了！会产生覆盖！所有使用追加

追加

> list.appendChild(js)

```html
    <p id="js">
        javascript
    </p>

  <div id="list">
      <p id="se">JavaSE</p>
      <p id="ee">javaee</p>
      <p id="me">javame</p>
  </div>
 <script>
     var js=document.getElementById('js');
     var list=document.getElementById('list');

list.appendChild(js)
 </script>

```

![QQ图片20200327224225](javascript操作DOM对象(对象)4.assets/QQ图片20200327224225.png)

> 创建一个新的标签

```HTML
 <script>
     var js=document.getElementById('js');//已存在的节点
     var list=document.getElementById('list');

     //通过JS创建一个新的节点
     var newP=document.createElement('p');//创建一个新的节点
       newP.id='pd'; //新节点的id
      newP.innerText='新的节点' //添加新节点的内容

     list.appendChild(newP);//追加到list标签中
     
         //创建一个标签节点（通过这个属性，可以设置任意的）
     var myScript=document.createElement('script');
       myScript.setAttribute('type','text/javascript');
       
            //创建一个style标签
         var Mystyle=document.createElement('style');
             Mystyle.setAttribute('type','text/css');
            Mystyle.innerHTML='body{background-color:chartreuse;}';//设置标签的内容

         document.getElementsByTagName('head')[0].appendChild(Mystyle)

 </script>
```

> ```
> insertBefore
> ```

 

```html
 <script>
     var js=document.getElementById('js');//已存在的节点
     var list=document.getElementById('list');
     var ee=document.getElementById('ee');
      //要包含的节点.insertBefore(新的节点,旧的节点)
     list.insertBefore(js,ee);
 </script>
```

jQuery网站：http://jquery.cuishifeng.cn/

