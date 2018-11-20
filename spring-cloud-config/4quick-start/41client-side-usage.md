要在应用程序中使用这些功能，您可以将其构建为依赖于spring-cloud-config-client的Spring Boot应用程序（例如，请参阅config-client或示例应用程序的测试用例）。添加依赖项最方便的方法是使用Spring Boot启动程序`org.springframework.cloud:spring-cloud-starter-config`。Maven用户还拥有一个父pom和BOM \(Spring -cloud-starter-parent\)，以及一个用于Gradle和Spring CLI用户的Spring IO版本管理属性文件。以下示例显示了典型的Maven配置：

**pom.xml. **

```
<parent>
       <groupId>org.springframework.boot</groupId>
       <artifactId>spring-boot-starter-parent</artifactId>
       <version>{spring-boot-docs-version}</version>
       <relativePath /> <!-- lookup parent from repository -->
   </parent>

<dependencyManagement>
	<dependencies>
		<dependency>
			<groupId>org.springframework.cloud</groupId>
			<artifactId>spring-cloud-dependencies</artifactId>
			<version>{spring-cloud-version}</version>
			<type>pom</type>
			<scope>import</scope>
		</dependency>
	</dependencies>
</dependencyManagement>

<dependencies>
	<dependency>
		<groupId>org.springframework.cloud</groupId>
		<artifactId>spring-cloud-starter-config</artifactId>
	</dependency>
	<dependency>
		<groupId>org.springframework.boot</groupId>
		<artifactId>spring-boot-starter-test</artifactId>
		<scope>test</scope>
	</dependency>
</dependencies>

<build>
	<plugins>
           <plugin>
               <groupId>org.springframework.boot</groupId>
               <artifactId>spring-boot-maven-plugin</artifactId>
           </plugin>
	</plugins>
</build>

   <!-- repositories also needed for snapshots and milestones -->
```

现在您可以创建一个标准的Spring Boot应用程序，例如以下HTTP服务端：

```
@SpringBootApplication
@RestController
public class Application {

    @RequestMapping("/")
    public String home() {
        return "Hello World!";
    }

    public static void main(String[] args) {
        SpringApplication.run(Application.class, args);
    }

}
```

当此HTTP服务端运行时，它从端口8888上的默认本地配置服务器（如果它正在运行）中获取外部配置。要修改启动行为，可以使用bootstrap.properties更改配置服务器的位置（类似于application.properties，但适用于应用程序上下文的引导阶段），如以下示例所示：

```
spring.cloud.config.uri: http://myconfigserver.com
```

bootstrap properties在/env端点中作为高优先级属性源显示，如下例所示。

```
$ curl localhost:8080/env
{
  "profiles":[],
  "configService:https://github.com/spring-cloud-samples/config-repo/bar.properties":{"foo":"bar"},
  "servletContextInitParams":{},
  "systemProperties":{...},
  ...
}
```

名为\`\`configService:&lt;URL of remote repository&gt;/&lt;file name&gt;包含foo属性，值为bar，优先级最高。

```
property source属性源名称中的URL是git存储库，而不是config server配置服务器URL。
```



