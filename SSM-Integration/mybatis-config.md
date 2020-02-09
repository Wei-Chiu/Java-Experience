# mybatis-config.xml

``` xml
<?xml version="1.0" encoding="UTF-8" ?>
<!DOCTYPE configuration
        PUBLIC "-//mybatis.org//DTD Config 3.0//EN"
        "http://mybatis.org/dtd/mybatis-3-config.dtd">
<configuration>
    
    <typeAliases>
        <package name="com.kuang.pojo"/>
    </typeAliases>
  
    <!-- 这个 mappers 配置可以放到创建了 mapper 接口和对应的 mapper.xml 文件之后，再来进行关联 -->
    <mappers>
        <mapper resource="com/kuang/dao/BookMapper.xml"/>
    </mappers>

</configuration>
```

