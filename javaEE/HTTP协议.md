### Http

#### 4.1、什么是HTTP

<hr>

HTTP(超文本传输协议)是一个简单的请求响应协议，它通常在TCP之上。

- 文本：html，字符串，~...
- 超文本：图片，视频，音频，定位，地图...
- 80

https:安全的

- 443

#### 4.2、两个时代

http1.0

HTTP/1.0:客户端可以与web服务器连接后，只能获得一个web资源，断开资源。

http2.0

HTTP/1.1:客户端可以与web服务器连接后，可以获得多个web资源。

#### 4.3Http请求

**客户端--发请求--服务器**

百度：

```Java
Request URL: https://www.baidu.com/ --请求地址
Request Method: GET --get请求方式  
Status Code: 200 OK    状态码：200
Remote(远程) Address: 36.152.44.95:443
Referrer Policy: unsafe-url
```

**1.请求行**

请求行中的请求方式：GET

请求方式：Get，Post，HEAD.DELETE,PUT,TRACT..

   **get:**请求能够携带的参数比较少，大小有限制，会在浏览器的URL地址宜兰显示数据内容，不安全，但是高效。

  **post：**请求能够携带的参数比较多，大小没有限制，不会在浏览器的URL地址宜兰显示数据内容，安全，但是不高效。

**2.消息头**

```java 
Accept:--告诉浏览器，它所支持的数据类型
Accept-Encoding: --支持那种编码格式   GBK  UTF-8 GB2312  ISO8859-1
Accept-Language: 告诉浏览器语言
Cache-Control:缓存控制
Connection: 告诉浏览器，请求完成是断开还是保持连接
HOST:主机..../

```



#### 4.4Http响应

**服务端-响应-客户端**

百度：

```Java
Cache-Control: private   --缓存控制
Connection: keep-alive   --连接
Content-Encoding: gzip    --编码
Content-Type: text/html;charset=utf-8 --类型
```

**1.响应体**

```Java
Accept:--告诉浏览器，它所支持的数据类型
Accept-Encoding: --支持那种编码格式   GBK  UTF-8 GB2312  ISO8859-1
Accept-Language: 告诉浏览器语言
Cache-Control:缓存控制
Connection: 告诉浏览器，请求完成是断开还是保持连接
HOST:主机..../
Refrush:告诉客户端，多久刷新一次
Location:网页重新定位；
```

**2.响应状态码（重点）**

200：请求响应成功 200

3xx：请求重定向

   重定向：重新到新的位置

4xx：资源不存在 404

5xx:服务器代码错误  500  502：网关错误



**常见面试题：**

当你的浏览器中地址栏输入地址并回车的一瞬间到页面能够展示回来，经历了什么？

 