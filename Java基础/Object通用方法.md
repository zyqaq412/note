##### 概览

```java

public native int hashCode()

public boolean equals(Object obj)

protected native Object clone() throws CloneNotSupportedException

public String toString()

public final native Class<?> getClass()

protected void finalize() throws Throwable {}

public final native void notify()

public final native void notifyAll()

public final native void wait(long timeout) throws InterruptedException

public final void wait(long timeout, int nanos) throws InterruptedException

public final void wait() throws InterruptedException
```

##### equals()

###### 1.等价关系

```java
//自反性
    
x.equals(x); // true
//对称性

x.equals(y) == y.equals(x); // true
//传递性

if (x.equals(y) && y.equals(z))
    x.equals(z); // true;
//一致性

多次调用 equals() 方法结果不变

x.equals(y) == x.equals(y); // true
//与 null 的比较

对任何不是 null 的对象 x 调用 x.equals(null) 结果都为 false

x.equals(null); // false;
```

###### 2.等价与相等

- 对于基本类型，== 判断两个值是否相等，基本类型没有 equals() 方法。
- 对于引用类型，== 判断两个变量是否引用同一个对象，而 equals() 判断引用的对象是否等价。