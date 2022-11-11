#### 1.注册驱动

```java
Class.forName("com.mysql.cj.jdbc.Driver");//mysql8.0
Class.forName("com.mysql.jdbc.Driver");//mysql8.0以前
```

#### 2.获取连接

```java
//String url = "jdbc:mysql://127.0.0.1:3306/test";//5.7这样写
//String url = "jdbc:mysql://127.0.0.1:3306/test?useSSL=false&serverTimezone=UTC";//mysql8需要添加时区信息
String url = "jdbc:mysql://127.0.0.1:3306/test?&useSSL=false&serverTimezone=UTC";//加上&也可以
//如果连接的是本地mysql服务器并且默认端口是3306  127.0.0.1:3306 
String username="root";//账户名
String password="123456";//密码
Connection conn = DriverManager.getConnection(url, username, password);//获取数据集连接对象

```

#### 3.获取 sql 执行对象

```java
//获取执行sql对象 Statement
Statement stmt = conn.createStatement();

//处理结果集
ResultSet rs = null;

rs=stmt.executeQuery(sql);//executeQuery 执行select语句
rs=stmt.executeUpdate(sql);//executeUpdate 执行 INSERT、UPDATE 或 DELETE 语句以及 SQL DDL（数据定义语言）语句，例如 CREATE TABLE 和 DROP TABLE。INSERT、UPDATE 或 DELETE 语句的效果是修改表中零行或多行中的一列或多列。executeUpdate 的返回值是一个整数（int），指示受影响的行数（即更新计数）。对于 CREATE TABLE 或 DROP TABLE 等不操作行的语句，executeUpdate 的返回值总为零。
rs=stmt.execute(sql);//方法execute：可用于执行任何SQL语句，返回一个boolean值，表明执行该SQL语句是否返回了ResultSet。如果执行后第一个结果是ResultSet，则返回true，否则返回false。但它执行SQL语句时比较麻烦，通常我们没有必要使用execute方法来执行SQL语句，而是使用executeQuery或executeUpdate更适合，但如果在不清楚SQL语句的类型时则只能使用execute方法来执行该SQL语句了。

```

#### JDBC API 详解

```java
//Connection
1.获取执行sql对象
	//普通执行sql对象
	Statement createStatement()
	//预编译sql的执行sql对象防止sql注入
	PreparedStatement prepareStatement(sql)
	//执行存储过程的对象
	CallableStatement prepareCall(sql)
2.事务管理
    开启事务：setAutoCommit(boolean autoCommit); //true为自动提交事务，false为手动
	提交事务：commit()
    回滚事务: rollback();
//Statement
    1.执行sql语句
    	int executeUpdate(sql) //执行DML,DDL语句
    	//返回值DML语句影响的行数，DDL语句执行后，成功也可能返回0
    	ResultSet executeQuery(sql)://执行DQL语句
		//返回值：ResultSet 结果集对象

//ResultSet
	1.封装了DQL查询语句的结果
        ResultSet stmt.executeQuery(sql):执行DQL语句返回ResultSet对象
      获取查询结果
      	boolean next()://将光标向后移动一行，判断当前行是否为有效行
			返回值：
                true：有效行，当前行有数据
                false ： 无效行，当前行无数据
        xxx getXxx(参数):获取数据
         xxx:数据类型；如 Int getInt(参数) String getString(参数)
        参数：
             int:列的编号，从1开始
             String ：列名
                 
//PreparedStatement
     PreparedStatement作用
        1.预编译sql语句并执行，预防sql注入
            //获取 PreparedStatement 对象
                 //sql语句中的参数值，使用?占位符替代
                 String sql = "select * from user where uesrname = ? and password = ?";
				//通过Connection对象获取，并传入对应的sql语句
				PreparedStatement pstmt = conn.prepareStatement(sql); 
			//设置参数值
				PreparedStatement对象：setXxx(参数1,参数2):给?赋值
                    Xxx：数据类型：如setInt(参数1,参数2);
					参数：
                        参数1:?的位置编号，从1开始
                        参数2:?的值
                            
             //执行sql
                  executeUpdate();/executeQuery();:不需要传递sql
		
     sql注入
         sql注入是通过操作输入来修改事先定义好的sql语句。用以达到执行代码对服务器进行攻击的方法
                 
```



 
