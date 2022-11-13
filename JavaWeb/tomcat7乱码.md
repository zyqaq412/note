请求乱码

```java
//post方法
		设置请求字符编码就行
		request.setCharacterEncoding("utf-8");//设置请求字符编码
//get方法
	/*
	get方法的参数在url上 浏览器会以utf-8的格式进行url编码
	tomcat7 会以 ISO-8859-1 的格式解码 所以会乱码
	
	*/

String name = "张三";
//URL编码
String encode = URLEncoder.encode(name,"utf-8");
System.out.println(encode);//%E5%BC%A0%E4%B8%89

//URL解码
String decode = URLDecoder.decode(encode,"utf-8");
System.out.println(decode);//张三

//tomcat7 解码
String decode1 = URLDecoder.decode(encode,"ISO-8859-1");
System.out.println(decode1);//å¼ ä¸

//解码和编码是tomcat服务器自己完成
//解决get乱码

public static String luanMa(String str){
        try {
            //tomcat以ISO-8859-1解码 我们以ISO-8859-1格式转换为字节数组
            byte[] bytes = str.getBytes("ISO-8859-1");
            //再将字节数组转为字符串
            String s = new String(bytes,"utf-8");
            return s;
        } catch (UnsupportedEncodingException e) {
            throw new RuntimeException(e);
        }
    }
String username = "张三";
String username = UTIL.luanMa(request.getParameter("username"));
System.out.println(username);//张三
```

​	

响应乱码

```java
response.setContentType("text/html;charset=utf-8");//设置响应字符编码
```



