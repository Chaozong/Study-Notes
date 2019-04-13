# SpringCloud简介
>[demo演示地址](https://github.com/spring-cloud-incubator/spring-cloud-alibaba/blob/master/README-zh.md)  
[官方文档](https://github.com/spring-cloud-incubator/spring-cloud-alibaba/blob/master/README-zh.md)
## 一、是什么
springCloud是基于SpringBoot的一整套实现微服务的框架。他提供了微服务开发所需的配置管理、服务发现、断路器、智能路由、微代理、控制总线、全局锁、决策竞选、分布式会话和集群状态管理等组件。
简单来说，springCloud是一个用于**微服务的平台**，提供了各种各样微服务所需的组件

## 二、怎么用
要使用springCloud，需要先理解微服务架构，了解微服务中的事务一致性，可用性等，再学习springCloud中的相关组件。  
如：使用Spring Cloud构建简单的微服务项目,常用的组件有:  
+ Sentinel：面向分布式服务架构的轻量级流量控制产品，主要以流量为切入点，从流量控制、熔断降级、系统负载保护等多个维度来保护服务的稳定性
+ Nacos：一个更易于构建云原生应用的动态服务发现、配置管理中心和服务管理平台(和zookeeper、Eureka等同属于服务协调中心)
+ RocketMQ：一款开源的分布式消息系统
+ Hystrix：断路器，防止单个服务的崩溃引发的雪崩效应，及时熔断服务来保护系统
+ Spring Cloud Gateway：Api网关，提供路由、负载均衡和反向代理等功能(类似nginx)
+ Config：配置中心，可以让各个子服务远程地使用配置中心里的配置

## 三、简单demo
+ 创建依赖管理，引入springCloud项目中需要依赖的组件
+ 创建服务提供者、消费者,并为每个服务配置注册中心(也可以使用Config配置中心，远程获取配置)
    ```
    #服务消费者
    spring:
      application:
        name: nacos-consumer #当前服务名
      cloud:
        nacos:
          discovery:
            server-addr: 127.0.0.1:8848  #服务注册中心地址

    server:
      port: 9091

    management:
      endpoints:
        web:
          exposure:
            include: "*"

    #服务提供者
    spring:
      application:
        name: nacos-provider
      cloud:
        nacos:
          discovery:
            server-addr: 127.0.0.1:8848

    server:
      port: 8081

    management:
      endpoints:
        web:
          exposure:
            include: "*"        
    ```
+ 依次启动注册中心、各个子服务

    