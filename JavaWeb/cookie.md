## Cookie基本使用

​	Cookie：客户端会话技术，将数据保存到客户端，以后每次请求都携带Cookie数据进行访问

### 	Cookie基本使用：

#### 		发送cookie

​		1.创建Cookie对象，设置数据

```java
Cookie cookie = new Cookie("key","value");//username,zs
```

​		2.发送Cookie对象到客户端：使用response对象

```java
response.addCookie(cookie);
```

#### 		获取cookie

```java
//获取cookie用request
Cookie[] cookies = request.getCookies();
//遍历数组取出每一个cookie
        for (Cookie cookie : cookies) {
            String name = cookie.getName();
           if ("username".equals(name)){
               String value = cookie.getValue();
               System.out.printf("%s:%s",name,value);//username:zs
           }

        }
```

### Cookie原理

Cookie的实现是基于HTTP协议的

​	响应头：set-cookie

![image](https://github.com/zyqaq412/note/blob/main/img/JavaWeb/cookie响应标头.png)

![image](..\img\JavaWeb\cookie响应标头.png)

​	请求头：cookie

![image](https://github.com/zyqaq412/note/blob/main/img/JavaWeb/cookie请求头.png)

![image](..\img\JavaWeb\cookie请求头.png)

### Cookie使用细节

#### 	Cookie存活时间

​		默认情况下，Cookie存储在浏览器内存中，当浏览器关闭，内存释放，则Cookie销毁

​		setMaxAge(int seconds) 设置Cookie存活时间

​			1.正数：将Cookie写入浏览器所在电脑的硬盘，持久化存储，到时间自动删除

​			2.负数：默认值，Cookie在当前浏览器内存中，当浏览器关闭，则Cookie被销毁

​			3. 零：删除对应Cookie

#### 	Cookie存储汉字

```java
Cookie cookie = new Cookie("username\n","张三");
//cookie不支持中文
java.lang.IllegalArgumentException: Control character in cookie value or attribute.
 //如果要存储中文，则需进行转码：URL编码
String value = "张三";
        value=URLEncoder.encode(value,"UTF-8");
        System.out.println("value :"+value);
        Cookie cookie = new Cookie("username",value);
```



## Session基本使用

### 	session介绍

​			服务端会话跟踪技术，将数据保存到服务器

​					Session是存储在服务端而Cookie是存储在客户端

​					存储在客户端的数据容易被窃取和截获，存在很多不安全的因素

​					存储在服务端的数据相比于客户端来说就更安全

​			JavaEE提供HttpSeesion接口，来实现一次会话的多次请求数据共享功能

​			使用：

​					获取Seesion对象

```java
HttpSeesion seesion = request.getSeesion();
```

​					Session对象功能

```java
void setAttribute(String name,Object o);//存储数据到session域中
Object getAttribute(String name);//根据key值获取值
void removeAttribute(String name);//根据key值删除键值对

```

### 	session原理

​		session是基于cookie实现的

```java
//浏览器请求头cookie会带一个：JSESSIONID=F6480D00F839998CA5E6DDE71093CF18
//Cookie: JSESSIONID=F6480D00F839998CA5E6DDE71093CF18; username=%E5%BC%A0%E4%B8%89
HttpSession session = request.getSession();
//服务器获取session时会看有没有 JSESSIONID=F6480D00F839998CA5E6DDE71093CF18 的session
//有就返回，没有就获取一个新的
```

### 	session使用细节

​		session 钝化 活化：
​			服务器重启后，session中的数据是否还存在

​			钝化 ：在服务器正常关闭后，tomcat会自动将session的数据写入硬盘中

​					钝化的数据路径为:`项目目录\target\tomcat\work\Tomcat\localhost\项目名称\SESSIONS.ser`

![image](../img/JavaWeb/session钝化.png)

​			活化：再次启动服务器后，会从文件中加载数据到session中

​					数据加载到Session中后，路径中的`SESSIONS.ser`文件会被删除掉 

​		session销毁

```xml
<!--默认30分钟无操作销毁-->
<session-config>
    <session-timeout>30</session-timeout>
  </session-config>
```

```java
//调用session对象的invalidate()方法
```

## cookie和session小结

* Cookie 和 Session 都是来完成一次会话内多次请求间==数据共享==的。

所需两个对象放在一块，就需要思考:

Cookie和Session的区别是什么?

Cookie和Session的应用场景分别是什么?

* 区别:
  * 存储位置：Cookie 是将数据存储在客户端，Session 将数据存储在服务端
  * 安全性：Cookie不安全，Session安全
  * 数据大小：Cookie最大3KB，Session无大小限制
  * 存储时间：Cookie可以通过setMaxAge()长期存储，Session默认30分钟
  * 服务器性能：Cookie不占服务器资源，Session占用服务器资源
* 应用场景:
  * 购物车:使用Cookie来存储
  * 以登录用户的名称展示:使用Session来存储
  * 记住我功能:使用Cookie来存储
  * 验证码:使用session来存储
* 结论
  * Cookie是用来保证用户在未登录情况下的身份识别
  * Session是用来保存用户登录后的数据
