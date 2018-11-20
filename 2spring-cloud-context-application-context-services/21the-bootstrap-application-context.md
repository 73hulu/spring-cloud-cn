Spring Cloud应用程序通过创建“bootstrap”上下文来运行，该上下文是主应用程序的父上下文。它负责从外部源加载配置属性以及解密本地外部配置文件中的属性。这两个上下文共享一个`Environment`，它是任何Spring应用程序的外部属性的来源。默认情况下，引导属性bootstrap properties（不是bootstrap.properties，而是在引导阶段加载的属性）以高优先级添加，因此本地配置无法覆盖它们。

 引导上下文bootstrap context使用与主应用程序上下文不同的约定来定位外部配置。您可以使用bootstrap.yml代替application.yml（或.properties），使引导程序和主要上下文的外部配置保持良好分离。以下清单显示了一个示例：

**bootstrap.yml**

```
spring:
  application:
    name: foo
  cloud:
    config:
      uri: ${SPRING_CONFIG_URI:http://localhost:8888}
```

如果您的应用程序需要来自服务端的任何特定于应用程序的配置，则最好设置spring.application.name（在bootstrap.yml或application.yml中）。

您可以通过设置spring.cloud.bootstrap.enabled = false来完全禁用引导过程（例如，在系统属性中）。

