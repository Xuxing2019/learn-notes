### 1.操作表单（验证）

> 表单是什么  form表单  DOM树

- 文本框 text
- 下拉框 <select>
- 单选框 radio
- 多选框 checkbox
- 隐藏域 hidden
- 密码框 password
- ....

表单的目的：提交信息

> 获得要提交的信息

```JavaScript
     var input_text=document.getElementById('username');
      var boy_text=document.getElementById('boy');
      var girl_text=document.getElementById('girl');


     //得到输入框的值
     input_text.value;
     //更改输入框的值
     input_text.value='123';

     //对于单选框，多选框等等固定的值。boy_radio.value只能取到当前的值
     boy_text.checked;//返回的结果，是否为true。如果为true，则被选中~
     //选中指定的单选框
     girl_text.checked='true'//赋值

```

#### 2.提交表单

**md5.加密密码，表单的优化**

```HTML

 <script src="https://cdn.bootcss.com/blueimp-md5/2.10.0/js/md5.min.js"></script>
<!--
 表单绑定提交时间 onclik
-->

<form action="https://www.cnblogs.com/jun1019/p/6243295.html" method="post" onsubmit="return  a()">
    <p>  <span>用户名：</span><input type="text" id="username" name="username">
    </p>
        <p><span>密码：</span><input type="password" id="password" name="password"></p>

<!--     绑定事件 onclick 被点击-->
<button type="submit" >提交</button>
</form>

<script>
    function a() {

        var username_value=document.getElementById('username');
        var password_value=document.getElementById('password');
        var md5pwd=document.getElementById('md5-password');
        console.log(username_value.value);
        console.log(password_value.value);
        password_value.value=md5(pwd.value);
          //MD5算法
            md5pwd=md5(pwd.value)
        //可以验证判断表单内容true就是提交，flase，不能提交

       return true;
    }
</script>
```

