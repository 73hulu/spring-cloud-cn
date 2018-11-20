[Cloud Native](https://pivotal.io/platform-as-a-service/migrating-to-cloud-native-application-architectures-ebook)是一种应用程序开发风格，鼓励在持续交付和价值驱动开发领域轻松采用最佳实践。一个相关的规程是构建12因素的应用程序，其中开发实践与交付和操作目标保持一致——例如，通过使用声明式编程和管理和监视。Spring Cloud以多种特定方式促进这些开发风格。起点是一组特性，分布式系统中的所有组件都需要方便地访问这些特性。

许多这些特性都由Spring Boot覆盖，Spring Cloud就是在Spring Boot之上构建的。Spring Cloud将更多功能作为两个库提供：Spring Cloud Context和Spring Cloud Commons。Spring Cloud Context为Spring Cloud应用程序的ApplicationContext（引导上下文，加密，刷新范围和环境端点）提供实用程序和特殊服务。Spring Cloud Commons是一组用于不同Spring Cloud实现的抽象和公共类（例如Spring Cloud Netflix和Spring Cloud Consul）。



