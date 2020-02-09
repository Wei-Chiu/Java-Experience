# Mybatis 配置文件

在 MyBatis 单独使用时，需要通过 SqlSessionFactoryBuilder 创建 SqlSessionFactory，再通过 SqlSessionFactory 获取 SqlSession。

*静态工具类如下:* 

```java
package Utils;

import org.apache.ibatis.io.Resources;
import org.apache.ibatis.session.SqlSession;
import org.apache.ibatis.session.SqlSessionFactory;
import org.apache.ibatis.session.SqlSessionFactoryBuilder;

import java.io.IOException;
import java.io.InputStream;

public class MybatisUtils {


    private static  SqlSessionFactory sqlSessionFactory;

    static  {
        try {
            String resource = "mybatis-config.xml";
            InputStream inputStream = Resources.getResourceAsStream(resource);
            sqlSessionFactory = new SqlSessionFactoryBuilder().build(inputStream);
        } catch (IOException e) {
            e.printStackTrace();
        }
    }

    public static SqlSession getSqlSession() {
        return sqlSessionFactory.openSession();
    }
}

```

*测试类调用如下：*

```java
@Test
public void addBlog() {
    SqlSession sqlSession = MybatisUtils.getSqlSession();
    BlogMapper mapper = sqlSession.getMapper(BlogMapper.class);

    Blog blog = new Blog();
    blog.setId(IDUtils.getId());
    blog.setTitle("Mybatis is so easy");
    blog.setAuthor("kuangTalk");
    blog.setCreateTime(new Date());
    blog.setViews(9999);

    mapper.addBlog(blog);

    blog.setId(IDUtils.getId());
    blog.setTitle("Spring is so easy");
    mapper.addBlog(blog);

    blog.setId(IDUtils.getId());
    blog.setTitle("WeChat is so easy");
    mapper.addBlog(blog);

    sqlSession.commit();
    sqlSession.close();
}
```

*MyBatis XML 配置如下：*

```xml
<?xml version="1.0" encoding="UTF-8" ?>
<!DOCTYPE configuration
        PUBLIC "-//mybatis.org//DTD Config 3.0//EN"
        "http://mybatis.org/dtd/mybatis-3-config.dtd">

<configuration>
    <!-- 外部配置文件，优先使用配置文件中的值 -->
    <properties resource="db.properties">
    <!-- 可以增加属性配置-->
<!--        <property name="" value=""/>-->
    </properties>

    <!--  引入日志  -->
    <settings>
        <!-- 默认日志工厂，不需要自己配置-->
        <setting name="logImpl" value="STDOUT_LOGGING"/>
        <!-- 数据库名到实体类名的自动映射 -->
        <setting name="mapUnderscoreToCamelCase" value="true"/>
        <!--显示开启缓存-->
<!--        <setting name="cacheEnabled" value="true"/>-->
    </settings>

    <!-- 别名 -->
    <typeAliases>
    <!--为实体类起别名，可以自己取名字-->
<!--        <typeAlias type="pojo.User" alias="UUUser"></typeAlias>-->
    <!--添加实体类搜索包名，不能自己取名字，除非在实体类定义时添加：@Alias("")-->
<!--        <package name="pojo"/>-->
    </typeAliases>

    
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

    <!-- 绑定 mapper-->
    <mappers>
        <mapper class="mapper.StudentMapper"/>
        <mapper class="mapper.TeacherMapper"/>
        <mapper class="mapper.BlogMapper"/>
    </mappers>

</configuration>
```

