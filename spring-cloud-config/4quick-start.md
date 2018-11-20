快速入门使用Spring Cloud Config Server的服务端和客户端。

首先，启动服务端，如下所示：

```
$ cd spring-cloud-config-server
$ ../mvnw spring-boot:run
```

服务端是Spring Boot应用程序，因此如果您愿意，可以从IDE运行它（主类是ConfigServerApplication）。

接下来尝试一个客户端，如下所示：

```
$ curl localhost:8888/foo/development
{"name":"foo","label":"master","propertySources":[
  {"name":"https://github.com/scratches/config-repo/foo-development.properties","source":{"bar":"spam"}},
  {"name":"https://github.com/scratches/config-repo/foo.properties","source":{"foo":"bar"}}
]}
```

定位属性源的默认策略是克隆git存储库（在spring.cloud.config.server.git.uri）并使用它来初始化一个迷你SpringApplication。mini-application’s Environment环境用于枚举属性源并在JSON端点发布它们。

HTTP服务具有以下形式的资源：

```
/{application}/{profile}[/{label}]
/{application}-{profile}.yml
/{label}/{application}-{profile}.yml
/{application}-{profile}.properties
/{label}/{application}-{profile}.properties
```

其中`application`作为`SpringApplication`中的spring.config.name注入（通常是常规Spring Boot应用程序中的`application`），`profile`是一个活动的配置文件（或以逗号分隔的属性列表），`label`是一个可选的git标签（ 默认为master。）

Spring Cloud Config Server从git存储库\(必须提供\)提取远程客户端的配置，如下例所示:

```
spring:
  cloud:
    config:
      server:
        git:
          uri: https://github.com/spring-cloud-samples/config-repo
```



