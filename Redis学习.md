# Redis学习

## 1.概述

c语言是编写底层的

java是应用层

Redis的底层使用C语言编写的，是基于内存进行存储的，支持 key-value 的存储形式。

java 通过中间件调用

基于key-value 形式的数据字典，结构非常简单，没有数据表的概念，直接用键值对的形式完成数据的管理，Redis支持5种数据类型：

- 字符串
- 列表 类似List
- 集合 类似Set
- 有序集合 类似有序Set
- 哈希 类似hashmap 外面加个key

{

​    key:value

​    key:{

​        	key:value

​            }

}

读写速度快，操作起来非常简单。

## 2.安装Redis

1.下载Redis redis.io

2.解压，并在本地硬盘任意位置新建一个redis文件夹

里面包含

- bin （放置启动Redis的可执行文件）启动文件  redis-cli  redis-server
- db  （放置数据文件）dump.rdb
- etc  （放置配置文件爱你，设置Redis服务的端口、日志文件位置、数据文件位置）redis.conf其中日志存放位置就关联到下面的文件了
- 和一个log-redis.log文件 

## 3.启动Redis服务

1.进入Redis目录（自己新建的文件）

2.输入命令：

**启动：**

sudo ./bin/redis-server ./etc/redis.conf 启动redis-sercer

./bin/redis-cli 启动redis-cli

**对数据进行操作：**

set key name myredis 设置键值对

get name 获取值根据键

set name java 覆盖

get name 重新获取

keys * 查询key值

keys na* 模糊查询key键

shutdown 退出server

ctrl c 退出cli

---

**在window下如何操作：**

首先下载压缩包，解压至目录Redis[版本号]，进入这个目录

redis-server.exe redis.windows.conf

redis-cli.exe -h 127.0.0.1 -p 6379

## 4.SpringBoot 整合Redis

**Spring Data Redis 操作 Redis**

1.创建一个maven工程

2.pom.xml

- spring-boot-starter-data-redis

- commons-pool2

- lombok

- spring-boot-starter-web web  其实是springMVC，暂时这样理解

3.创建实例类

**impl Serializable 实现序列化接口**，不实现，无法存入redis

将一个对象存起来，就要实现序列化接口

4.创建控制器

@RequestBody 将json对象转化为java对象

注入private RedisTemplate redisTemplate

```java
redisTemplate.opsForValue.set("student",student);
```

开箱即用

5.创建配置文件application.yml

```yaml
spring:
    redis:
        database: 0
        host: localhost
        port: 6379
```

5.启动springboot启动类

@SpringbootApplication

get student

(nil) 空的意思，这个时候取不出来值是因为用springboot操作的时候，redis在key前加了前缀，所以不能按原来的key值取出来

keys *student

存的时候序列化，取的时候，反序列化

```
(强转类型)redisTemplate.opsForValue.get(key);
```

删除

```
redisTemplate.delete(key);
redisTemplate.hasKey(key);//false表示成功，因为已经把key删除掉了
```

## 5.Redis五种数据类型

**字符串**

```java
redisTemplate.opsForValue.set(key,value)
(String)redisTemplate.opsFoeValue.get(key)
```

字符串和对象都用value

**列表**

```java
List<String>
ListOperations<String,String> a = redisTemplate.opsForList();
//像一个管道，可以从左边加，也可以从右边加
a.leftPush("list","value1");
a.leftPush("list","value2");
a.leftPush("list","value3");
//这三个的key是一样的
List<String> b = a.range("list",0,2);
//0和2是截取的下标，截取0到2，所以这是全部三个都取出来
```

**集合**

```java
Set<String>
SetOperationsredis<String,String> a = redisTemplate.opsForSet();
a.add("set","value1");
a.add("set","value1");
a.add("set","value2");
a.add("set","value2");
a.add("set","value3");
a.add("set","value3");
//存了6个，两两重复
Set<String> b = a.members("set");
//重复的东西不会存进去，只会取出来三个值
```

**有序集合**

```java
Set<String>
ZSetOperationsredis<String,String> a = redisTemplate.opsForZSet();
a.add("zset","value1",1);
a.add("zset","value2",2);
a.add("zset","value3",3);
//后面的序号，根据此排序
Set<String> b = a.range("zset",0,2);
```

**哈希**

```java
//HashMap key value
//HashOperations key hashkey value 
//key是每一组数据的id 
//hashkey和value是一组完整的HashMap数据，通过key来区分不同的HashMap
HashMap hashMap1 = new HashMap();
hashMap1.pur(key1,value1);
HashMap hashMap2 = new HashMap();
hashMap2.pur(key2,value2);
HashMap hashMap3 = new HashMap();
hashMap3.pur(key3,value3);
HashOperations<String，String,String> a = redisTemplate.opsForHash();
a.put(hashMap1,key1,value1);
a.put(hashMap2,key2,value2);
a.put(hashMap3,key3,value3);
a.get(key,hashkey);
//取的时候用两个key
```