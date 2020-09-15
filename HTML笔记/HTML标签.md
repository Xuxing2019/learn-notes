### html常用标签：

<!DOCTYPE html>    //指定文档的类型，为html类型
<html>        //开始标签，对应结束标签

<head>     //html必备标签，表示头部

<title>     //设置网页标题，最后显示在浏览器的头部
</title>

<meta charset="utf-8" />  //定义字符集，utf-8 解释中文乱码
</head>

<body>     //html必备标签，表示身体

</body>

</html>
1、 <!--   -->：写注释的快捷键，或者是注释掉一部分内容，用ctrl+/ 。  并注意浏览器只解释标签，不解释注释里面的。  写注释的好处就是提高代码的可读性

2、<h1>~<h6>  </h1>~</h6> :  标题标签   其中可以以 属性名=“属性值”的方式设置标题样式，<h1  align="center" > 标题 </h1>       align="center"  用来设置对齐方式，居中对齐

3、<p>段落标签</p> : 每一个段落之间会空一行，段落里面会有很多的嵌套

4、<em>斜体</em>: 斜体的运用不广泛，但是有的时候必须要，em为斜体的标签元素

5、<strong>加粗</strong>: <strong>加粗很常见，有的时候加粗的文字不一定是标题，有的可能就是直接加粗



6、<hr />: 水平线，横线，它就是一条直线，并且它是一个单标签

7、<img src="" alt="" width="" height="" />:   单标签，src指定图片的路径。alt图片资源路径没用时，替代的文本。width和height用来设置图片的宽度和高度
6.链接标签<a> <!--

  a标签

  href：必填，表示跳转那个页面

  target:表示窗口在那里打开 ——blank在新的窗口打开 _self在当前窗口打开

-->

```html
<i>...</i>                      斜体字 

<em>...</em>              斜体字(强调)

<center>…</center>   居中文本

<ul>…</ul>                 无序列表 

<ol>…</ol>                 有序列表

<li>…</li>                    列表项目
自定义列表：
<dl>
    <dt>学科</dt>
    <dd>java</dd>
        <dd>linux</dd>
        <dd>python</dd>  
    <dd>c++</dd>
</dl>


<font>                         定义文本字体尺寸、颜色、大小

<sub>                         下标

<sup>                         上标

<br>                           换行

<p>                            段落
    
    
    <table>…</table>   定义表格

<th>…</th>            定义表格中的表头单元格

<tr>…</tr>             定义表格中的行

<td>…</td>           定义表格中的单元
    
    
    <form>…</form>    定义供用户输入的 HTML 表单

<frame>                 定义框架集的窗口或框架
    
    <!--音频和视频-->
    <video>：视频， contorls 控制条，autoplay：自动播放
    <video src="..."" contorls autoplay></video>
     <audio>:音频    contorls 控制条，autoplay：自动播放
     <audio src="..." contorls autoplay></audio></video>
         
                     
                     
    
```



**表单**

```html
    <h1>注册</h1>
    <!-- 
        表单form
        action:表单的提交位置，可以是网站，也可以是请求地址
        method:post,get提交方式
        get：提交的方式我们能在url看到我们的提交的信息，不安全但是 高效
       post：比较安全，传输大文件，

     -->
     <form action="列表.html" method="POST">
     <!-- 文本输入框 -->
     <p>名字：<input type="text" name="username"></p>
     <!-- 密码框 -->
     <p>密码：<input type="password" name="pwd"></p>
         
         
     <!-- 单选框标签
    input type ="radio"
    value:单选框的值
    name:表示组
checked：默认选中
    -->
    <p>
        性别：
        <input type="radio" value="boy" name="sex"/>男
        <input type="radio" value="girl" name="sex"/>女

    </p>
         
         
         
    <!-- 多选框
    
        input type="checkbox"
checked：默认选中
    -->
     
    <p>
      爱好:
      <input type="checkbox" value="sleep" name="hobby">睡觉：
      <input type="checkbox" value="code" name="hobby">打代码
      <input type="checkbox" value="chat" name="hobby">聊天
      <input type="checkbox" value="game" name="hobby">游戏
    </p>

     
<!-- 按钮
  input type="button" 普通
  input type="image"  图片
  input type="submit" 提交
  input type="reset"  重置
-->
    <p>按钮：
        <input type="button" name="btn1" value="点击变成">
        图片按钮：
        <input type="image" src="resources\images\QQ图片20200321231838.jpg">
    </p>
   <!-- 下拉框，列表框 -->
    <p>城市：
        <select name="城市名称">
            <option value="beiing">北京</option>
            <option value="hangzhou">杭州</option>
            <option value="shanghai">上海</option>
            <option value="shenzhen">深圳</option>
            <option value="guangzhou">广州</option>
   
        </select>
   
     </p>
        <!-- 文本域
            cols:30列
            rows:10行
       -->
       <p>反馈：
           <textarea name="textarea" id="" cols="30" rows="10">文本内容</textarea>
       </p>
   
       <!-- 文件域 
          input type="file" name="files"
         
       -->
      <p>
          <input type="file" name="files">
          <input type="button" value="上传" name="upload">
      </p>
   
     
         
         
       <!-- 邮件验证 -->
        <p>邮箱:
            <input type="email" name="email">

        </p>
        <!-- URL -->
        <p>URL:
<input type="url" name="url" >
<!-- 数字 -->
        </p>
       <input type="number" name="num" max="100" step="10">

       <!-- 滑块
    input type="range"
    -->
        <P>音量:
            <input type="range" min="0" max="100">


        </P>

        <!-- 搜索框search -->
        <p>搜索:
            <input type="search" name="search">

        </p>

       
         
     <p>
        <!-- 提交 -->
         <input type="submit">
         <!-- 重置 -->
         <input type="reset">
     </p>
    </form>
```

表单元素格式：

![QQ截图20200322152225](C:\Users\Administrator\Desktop\HTML\QQ截图20200322152225.jpg)



**表单的应用：**

disabled：禁用

hidden：隐藏

```
     <!-- 增强鼠标可用性 根据id指向一个位置-->
        <p> <label for="mark">点我</label>
            <input type="text" id="mark">
        </p>
```

placeholder：提示信息（用在所有的输入框中）

required：非空判断（用在所有的输入框中）

pattern 正则表达式判断

