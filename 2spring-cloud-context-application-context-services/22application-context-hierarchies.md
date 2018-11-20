如果从SpringApplication或SpringApplicationBuilder构建应用程序上下文，则会将Bootstrap context 添加为该上下文的父级。

Spring的一个特性是，子上下文从父上下文继承属性源和概要文件，所以main application context 相对于没有使用Spring Cloud Config，会新增额外的property sources。额外的property sources有：

* “bootstrap”：如果在Bootstrap上下文中找到任何PropertySourceLocators，并且它们具有非空属性，则会出现具有高优先级的可选CompositePropertySource。一个例子是来自Spring Cloud Config Server的属性。 有关如何自定义此属性源内容的说明，请参见“第2.6节”“自定义Bootstrap属性源”[“Section 2.6, “Customizing the Bootstrap Property Sources””](https://cloud.spring.io/spring-cloud-static/Finchley.SR2/multi/multi__spring_cloud_context_application_context_services.html#customizing-bootstrap-property-sources)。

* “applicationConfig: \[classpath:bootstrap.yml\]”（如果有spring.profiles.active=production则例如 applicationConfig: \[classpath:/bootstrap.yml\]\#production）：如果您有bootstrap.yml（或.properties），则这些属性用于配置Bootstrap上下文。然后，在设置其父级时，它们将添加到子上下文中。~~它们的优先级低于application.ym~~l（或.properties）以及作为创建Spring Boot应用程序的正常部分添加到子级的任何其他属性源。有关如何自定义这些属性源的内容的说明，请参见“2.3节”，“更改Bootstrap属性的位置”  [“Section 2.3, “Changing the Location of Bootstrap Properties”” ](https://cloud.spring.io/spring-cloud-static/Finchley.SR2/multi/multi__spring_cloud_context_application_context_services.html#customizing-bootstrap-properties)。

由于属性源的排序规则，“bootstrap”条目优先。但请注意，这些条目不包含来自bootstrap.yml的任何数据，它具有非常低的优先级，但可用于设置默认值。

您可以通过设置您创建的任何`ApplicationContext`的父上下文来扩展上下文层次结构----例如，通过使用它自己的接口或使用SpringApplicationBuilder便利方法\(`parent()`、`child()`和`sibling()`\)。bootstrap context是您自己创建的最高级祖先的父级。层次结构中的每个上下文都有自己的“bootstrap”（可能是空的）属性源，以避免无意中将父级的值提升到其后代。如果有Config Server，层次结构中的每个上下文也可以（原则上）具有不同的spring.application.name，因此也可以使用不同的远程属性源。普通Spring应用程序上下文行为规则适用于属性解析：来自子上下文的属性会根据名称和属性源名重写父上下文中的属性。\(如果子节点具有与父节点同名的属性源，则来自父节点的值不包含在子节点中\)。

