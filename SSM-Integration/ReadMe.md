# [SSM完整环境搭建过程](https://blog.kuangstudy.com/index.php/archives/487/)

## 基本环境搭建

1. 新建一个 maven 项目，添加 web 支持
2. 倒入相关 pom [依赖](../SSM-Integration/Pom_Detail.md)，在 pom 中设置[资源过滤](../SSM-Integration/Resource_Filter.md)
3. 建立基本结构和配置框架：

   - src.java.pojo
   - src.java.dao
   - src.java.service
   - src.java.controller
   - [mybatis-config.xml](../SSM-Integration/mybatis-config.md)
   - [applicationContext.xml](../SSM-Integration/applicationContext.md)

## Mybatis 层编写

4. 配置数据库文件 [database.properties](../SSM-Integration/dataBaseProperties.md)
5. IDEA 连接数据库
6. 编写 Mybatis 核心配置文件 [mybatis-config.xml](../SSM-Integration/mybatis-config.md)，这个文件稍后在 Spring 整合 Mybatis 的时候被读取，在创建 sqlSessionFactory 的时候用到
7. 编写 src.java.pojo 中的[实体类](../SSM-Integration/pojoBooks.md)，可能需要使用 lombok 插件
8. 编写 src.java.dao 中的 [mapper接口](../SSM-Integration/daoBookMapper.md)，和 [mapper 对应的 xml](../SSM-Integration/daoBookMapperXML.md)
9. 编写 src.java.service 中的[接口](../SSM-Integration/serviceBookService.md)和[实现类](../SSM-Integration/serviceBookServiceImpl.md)，这里 service 层调 dao 层，是常用思想，这里实现类中的 dao 注入可能找不到 bean，应该检查 web.xml

## Spring 层编写

10. [配置 Spring 整合 Mybatis (Spring-dao.xml)](../SSM-Integration/springDaoXML.md)，就是在 Spring 中注册 Mybatis 需要的几个类，回忆 [Mybatis 配置文件](../SSM-Integration/mybatisConfigXML.md)内容，两个可以进行对比
11. [配置 Spring 整合 Service 层 (Spring-service.xml)](../SSM-Integration/springServiceXML.md)，Service 层有一个业务实现类 BookServiceImpl，实现类中有一个 BookMapper ，在这里的需要注入这个 BookMapper

## SpringMVC 层

12. 编写 [web.xml](../SSM-Integration/webXML.md)，注册 DispatcherServlet

13. 编写 [spring-mvc.xml](../SSM-Integration/webXML.md)，开启注解扫描，默认过滤，自动注册 HandlerMapping 和 HandlerAdapter，视图解析器，（解决 json 返回的乱码问题也在这里）

14. 编写 Spring 配置整合文件 [applicationContext.xml](../SSM-Integration/applicationContext.md)

    ​			

    ​				

    — 配置文件结束 —



遇到的错误：