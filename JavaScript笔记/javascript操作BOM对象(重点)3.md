### 一.操作BOM对象（重点）

> 浏览器介绍

JavaScript和浏览器的关系？

JavaScript的诞生就是为了能在浏览器上运行！

BOM:浏览器对象模型

- IE 6~11

- Chrome

- safari

- FireFox

  三方：

  QQ浏览器

  360浏览器

  > **window**

  window代表浏览器的窗口

```JavaScript
window.alert(1)
true
alert: 1 blog-common.min.js:1:69700
window.innerHeight
138
window.innerWidth
1696
window.outerHeight
932
window.outerWidth
1723
//可以调整浏览器窗口试试...
```

> **Navigator**

Navigator，封装了浏览器的信息

```JavaScript
navigator.appName
"Netscape"
navigator.appVersion
"5.0 (Windows)"
navigator.userAgent
"Mozilla/5.0 (Windows NT 10.0; Win64; x64; rv:74.0) Gecko/20100101 Firefox/74.0"
navigator.platform
"Win32
```

大多数时候，我们不会使用**navigator**对象，因为会被人为修改！

不建议使用这些属性来判断编写代码

> **screen**

代表屏幕的尺寸

```JavaScript
screen.width
1484
screen.height
928
```



> location （重要）

location代表当前页面的URL的信息

```JavaScript
host: "www.cnblogs.com"
href: "https://www.cnblogs.com/loveyaxin/p/11151586.html"
protocol: "https:"
reload: reload()//刷新网页
//设置新的地址
location.assign('https://blog.kuangstudy.com/')
```



> document

document代表当前的页面信息，HTML DOM文档树

```JavaScript
document.title
"百度一下，你就知道"
document.title="郭金荣"
"郭金荣"
```

获取具体的文档树节点（就是html这些）

```JavaScript
<dl id="app">
    <dt>java</dt>
    <dd>javaSE</dd>
    <dd>javaEE</dd>
 </dl>
<script>

    var dl=document.getElementById('app');
</script>
```

获取网页的cookie

```JavaScript
document.cookie
"__gads=ID=b3d87c38ebfb47be:T=1584494092:S=ALNI_MYdXii3FrsgyCFbeFj8xBv8EhzvtQ; Hm_lvt_742e9bdb6e867044bb348deab863d79d=1584603424; _gat=1; _ga=GA1.2.1455459806.1584414382; _gid=GA1.2.1150551890.1585203158"
```

劫持cookie原理

www.taobao.com

```
<script src="aa.js"></script>
<!--恶意人员：获取你的cookie上传到他的服务器>
```

服务器端可以设置cookie:httpOnly （只读的）

> history

```javascript
history.back()//前进
history.forward()//后退
```

