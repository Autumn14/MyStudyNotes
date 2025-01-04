# SpringCloud全家桶学习

## 1.概述

单体应用存在的问题：

- 随着业务的发展，开发变得越来越复杂。
- 修改、新增某个功能，需要对整个系统进行测试、重新部署。
- 一个模块出现问题，很可能导致整个系统崩溃。
- 多个开发团队同事对数据进行管理，容易产生安全漏洞。
- 各个模块使用同一种技术进行开发，各个模块很难根据实际情况选择适合的技术框架，局限性很大。
- 模块内同过于复杂，如果员工离职，可能需要很长时间才能完成交接工作。

分布式、集群

集群：一台服务器无法负荷高并发的数据访问量，那么就设置十台服务器一起分担，十台不行就设置一百台（物理层面）。很多人干同一件事，来分摊压力。

分布式：将一个复杂问题拆分成若干个简单的小问题，将一个大型的项目架构拆分成若干个微服务来协同完成（软件设计层面）。将一个庞大的工作拆分成若干个小步骤，分别由不同的人完成这些小步骤，最终将所有的结果进行整合实现大的需求。

负载，处理高并发。

网关，请求统一的入口。

沟通成本，数据一致性。

SpringCloud完全基于SpringBoot，服务调用的方式也是基于REST API。

Eureka、Feign、Ribbon、Zuul、Hystrix

服务治理：Eureka

服务通信：Ribbon

服务通信：Feign

服务网关：Zuul

服务容错：Hystrix

服务配置：Config

服务监控：Actuator

服务跟踪：Zipkin

**服务治理：**

服务治理的核心有三部分组成：服务提供者、服务消费者、注册中心

在分布式系统架构中，每个微服务启动时，将自己的信息存储在注册中心，叫做服务注册。

服务消费者从注册中心获取服务提供者的网络信息，通过该信息调用服务，叫做服务发现。

Spring Cloud 的服务治理使用 Eureka 来实现，Eureka 是 Netflix 开源的基于REST的服务治理解决方案，Spring Cloud集成了Eureka，提供服务注册和服务发现的功能，可以和基于Spring Boot搭建的微服务应用轻松完成整合，开箱即用，Spring Cloud Eureka。

## 2.Spring Cloud Eureka

- Eureka Server ，注册中心
- Eureka Client ，所有要进行注册的微服务通过Eureka Client连接到 Eureka Server，完成注册。

### Eureka Server代码实现：

这里springboot的版本是2.0.7，实际按照你的项目去找对应的spring cloud版本。

2021.0.9

**创建父工程：**

```xml
<dependencyManagement>
    <dependencies>
        <dependency>
            <groupId>org.springframework.cloud</groupId>
            <artifactId>spring-cloud-dependencies</artifactId>
            <version>Finchley.SR2</version>
            <type>pom</type>
            <scope>import</scope>
        </dependency>
    </dependencies>
</dependencyManagement>
```

**在父工程下创建Module，pom.xml：**

注册中心：

```xml
<dependencies>
    <dependency>
        <groupId>org.springframework.cloud</groupId>
        <artifactId>spring-cloud-starter-netflix-eureka-server</artifactId>
        <version>2.0.2.RELEASE</version>
    </dependency>
</dependencies>
```

**创建配置文件Application.yml，添加 Eureka Server 相关配置：**

Module下：

```yaml
server:
    port: 8761
eureka:
    client:
        register-with-eureka: false #是否注册自己，因为是注册中心，所以只注册别人，不注册自己
        fetch-registry: false #是否要同步其它注册中心的树
        service-url: 
            defaultZone: http://localhost:8761/eureka/
```

> 属性说明

`server.port`：当前 Eureka Server 服务端口。

`eureka.client.register-with-eureka`：是否将当前的 Eureka Server 服务作为客户端进行注册。

`eureka.client.fetch-fegistry`：是否获取其他 Eureka Server 服务的数据。

`eureka.client.service-url.defaultZone`：注册中心的访问地址。

**创建启动类**

@SpringBootApplication

声明该类是Spring Boot服务的入口

@EnableEurekaServer

声明该类是一个Eureka Server微服务，提供服务注册和服务发现功能，即注册中心。

```xml
<dependencies>
    <!-- 解决 JDK9 以上没有 JAXB API的问题 -->
    <dependency>
        <groupId>javax.xml.bind</groupId>
        <artifactId>jaxb-api</artifactId>
        <version>2.3.0</version>
    </dependency>

    <dependency>
        <groupId>com.sun.xml.bind</groupId>
        <artifactId>jaxb-impl</artifactId>
        <version>2.3.0</version>
    </dependency>

    <dependency>
        <groupId>com.sun.xml.bind</groupId>
        <artifactId>jaxb-core</artifactId>
        <version>2.3.0</version>
    </dependency>

    <dependency>
        <groupId>javax.activation</groupId>
        <artifactId>activation</artifactId>
        <version>1.1.1</version>
    </dependency>
</dependencies>
```

**http://localhost:8761**

去验证

### Eureka Client代码实现：

**在父工程下创建Module，pom.xml：**

```xml
<dependencies>
    <dependency>
        <groupId>org.springframework.cloud</groupId>
        <artifactId>spring-cloud-starter-netflix-eureka-client</artifactId>
        <version>2.0.2.RELEASE</version>
    </dependency>
</dependencies>
```

**创建配置文件 application.xml ，添加 Eureka Client 相关配置：**

```yaml
server:
    port: 8010
spring:
    application:
        name: provider #微服务的名字 提供者
eureka:
    client:
        service-url:
            defaultZone: http://localhost:8761/eureka/
    instance:
        prefer-ip-address: true
```

> 属性说明

`spring.application.name`： 当前服务注册在 Eureka Server 上的名称。

`eureka.client.service-url.defaultZone`： 注册中心的访问地址。

`eureka.instance.prefer-ip-address:`： 是否将当前服务的 IP 注册到 Eureka Server。

**创建启动类：**

@SpringBootApplication

只加这个注解就可以了

首先启动注册中心，然后启动服务提供者

启动多个微服务

## 3.RestTemplate 的使用

概念：

Rest Template 是 Spring 框架提供的基于REST的服务组件，底层是对HTTP请求及响应进行了封装，提供了很多访问 REST 服务的方法，可以简化代码开发。

使用：

**创建maven工程，在pom.xml中引入相关依赖**

有springboot就可以调用

启动类：

```java
@SpringBootApplication
public class RestTemplateAllpication {
    public static void main(String[] args){
        SpringApplication.run(RestTemplateAllpication.class, args);
    }

    @Bean
    public RestTemplate resTemplate(){
        return new RestTemplate();
    }  
}
```

调用：

```java
//get
restTemplate.getForEntity(url路径,结果集的类.class).getBody();
restTemplate.getForObject(url路径,结果集的类.class);
//参数
restTemplate.getForEntity(url路径/{id},结果集的类型,id).getBody();
restTemplate.getForObject(url路径/{id},结果集的类型,id)
//post
restTemplate.postForEntity(url路径,传参,返回值).getBody();
restTemplate.postForObject(url路径,传参,返回值);
//put
restTemplate.put(url路径,传参);
//delete
restTemplate.delete((url路径/{id},id);
```

## 4.服务消费者consumer

**创建maven工程，在pom.xml中引入相关依赖**

```xml
<dependencies>
    <dependency>
        <groupId>org.springframework.cloud</groupId>
        <artifactId>spring-cloud-starter-netflix-eureka-client</artifactId>
        <version>2.0.2.RELEASE</version>
    </dependency>
</dependencies>
```

**创建配置文件application.yml**

```yaml
server:
    port: 8020
spring:
    application:
        name: consumer #微服务的名字 消费者
eureka:
    client:
        service-url:
            defaultZone: http://localhost:8761/eureka/ #注册中心的访问地址
    instence:
        prefer-ip-address: true
```

**创建启动类**

@SpringBootApplication

**启动类注入restTemplate**

```java
@Bean
public RestTemplate resTemplate(){
    return new RestTemplate();
} 
```

**在controller使用restTemplate调用提供者**

启动注册中心

启动服务提供者

启动服务消费者

## 5.服务网关

管理请求

Zuul

Spring Cloud 集成了 Zuul 组件，实现服务网关。

概念：

Zuul 是 Netflix 提供的一个开源的 API 网关服务器，是客户端和网站后端所有请求的中间层，对外开发一个API，将所有请求导入统一的入口，屏蔽了服务器的具体实现逻辑，Zuul可以实现反向代理的功能，在网关内部实现动态路由、身份验证、IP过滤、数据监控等。

**创建maven工程，在pom.xml中引入相关依赖**

先要引入Eureka Client 

```xml
<dependencies>
    <dependency>
        <groupId>org.springframework.cloud</groupId>
        <artifactId>spring-cloud-starter-netflix-eureka-client</artifactId>
        <version>2.0.2.RELEASE</version>
    </dependency>
    <dependency>
        <groupId>org.springframework.cloud</groupId>
        <artifactId>spring-cloud-starter-netflix-zuul</artifactId>
        <version>2.0.2.RELEASE</version>
    </dependency>
</dependencies>
```

**创建配置文件application.yml**

```yaml
server:
    port: 8030
spring:
    application:
        name: gateway #微服务的名字 网关
eureka:
    client:
        service-url:
            defaultZone: http://localhost:8761/eureka/ #注册中心的访问地址
zuul:
    routes: 
        provider: /p/** #提供者的别名        
```

> 属性说明：

`zuul.routes.provider`： 给服务者provider设置映射

**创建启动类**

@EnableZuulProxy：包含了`@EnableZuulServer`，设置该类是网关的启动类。

@EnableAutoConfiguration：可以帮助Spring Boot应用将所有符合条件的`@Configuration`配置加在到当前Spring Boot创建并使用的IOC容器中。

不加@SpringBootApplication

先启动注册中心

启动服务提供者

启动网关，不启动消费者

`localhost:8030/p/student/findAll`这是一个示例

服务通过网关去调用

**Zuul自带了负载均衡的作用**

修改provider代码

```java
@Value("$server.port")
private String port;

@GetMapping("index")
public String index(){
    return "当前端口：" + this.port;
}
```

先启动注册中心

再启动provider，第一个。

再启动provider，第二个，（再写一个启动类，提前修改配置文件的端口。）

再启动网关。

这时候通过网关去访问index接口，会返回8011（第二个provider实例的端口），再访问则会返回8010（第一个）。

两个服务交替帮我们返回。

## 6.Ribbon 负载均衡

概念：

Spring Cloud Ribbon 是一个负载均衡解决方案，Ribbon 是 Netflix 发布的负载均衡器，Spring Cloud Ribbon 基于 Netflix Ribbon 实现的，是一个用于对 HTTP 请求进行控制的负载均衡客户端。

在注册中心对 Ribbon 进行注册之后，Ribbon 就可以基于某种负载均衡算法，如轮询、随机、加权轮询、加权随机等自动帮助服务消费者调用接口，开发者也可以根据某种需求自定义 Ribbon 负载均衡算法。实际开发中，Spring Cloud Ribbon 需要结合 Spring Cloud Eureka 来使用，Eureka Server 提供所有可以调用的服务提供者列表，Ribbon 基于特定的负载均衡算法从这些服务提供者中选择要调用的具体实例。

**创建 Module，pom.xml**

```xml
<dependencies>
    <dependency>
        <groupId>org.springframework.cloud</groupId>
        <artifactId>spring-cloud-starter-netflix-eureka-client</artifactId>
        <version>2.0.2.RELEASE</version>
    </dependency>
</dependencies>
```

**创建配置文件application.xml**

```yaml
server:
    port: 8030
spring:
    application:
        name: ribbon
eureka:
    client:
        service-url:
            defaultZone: http://localhost:8761/eureka/ #注册中心的访问地址
    instance:
        prefer-ip-address: true
```

**创建启动类**

@SpringbBootApplication

```java
@Bean
@LoadBalanced
public RestTemplate restTemplate(){
    return new RestTemplate();
}
```

`@LoadBalanced`：声明一个基于 Ribbon 的负载均衡。

Controller调用

```java
restTemplate.getForObject("htttp://provider/student/findAll",Collection.class)
restTemplate.getForObject("htttp://provider/student/index",String.class)
```

先启动注册中心

再启动两个服务提供者

在启动 Ribbon

再调用 Ribbon 去访问服务提供者 

## 7.Feign

概念：

与 Ribbon 一样， Feign 也是有 Netflix 提供的，Feign 是一个声明式、模板化的Web Service客户端，它简化了开发者编写Web服务客户端的操作，开发者可以通过简单的接口和注解来调用 HTTP API，Spring Cloud Feign，它整合了Ribbon 和 Hystrix，具有可插拔、基于注解、负载均衡、服务熔断等一系列便捷功能。

相比较 Ribbon  + RestTemplate 的方式，Feign 大大简化了代码的开发，Feign 支持多种注解，包含 Feign 注解、JAX-RS 注解、Spring MVC 注解等，Spring Cloud对Feign进行了优化，整合了 Ribbon 和 Eureka，从而让 Feign 的使用更加方便。

**Ribbon 和 Feign 的区别**

Ribbon 是一个通用的 HTTP 客户端工具，Feign 是基于 Ribbon 实现的。

**Feign的特点**

1、Feign是一个声明式的 Web Service 客户端。

2、支持 Feign 注解、SpringMVC注解、JAX-RS 注解。

3、Feign 基于 Ribbon 实现，使用起来更加简单。

4、Feign 集成了 Hystrix ，具备服务熔断的功能。

**实现如下：**

**创建 Module ， pom.xml**

```xml
<dependencies>
    <dependency>
        <groupId>org.springframework.cloud</groupId>
        <artifactId>spring-cloud-starter-netflix-eureka-client</artifactId>
        <version>2.0.2.RELEASE</version>
    </dependency>
    <dependency>
        <groupId>org.springframework.cloud</groupId>
        <artifactId>spring-cloud-starter-openfeign</artifactId>
        <version>2.0.2.RELEASE</version>
    </dependency>
</dependencies>
```

**创建配置文件application.yml**

```yaml
server:
    port: 8050
spring:
    application:
        name: feign
eureka:
    client:
        service-url:
            defaultZone: http://localhost:8761/eureka/ #注册中心的访问地址
    instance:
        prefer-ip-address: true
```

**创建启动类**

```java
@SpringBootApplication
@EnableFeignClients
public class FeignApplication{
    public static void main(String[] args){
        SpringAppplication.run(FeignApplication.calss,args);
    }
}
```

**创建FeignProviderClient接口（创建声明式接口）**

新建一个feign文件夹，将接口放在文件夹下面。

```java
@FeignClient(value = "provider")
public interface FeignProviderClient{
    @GetMapping("/student/findAll")
    public Collection<Student> findAll();

    @GetMapping("/student/index")
    public String index();
}
```

provider这个value的值是服务提供者在注册中心的映射

**创建Controller**

```java
@RestContrller
@RequestMapping("/feign")
public class FeignHandler{
    @AutoWired
    private FeignProviderClient feignProviderClient;

    @GetMapping("/findAll")
    public Collection<Student> findAll(){
        return feignProviderClient.findAll();
    }

    @GetMapping("/index")
    public String index(){
        return feignProviderClient.index();
    }
}
```

启动注册中心、服务提供者、Feign

**服务熔断**

一个需求调用多个微服务，如果其中一个出现问题，可能导致业务延迟，甚至崩溃。

当某一个微服务出现问题，通过一种降级处理，或者某些应急处理，使服务不要整体崩溃。

**服务熔断，application.yml添加熔断机制**

```yaml
server:
    port: 8050
spring:
    application:
        name: feign
eureka:
    client:
        service-url:
            defaultZone: http://localhost:8761/eureka/ #注册中心的访问地址
    instance:
        prefer-ip-address: true
feign:
    hystrix:
        enable: true
```

`feign.hystrix.enable`：是否开启熔断器。

**创建 FeignProviderClient 接口的实现类 FeignError，定义容错处理逻辑，通过`@Component`注解将 FeignError 实例注入IoC容器中：**

```java
@Component
public calss FeignError implements FeignProviderClient{
    @Override
    public Collection<Student> findAll(){
        return null;
    }

    @Override
    public String index(){
        return "服务正在维护中……";
    }
}
```

**在FeignProviderClient定义处通过 `FeignClient` 的 fallback 属性设置映射**

```java
@FeignClient(value = "provider" fallback = FeignError.class)
public interface FeignProviderClient{
    @GetMapping("/student/findAll")
    public Collection<Student> findAll();

    @GetMapping("/student/index")
    public String index();
}
```

再次启动注册中心，但不启动服务提供者，用Feign消费者调用服务提供者的时候，由于服务提供者是DOWN，所以触发熔断机制，返回了FeignProviderClient的实现类FeignError中的内容。

## 8.Hystrix 容错机制

在分布式系统中，各个微服务都是相互依赖相互调用的，实际上运行情况，可能由于某种原因导致某一个微服务不可用，那么依赖这个微服务的其他微服务，就可能出现响应时间过长或者请求失败的情况。

 在不改变各个微服务调用关系的前提下，针对错误情况进行预先处理。

设计原则：

- 1、服务隔离机制
- 2、服务降级机制
- 3、熔断机制
- 4、提供实时的监控和报警功能
- 5、提供实时的配置修改功能

Hystrix 数据监控需要结合 Spring Boot Actuator 来使用，Actuator 提供了对服务的健康检查、数据统计，可以通过 hystrix.stream 节点获取监控的请求数据，提供了可视化的监控界面。

**创建 Module ， pom.xml**

```xml
<dependencies>
    <dependency>
        <groupId>org.springframework.cloud</groupId>
        <artifactId>spring-cloud-starter-netflix-eureka-client</artifactId>
        <version>2.0.2.RELEASE</version>
    </dependency>
    <dependency>
        <groupId>org.springframework.cloud</groupId>
        <artifactId>spring-cloud-starter-openfeign</artifactId>
        <version>2.0.2.RELEASE</version>
    </dependency>
    <!-- 健康监控 -->
    <dependency>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-actuator</artifactId>
        <version>2.0.7.RELEASE</version>
    </dependency>
    <!-- hystrix -->
    <dependency>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-cloud-starter-netflix-hystrix</artifactId>
        <version>2.0.2.RELEASE</version>
    </dependency>
    <!-- 可视化的界面 hystrix仪表盘 -->
    <dependency>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-cloud-starter-netflix-hystrix-dashboard</artifactId>
        <version>2.0.2.RELEASE</version>
    </dependency>
</dependencies>
```

**创建配置文件application.yml**

```yaml
server:
    port: 8060
spring:
    application:
        name: hystrix
eureka:
    client:
        service-url:
            defaultZone: http://localhost:8761/eureka/ #注册中心的访问地址
    instance:
        prefer-ip-address: true
feign:
    hystrix:
        enable: true
management:
    endpoints:
        web:
            exposure:
                include: 'hystrix.stream'
```

**创建启动类**

```java
@SpringBootApplication
@EnableFeignClients
@EnableCircuitBreaker
@EnableHystrixDashboard
public class HystrixApplication{
    public static void main(String[] args){
        SpringAppplication.run(HystrixApplication.calss,args);
    }
}
```

> 注解说明

`@EnableCircuitBreaker`：声明启动数据监控

`@EnableHystrixDashboard`： 声明启用可视化的数据监控，hystrix仪表盘

**创建FeignProviderClient接口（创建声明式接口）**

如Feign

**创建Controller**

```java
@RestContrller
@RequestMapping("/hystrix")
public class FeignHandler{
    @AutoWired
    private FeignProviderClient feignProviderClient;

    @GetMapping("/findAll")
    public Collection<Student> findAll(){
        return feignProviderClient.findAll();
    }

    @GetMapping("/index")
    public String index(){
        return feignProviderClient.index();
    }
}
```

下面开始测试：

启动注册中心

再启动服务提供者

再启动hystrix

**localhost://8060/actuator/hystrix.stream**  监控网页

**localhost://8060/hystrix** 可视化页面

## 9.Spring Cloud 配置中心

配置文件统一管理

Spring Cloud Config，通过服务端可以为多个客户端提供配置服务。

Spring Cloud Config 可以将配置文件存储在本地，也可以将配置文件存储在远程的 Git 仓库。

不重启微服务的前提下，修改配置。

创建 Config Server，通过它管理所有的配置文件。

### 本地文件系统

**创建 Module ， pom.xml**

nativeconfigserver

```xml
<dependencies>
    <dependency>
        <groupId>org.springframework.cloud</groupId>
        <artifactId>spring-cloud-config-server</artifactId>
        <version>2.0.2.RELEASE</version>
    </dependency>
</dependencies>
```

**创建配置文件application.yml**

```yaml
server:
    port: 8762
spring:
    application:
        name: nativeconfigserver
    profiles:
        active: native
    cloud:
        config:
            server:
                native:
                    search-locations: classpath:/shared
```

> 属性说明

`profiles.active` ： 配置文件的获取方式

`cloud.config.server.native.search-locations` ： 本地配置文件存放的路径

**在resources目录下创建本地目录shared，然后在目录下创建配置文件configclient-dev.yml**

```yaml
server:
    port: 8070
foo: foo version 1
```

**创建启动类**

```java
@SpringBootApplication
@EnableConfigServer
public class NativeConfigApplication{
    public static void main(String[] args){
        SpringAppplication.run(NativeConfigApplication.calss,args);
    }
}
```

> 注解说明

`@EnableConfigServer` ： 声明配置中心。

**创建客户端读取本地配置中心的配置文件**

**创建 Module ， pom.xml**

nativeconfigclient

```xml
<dependencies>
    <dependency>
        <groupId>org.springframework.cloud</groupId>
        <artifactId>spring-cloud-starter-config</artifactId>
        <version>2.0.2.RELEASE</version>
    </dependency>
</dependencies>
```

读取配置

**创建 bootstrap.yml 配置文件，读取本地配置中心的相关信息**

```yaml
spring:
    application:
        name: configclient
    profiles:
        active: dev
    cloud:
        config:
            uri: http://localhost:8762
            fail-fast: true
```

name 和 active 用横线拼起来

> 属性说明

`cloud.config.uri` ： 配置本地 Config Server 的访问路径。

`cloud.config.uri.fail-fast` ： 设置客户端优先判断 Config Server 获取是否正常。

通过 `spring.application.name` 结合 `spring.profiles.active` 拼接目标配置文件名，configclient-dev.yml，去 Config Server 中查找该文件。

**创建客户端的启动类**

```java
@SpringBootApplication
public class NativeConfigClientApplication{
    public static void main(String[] args){
        SpringAppplication.run(NativeConfigClientApplication.calss,args);
    }
}
```

**测试：创建controller将配置文件的属性输出**

```java
@RestContrller
@RequestMapping("/native")
public class FeignHandler{
    @Value("${server.port}")
    private String port;
    @Value("${server.foo}")
    private String foo;

    @GetMapping("/index")
    public String index(){
        return this.port + "-" + this.foo;
    }
}
```

先启动注册中心

再启动 Config Server

再启动 Config Client

### 远程配置中心

**创建配置文件，上传至 GitHub**

```yaml
server:
    port: 8060
eureka:
    client:
        service-url:
            defaultZone: http://localhost:8761/eureka/ #注册中心的访问地址        
spring:
    application:
        name: configclient
```

**创建 Module ， pom.xml**

```xml
<dependencies>
    <dependency>
        <groupId>org.springframework.cloud</groupId>
        <artifactId>spring-cloud-config-server</artifactId>
        <version>2.0.2.RELEASE</version>
    </dependency>
</dependencies>
```

**创建配置文件application.yml**

```yaml
server:
    port: 8888
spring:
    application:
        name: configserver
    cloud:
        config:
            server:
                git:
                    uri: git地址
                    searchPaths: config
                    username: root
                    password: root
                label: master
eureka:
    client:
        service-url:
            defaultZone: http://localhost:8761/eureka/ #注册中心的访问地址    
```

**创建Config Client**

和本地的一样了

bootstrap.yml

```yaml
spring:
    cloud:
        config:
            name: configclient #git上目录下的文件名
            lable: master #git分支
            discovery:
                enabled: true #是否开启config服务发现支持
                service-id: configserver #配置中心在注册中心的名字
eureka:
    client:
        service-url:
            defaultZone: http://localhost:8761/eureka/ #注册中心的访问地址    
```

> 注解说明：

`spring.cloud.config.name` ： 当前服务注册在Eureka Server上的名称，与远程仓库配置文件名对应。

## 10. 服务跟踪

微服务依赖负载，在查问题的时候，非常复杂

Spring Cloud Zipkin

Zinkin 是一个可以采集并跟踪分布式系统中请求数据的组件，让开发者可以更加直观的监控到请求在各个微服务所消耗的时间等，Zipkin ： Zipkin Server 、Zipkin Clinent。

**使用：**

### 创建客户端 Zipkin Server

**创建 Module ， pom.xml**

```xml
<dependencies>
    <dependency>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-web</artifactId>
    </dependency>
    <dependency>
        <groupId>io.zipkin.java</groupId>
        <artifactId>zipkin-server</artifactId>
        <version>2.9.4</version>
    </dependency>
    <dependency>
        <groupId>io.zipkin.java</groupId>
        <artifactId>zipkin-autoconfigure-ui</artifactId>
        <version>2.9.4</version>
    </dependency>
</dependencies>
```

**创建配置文件application.yml**

```yaml
server:
    port: 9090
```

**创建启动类**

```java
@SpringBootApplication
@EnableZipkinServer
public class ZipkinServerApplication{
    public static void main(String[] args){
        SpringAppplication.run(ZipkinServerApplication.calss,args);
    }
}
```

> 注解说明

`@EnableZipkinServer` ： 声明启动Zipkin Server。

这是服务器就搭建起来了，然后再搭建一个客户端，zipkinclient

### 创建客户端 Zipkin Client

**创建 Module ， pom.xml**

```xml
<dependencies>
    <dependency>
        <groupId>org.springframework.cloud</groupId>
        <artifactId>spring-cloud-starter-zipkin</artifactId>
        <version>2.0.2.RELEASE</version>
    </dependency>
</dependencies>
```

**创建配置文件application.yml**

```yaml
server:
    port: 8090
spring:
    application:
        name: zipkinclient
    sleuth:
        web:
            client:
                enabled: true
        sampler:
            probability: 1.0
    ziplin:
        base-url: http://localhost:9090/
eureka:
    client:
        service-url:
            defaultZone: http://localhost:8761/eureka/ #注册中心的访问地址    
```

> 属性说明

`spring.sleuth.web.client.enabled` : 设置开启请求跟踪

`spring.sleuth.sampler.probability` : 设置采样比例，默认是1.0（在监控数据的时候使用的一个比例）

`spring.zipkin.base-url` : Zipkin Server地址

**创建启动类**

```java
@SpringBootApplication
public class ZipkinClientApplication{
    public static void main(String[] args){
        SpringAppplication.run(ZipkinClientApplication.calss,args);
    }
}
```

**创建Controller**

```java
@RestContrller
@RequestMapping("/zipkin")
public class ZipkinHandler{

    @Value("${server.port}")
    private String port;

    @GetMapping("/index")
    public String index(){
        return this.port;
    }
}
```

测试：

先启动注册中心

再启动 Zipkin Server

再启动 Zipkin Client

访问：

localhost:9090/zipkin/
