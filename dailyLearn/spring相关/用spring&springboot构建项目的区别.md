# 用spring与springboot构建项目的最初区别

## 启动类区别

### Spring

```java
public class SpringApplication {
    public static void main(String[] args) {
        ApplicationContext cxt = new ClassPathXmlApplicationContext("application.xml");
        Hello hello = (Hello) cxt.getBean("helloworld");
        System.out.println(hello.getName());
    }
}
```

### Springboot

```java
@SpringBootApplication
public class Application {

    public static void main(String[] args) {
        SpringApplication.run(Application.class, args);
    }
}
```

## web

### Spring

```java
一系列，忽略
```

### SpringBoot

```java

@RestController
public class HelloController {
    @RequestMapping("/")
    public String hello() {
        return "Hello World";
    }
}
```

## 配置

### Spring

```java
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xsi:schemaLocation="http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd">


    <bean id="helloworld" class="com.example.demo.leetcode.Hello">
        <property name="name" value="Spring"></property>
    </bean>

</beans>

```

### Springboot

不需要