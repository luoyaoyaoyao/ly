# IoC && Beans

IoC从字面上来看，Inversion of Control, 也被称作Dependency Injection. 与传统依赖来说，IoC实现了控制的反转，对象在被创建的时候，由一个调度系统将其需要的依赖注入进去，简而言之，上层控制底层。  

最基本的spring IoC容器spring-context 下有 spring-aop, spring-beans, spring-core, spring-expression

```java
<dependencies>
        <dependency>
            <groupId>org.springframework</groupId>
            <artifactId>spring-context</artifactId>
            <version>5.1.14.RELEASE</version>
        </dependency>
    </dependencies>
```

BeanFactory: 接口，为Bean提供配置机制
ApplicationContext: IoC容器，并负责初始化。BeanFactory的派生接口。并提供以下优点：

集成了：ListableBeanFactory<可以获取多个bean>; HierarchicalBeanFactory<多个beanFactory>; AutowireCapableBeanFactory<可自动装配bean>

1. 更容易与AOP集成

2. 资源访问

3. 事件传播

实例一个ApplicationContext：

```java
public static void main(String args[]) {
    ApplicationContext applicationContext = new ClassPathApplicationContext("application.xml");
}
```

实现一个Demo

```java
public class Person {
    public String getName () {
        return "LY";
    }
}
```

```java
<?xml version="1.0" encoding="UTF-8" ?>
<beans xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xmlns="http://www.springframework.org/schema/beans"
       xsi:schemaLocation="http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd" default-autowire="byName">

    <bean id="person" class="com.ly.concurrency.demo.Person"/>
</beans>
```

```java
public class Application {
    public static void main(String[] args) {
        ApplicationContext applicationContext = new ClassPathXmlApplicationContext("application.xml");
        System.out.println("Initialization success");
        Person person = applicationContext.getBean(Person.class);
        System.out.println(person.getName());
    }
}
```

打印结果：  
Initialization success  
LY

## BeanFactory

了解一下IoC容器的启动过程

```java

```

## IoC主要实现策略

### 依赖注入 (Dependency Injection)

优点：代码更为简洁，进一步解耦（能够更好的管理依赖），减少内存消耗（不需要重复创建对象）

### 模板设计模式

### 策略模式

1. 构造器注入

2. 参数注入

3. Setter注入

4. 接口注入

## IoC职责

1. 解耦执行到实现

2. 专注设计的模块

3. 不需要关心依赖的模块怎么实现的

## IoC实现

Java SE

* Java Beans

* Java ServiceLoader SPI

* JNDI

## 传统IoC容器的实现



## 轻量级IoC容器

## 构造器注入 VS Setter注入

