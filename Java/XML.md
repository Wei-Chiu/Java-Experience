# XML

### 资源过滤中 filtering 标签的作用

https://my.oschina.net/anxiaole/blog/1613348

```xml
<build>
    <resources>
        <resource>
            <directory>src/main/resources</directory>
            <filtering>true</filtering>
            <includes>
                <include>context.xml</include>
            </includes>
        </resource>

        <resource>
            <directory>src/main/resources</directory>
            <filtering>false</filtering>
            <excludes>
                <exclude>context.xml</exclude>
            </excludes>
        </resource>
    </resources>
</build>
```

配置中一共有两个resource，第一个resource配置是过滤src/main/resources目录下文件context.xml，若文件中有类似${key}这样的配置，就会根据maven的配置进行覆盖，让其**使用真实值来填写**，至于真实值如何来，后面会具体讲。

第二个resource配置是不过滤src/main/resources目录下除了context.xml的其他文件，也就不会用真实值来填写${key}这样的配置。

也许有人会有疑问，若只需要过滤context.xml的话，那就只需要配置第一个resource就可以了吧。其实不然，若是只配置第一个resource，第二个不配置，那么当你运行maven打包操作后，你就会发现，在工程的classpath下只有context.xml文件了，其他配置文件都没有打过来。所以第二个resource是必不可少的，指明其他配置文件是不需要过滤的，但是同样需要打包到classpath下。

其实filtering为true的时候，这时只会把过滤的文件打到classpath下，filtering为false的时候，会把不需要过滤的文件打到classpath下。

还有一点需要说明，若<filtering>、<include>和<exclude>都不配置，就是把directory下的所有配置文件都放到classpath下