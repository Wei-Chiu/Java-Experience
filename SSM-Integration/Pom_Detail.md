# pom 中每个依赖到底提供了哪些类

```xml
<!-- 
 - 从数据库，到控制器，到前端的思路： 
 - 
 - 数据库端：
 - mybatis：用于例如 mybatis-config.xml 的支持，在 sqlSessionFactory 创建的时候传入
 - c3p0：数据库连接池，用于配置 dataSource
 - mysql-connector-java：配置数据库驱动，只要使用 mybatis 就需要配置
 - spring-jdbc：用于用于在 spring-service 中配置事务管理器 DataSourceTransactionManager
 - mybatis-spring：用于在：配置SqlSessionFactory对象，注册MapperScannerConfigurer
 - 
 - 框架：
 - spring-webmvc：用于支持 spring-mvc 框架
 - 
 - 前端：
 - jstl：用于 jsp 页面的编写，在 allBook.jsp 中，第一行
 - 
 - 其他：
 - junit：单元测试
 - lombok：自动生成 get set 方法
 ->

<dependencies>
    <!--Junit-->
    <dependency>
        <groupId>junit</groupId>
        <artifactId>junit</artifactId>
        <version>4.12</version>
    </dependency>
    <!--数据库驱动-->
    <dependency>
        <groupId>mysql</groupId>
        <artifactId>mysql-connector-java</artifactId>
        <version>5.1.47</version>
    </dependency>
    <!-- 数据库连接池 -->
    <dependency>
        <groupId>com.mchange</groupId>
        <artifactId>c3p0</artifactId>
        <version>0.9.5.2</version>
    </dependency>

    <!--Servlet - JSP -->
    <dependency>
        <groupId>javax.servlet</groupId>
        <artifactId>servlet-api</artifactId>
        <version>2.5</version>
    </dependency>
    <dependency>
        <groupId>javax.servlet.jsp</groupId>
        <artifactId>jsp-api</artifactId>
        <version>2.2</version>
    </dependency>
    <dependency>
        <groupId>javax.servlet</groupId>
        <artifactId>jstl</artifactId>
        <version>1.2</version>
    </dependency>

    <!--Mybatis-->
    <dependency>
        <groupId>org.mybatis</groupId>
        <artifactId>mybatis</artifactId>
        <version>3.5.2</version>
    </dependency>
    <dependency>
        <groupId>org.mybatis</groupId>
        <artifactId>mybatis-spring</artifactId>
        <version>2.0.2</version>
    </dependency>

    <!--Spring-->
    <dependency>
        <groupId>org.springframework</groupId>
        <artifactId>spring-webmvc</artifactId>
        <version>5.1.9.RELEASE</version>
    </dependency>
    <dependency>
        <groupId>org.springframework</groupId>
        <artifactId>spring-jdbc</artifactId>
        <version>5.1.9.RELEASE</version>
    </dependency>
</dependencies>
```