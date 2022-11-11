# String常用方法

##### 1.charAt(int index)

```java
//返回指定索引的 char值

char c = "中国人".charAt(1);//”中国人“是一个对象，只要是对象就能，对象.方法()

System.out.println(c);//国
```

##### 2.int compareTo(String anotherString)

```java
//比较两个字符串的字典。
int result = "abc".compareTo("abc");
System.out.print("" + result);//0
int result4 = "cdab".compareTo("abcf");
//拿着字符串第一个字母和后面字符串的第一个字母比较，能分出大小就不再继续比较
System.out.print(" " + result4);//2(大于0)前大后小
```

##### 3.boolean contains(CharSequenec s)

```java
//判断前面字符串是否包含后面的子字符串

System.out.println("acv".contains("a"));//true
```

##### 4.boolean endsWith(String suffix)

```java
//判断当前字符串是否以某个字符串结尾

System.out.println("acv".endsWith("v"));//true
```

##### 5.boolean equals(Object anObject)

```java
//比较两个字符串必须使用equals方法不能使用==

//equals方法有没有调用2.compareTo方法？没有,equals方法只能看出是否相等，

//compareTo方法可以看出是否相等同时还能看出谁大谁小

System.out.println("acd".equals("acd"));//true
```

##### 6.boolean equalsIgnoreCase(String anotherString)

```java
//判断两个字符串是否相等忽略大小写

System.out.println("ACD".equals("acd"));//true
```

##### 7.byte[] getBytes()

​	将字符串对象转换成字节数组

```java
byte[] bytes = "abcdef".getBytes();
       for (int i = 0; i < bytes.length; i++) {
           System.out.print(bytes[i] + " ");//
       }
       System.out.println();
```

##### 8.int indexOf(String str)

​	判断某个字符串在当前字符串中第一次出现的索引

```java
System.out.println("adsada".indexOf("s"));//2
```

##### 9.boolean isEmpty()

​	判断某个字符串是否为空

```java
String s = null;//空指针异常
String s = "";
System.out.println(s.isEmpty());//true
```

##### 10.int length()

```java
//面试题：判断数组长度和判断字符串长度不一样
//判断数组长度是length属性，判断字符串长度是length()方法
int[] a = {1, 2, 3};
System.out.println(a.length);//3
System.out.println("abc".length());//3
```

##### 11.int lastIndexOf(String str)

```java
//判断某个子字符串在当前字符串最后一次出现的索引
System.out.println("abca".lastIndexOf("a"));//3
```

##### 12.String replace(CharSequence target, CharSequence replacement)

```java
//替换
//String的父接口就是：CharSequence
System.out.println("http://www.baidu.com".replace("http://", "https://"));
```

##### 13.String[] split(String regex)

```java
//拆分字符串
        String[] a1 = "1980-10-11".split("-");//"1980-10-11"以"-"分隔符进行拆分
        for (int i = 0; i < a1.length; i++) {
            System.out.print(a1[i] + " ");
        }
```

##### 14.boolean startsWith(String prefix)

```java
//判断某个字符串是否以某个子字符串开始
        System.out.println("abcfdf".startsWith("a"));//true

```

##### 15.String substring(int beginIndex)

```java
//参数是起始下标
//截取字符串
System.out.println("abcdefghijk".substring(2));
```

##### 16.String substring(int beginIndex, int endIndex)

```java
System.out.println("abcdefghijk".substring(2, 7));//起始包括，结尾不包括[2,7)

```

##### 17.char[] toCharArray()

```java
//将字符串转换为char数组
        char[] chars = "我是中国人".toCharArray();
        for (int i = 0; i < chars.length; i++) {
            System.out.print(chars[i] + " ");
        }
```

##### 18.String toLowerCase()

```java
//转换为小写
        System.out.println("ABC".toLowerCase(Locale.ROOT));
```

##### 19.String toUpperCase()

```java
//转换为大写
System.out.println("abc".toUpperCase(Locale.ROOT));
```

##### 20.String trim()

```java
 //去除字符串前后空白
        System.out.println("   a b c    ".trim());
```

##### 21.valueOf()

```java
//静态方法
//将非字符串转为字符串
//String s1 = String.valueOf(3.14);
//当参数是对象时会自动调用toString方法
String s1 = String.valueOf(new Customer());
System.out.println(s1);
```

