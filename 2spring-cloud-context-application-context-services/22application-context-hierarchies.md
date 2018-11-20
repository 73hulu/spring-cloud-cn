如果从SpringApplication或SpringApplicationBuilder构建应用程序上下文，则会将Bootstrap context 添加为该上下文的父级。

Spring的一个特性是，子上下文从父上下文继承属性源和概要文件，因此“主”应用程序上下文包含额外的属性源，而不是在没有Spring Cloud Config的情况下构建相同的上下文。其他属性来源如下:

* “bootstrap”：如果在Bootstrap上下文中找到任何PropertySourceLocators，并且它们具有非空属性，则会出现具有高优先级的可选CompositePropertySource。一个例子是来自Spring Cloud Config Server的属性。 有关如何自定义此属性源内容的说明，请参见“第2.6节”“自定义Bootstrap属性源”[“Section 2.6, “Customizing the Bootstrap Property Sources””](https://cloud.spring.io/spring-cloud-static/Finchley.SR2/multi/multi__spring_cloud_context_application_context_services.html#customizing-bootstrap-property-sources)。

* “applicationConfig: \[classpath:bootstrap.yml\]”（如果Spring配置文件有效，则显示相关文件）：如果您有bootstrap.yml（或.properties），则这些属性用于配置Bootstrap上下文。然后，在设置其父级时，它们将添加到子上下文中。它们的优先级低于application.yml（或.properties）以及作为创建Spring Boot应用程序的正常部分添加到子级的任何其他属性源。有关如何自定义这些属性源的内容的说明，请参见“2.3节”，“更改Bootstrap属性的位置”  [“Section 2.3, “Changing the Location of Bootstrap Properties”” ](https://cloud.spring.io/spring-cloud-static/Finchley.SR2/multi/multi__spring_cloud_context_application_context_services.html#customizing-bootstrap-properties)。

由于属性源的排序规则，“bootstrap”条目优先。但请注意，这些条目不包含来自bootstrap.yml的任何数据，它具有非常低的优先级，但可用于设置默认值。



