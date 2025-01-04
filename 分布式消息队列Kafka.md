# 分布式消息队列Kafka

## 1.总览

概念：

Kafka 是一个分布式消息队列，用于在不同的应用组件或者微服务之间传递消息。它的主要功能是解耦消息的生产者和消费者，实现异步通信。

## 2.下载安装

下载 zookeeper

在目录下新建一个data文件夹
然后修改配置文件zoo.cfg
`dataDir=D:\apache-zookeeper-3.8.4\data`

下载 kafka

在目录下新建一个logs文件夹

然后修改配置文件server.properties

`log.dirs=D:\apache-kafka-3.9.0\logs`



zookeeper
在windows系统上，可以在去bin目录下，执行两个文件。
第一个文件，服务器，zkServer.cmd
第二个文件，客户端，zkCli.cmd
然后，便可以在客户端下执行一些命令
`ls /`  查看node
`create /first-node`  创建node
`delete /first-node`  删除node
`set /first-node "hello zookeeper"`  set
`get /first-node`  get



kafka
在windows系统上，去bin目录，去windows目录下去执行文件

```
kafka-server-start.bat ..\..\config\server.properties
```

**创建测试主题topic：**

```
kafka-topics.bat --create --topic testTopic --bootstrap-server localhost:9092 --partitions 1 --replication-factor 1
```

```
kafka-topics.bat --list --bootstrap-server localhost:9092
```

> 命令解释：

`--create`：明确执行创建主题的操作。
`--topic`：指定要创建的主题名称，这里是`testTopic`。
`--bootstrap-servers`：告知 Kafka 客户端连接的 Kafka 服务器地址与端口，这里用本地服务`localhost:9092` 。
`--partitions`：主题分区数量设为 1。
`--replication-factor`：主题副本数量设为 1。

若创建成功，命令行输出会显示`Created topic testTopic`。

**发送消息：**

```
kafka-console-producer.bat --topic testTopic --bootstrap-server localhost:9092
```

此时，命令行光标会闪烁等待输入，输入任意文本消息，按回车键即可发送消息到`testTopic`主题。

**接收消息：**

```
kafka-console-consumer.bat --topic testTopic --bootstrap-server localhost:9092 --from-beginning
```

其中`--from-beginning`参数确保消费者从主题起始处开始接收消息，稍等片刻，之前在生产者窗口发送的消息就会逐一显示在这个窗口中，说明 Kafka 的消息收发功能正常。

## 3.SpringBoot集成kafka

**新建module，pom.xml**

```xml
    <dependencies>
        <dependency>
            <groupId>org.springframework.kafka</groupId>
            <artifactId>spring-kafka</artifactId>
            <version>2.8.11</version>
        </dependency>
        <dependency>
            <groupId>org.springframework.cloud</groupId>
            <artifactId>spring-cloud-starter-netflix-eureka-client</artifactId>
            <version>3.0.3</version>
        </dependency>
        <!-- spring boot web -->
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-web</artifactId>
            <version>${spring-boot-starter-web.version}</version>
            <scope>compile</scope>
        </dependency>
    </dependencies>
```

**新建application.yml**

```yaml
server:
  port: 8010
spring:
  application:
    name: kafka #微服务的名字 提供者
  kafka:
    bootstrap-servers: localhost:9092
eureka:
  client:
    service-url:
      defaultZone: http://localhost:8761/eureka/
  instance:
    prefer-ip-address: true
```

**创建kafka生产者：**

```java
@Component
public class KafkaProducer {

    private final KafkaTemplate<String, String> kafkaTemplate;

    public KafkaProducer(KafkaTemplate<String, String> kafkaTemplate) {
        this.kafkaTemplate = kafkaTemplate;
    }

    public void sendMessage(String topic, String message) {
        kafkaTemplate.send(topic, message);
    }
}
```

**创建kafka消费者：**

```java
@Component
public class KafkaConsumer {

    @KafkaListener(topics = "helloKafka", groupId = "testKafka")
    public void receiveMessage(ConsumerRecord<String, String> record) {
        System.out.println("kafka消费者收到的信息: " + record.value() +
                "来自的partition: " + record.partition());
    }

}
```

**创建启动类：**

```java
@SpringBootApplication
public class KafkaApplication {

    public static void main(String[] args) {
        ConfigurableApplicationContext context = SpringApplication.run(KafkaApplication.class, args);
        KafkaProducer producer = context.getBean(KafkaProducer.class);
        producer.sendMessage("helloKafka", "Hello, Kafka!");
    }

}
```

