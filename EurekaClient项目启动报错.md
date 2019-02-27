问题：EurekaClient项目启动报错
 Invocation of destroy method failed on bean with name 'scopedTarget.eurekaClient': 
 org.springframework.beans.factory.BeanCreationNotAllowedException: Error creating bean with name 'e
 Disconnected from the target VM, address: '127.0.0.1:51233', transport: 'socket'
    

异常报错：

    Invocation of destroy method failed on bean with name 'scopedTarget.eurekaClient': 
    org.springframework.beans.factory.BeanCreationNotAllowedException: 
    Error creating bean with name 'eurekaInstanceConfigBean': 
    Singleton bean creation not allowed while singletons of this factory are in destruction 
    (Do not request a bean from a BeanFactory in a destroy method implementation!)

原因及解决办法： 这是因为client里不包含Tomcat的依赖，所以Spring容器无法创建一些实例，从而导致项目无法启动，
只需在pom.xml文件中，加上web依赖即可：

    <dependency>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-web</artifactId>
    </dependency>