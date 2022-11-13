如果使用 Maven 来构建项目，则需将下面的依赖代码置于 pom.xml 文件中：

```xml
<dependency>
  <groupId>org.mybatis</groupId>
  <artifactId>mybatis</artifactId>
  <version>x.x.x</version>
</dependency>

<!--导入mysql 驱动jar包 配合mybatis使用 -->
    <dependency>
      <groupId>mysql</groupId>
      <artifactId>mysql-connector-java</artifactId>
      <version>8.0.17</version>
    </dependency>
```

创建mybatis-config.xml核心配置文件

官网配置模板

```xml
<?xml version="1.0" encoding="UTF-8" ?>
<!DOCTYPE configuration
  PUBLIC "-//mybatis.org//DTD Config 3.0//EN"
  "http://mybatis.org/dtd/mybatis-3-config.dtd">
<configuration>
  <environments default="development">
    <environment id="development">
      <transactionManager type="JDBC"/>
      <dataSource type="POOLED">
        <property name="driver" value="${driver}"/>
        <property name="url" value="${url}"/>
        <property name="username" value="${username}"/>
        <property name="password" value="${password}"/>
      </dataSource>
    </environment>
  </environments>
  <mappers>
    <mapper resource="org/mybatis/example/BlogMapper.xml"/>
  </mappers>
</configuration>

```

```xml
<!---->
<?xml version="1.0" encoding="UTF-8" ?>
<!DOCTYPE configuration
        PUBLIC "-//mybatis.org//DTD Config 3.0//EN"
        "http://mybatis.org/dtd/mybatis-3-config.dtd">
<configuration>
    <!--给 com.hzy.pojo 包下的实体类取别名 默认类名  -->
   <typeAliases>
      <package name="com.hzy.pojo"/>
   </typeAliases>    
    <!--
    environments：配置数据库连接环境信息。可以配置多个environment，通过default属性切换不	同的environment
    -->
    <environments default="development">
        <environment id="development">
            <transactionManager type="JDBC"/>
            <dataSource type="POOLED">
                <!--数据库连接信息-->
                <property name="driver" value="com.mysql.cj.jdbc.Driver"/>
				<!--  <property name="url" 		
			value="jdbc:mysql://localhost:3306/studenttest?&amp;//这里不要& 会报错
			useSSL=false&amp;serverTimezone=UTC"/>              -->
                <property name="url" value="jdbc:mysql://localhost:3306/test?useSSL=false&amp;serverTimezone=UTC"/>
                <property name="username" value="root"/>
                <property name="password" value="123456"/>
            </dataSource>
        </environment>
    </environments>
    <mappers>
        <!--加载sql映射文件-->
       <!-- <mapper resource="com/hzy/mapper/UserMapper.xml"/>-->
        <!--Mapper代理方式-->
        <package name="com.hzy.mapper"/>
    </mappers>
</configuration>
```



UserMapper.xml映射文件，UserMapper接口(实体类映射文件和查询接口)

UserMapper.xml

UserMapper接口   的目录结构要相同

![image](https://github.com/zyqaq412/note/blob/main/img/JavaWeb/image-20221111133509550.png)
![image](https://github.com/zyqaq412/note/blob/main/img/JavaWeb/image-20221111133455041.png)

![image](..\img\JavaWeb\image-20221111133455041.png)![image](..\img\JavaWeb\image-20221111133509550.png)

```xml
<?xml version="1.0" encoding="UTF-8" ?>
<!DOCTYPE mapper
        PUBLIC "-//mybatis.org//DTD Mapper 3.0//EN"
        "http://mybatis.org/dtd/mybatis-3-mapper.dtd">
<!--
    namespace:名称空间
-->
<mapper namespace="com.hzy.mapper.UserMapper">
    <!--<select id="selectAll" resultType="com.hzy.pojo.User">-->
    <!--取了别名后就不需要加包名，也不分大小写-->
    <select id="selectAll" resultType="User">
        select *
        from user;
    </select>
    <select id="selectById" resultType="user">
        select *
        from user where id = #{id};
    </select>
</mapper>
```

