[Cloud Native](https://pivotal.io/platform-as-a-service/migrating-to-cloud-native-application-architectures-ebook)是一种应用程序开发风格，鼓励在持续交付和价值驱动开发领域轻松采用最佳实践。一个相关的规程是构建12因素的应用程序，其中开发实践与交付和操作目标保持一致——例如，通过使用声明式编程和管理和监视。Spring Cloud以多种特定方式促进这些开发风格。起点是一组特性，分布式系统中的所有组件都需要方便地访问这些特性。

许多这些特性都由Spring Boot覆盖，Spring Cloud就是在Spring Boot之上构建的。Spring Cloud将更多功能作为两个库提供：Spring Cloud Context和Spring Cloud Commons。Spring Cloud Context为Spring Cloud应用程序的ApplicationContext（引导上下文，加密，刷新范围和环境端点）提供实用程序和特殊服务。Spring Cloud Commons是一组用于不同Spring Cloud实现的抽象和公共类（例如Spring Cloud Netflix和Spring Cloud Consul）。

如果由于“非法密钥大小”而导致异常并且您使用Sun的JDK，则需要安装Java Cryptography Extension（JCE）Unlimited Strength Jurisdiction Policy Files。 有关更多信息，请参阅以下链接：

* [Java 6 JCE](http://www.oracle.com/technetwork/java/javase/downloads/jce-6-download-429243.html)
* [Java 7 JCE](http://www.oracle.com/technetwork/java/javase/downloads/jce-7-download-432124.html)
* [Java 8 JCE](http://www.oracle.com/technetwork/java/javase/downloads/jce8-download-2133166.html)

无论您使用哪种版本的JRE / JDK x64 / x86，都要将文件解压缩到JDK / jre / lib / security文件夹中。

> Spring Cloud是在非限制性Apache 2.0许可下发布的。 如果您想为文档的这一部分做出贡献，或者如果发现错误，您可以在[github](https://github.com/spring-cloud/spring-cloud-commons/tree/master/docs/src/main/asciidoc)上找到项目的源代码和问题跟踪器。





