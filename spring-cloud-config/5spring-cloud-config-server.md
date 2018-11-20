Spring Cloud Config Server为外部配置（名称 - 值对或等效的YAML内容）提供基于HTTP资源的API。通过使用`@EnableConfigServer`注解，服务端可嵌入Spring Boot应用程序中。因此，以下应用程序是config server配置：

**ConfigServer.java.**

```
@SpringBootApplication
@EnableConfigServer
public class ConfigServer {
  public static void main(String[] args) {
    SpringApplication.run(ConfigServer.class, args);
  }
}
```

与所有Spring Boot应用程序一样，它默认在端口8080上运行，但您可以通过各种方式将其切换到更传统的端口8888。最简单的方法是设置默认配置存储库，方法是使用spring.config.name = configserver启动它（Config Server jar中有一个configserver.yml）。另一种方法是使用您自己的application.properties，如以下示例所示：

**application.properties. **

```
server.port: 8888
spring.cloud.config.server.git.uri: file://${user.home}/config-repo
```

其中$ {user.home} / config-repo是一个包含YAML和属性文件的git存储库。

> 在Windows上，如果文件URL是绝对的驱动器前缀，则需要额外的“/”（例如，file：/// $ {user.home} / config-repo）。

> 以下清单显示了在前面的示例中创建git存储库的方法：
>
> ```
> $ cd $HOME
> $ mkdir config-repo
> $ cd config-repo
> $ git init .
> $ echo info.foo: bar > application.properties
> $ git add -A .
> $ git commit -m "Add application.properties"
> ```



