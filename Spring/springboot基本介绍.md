# SpringBoot基本介绍
在spring基础上添加的一个扩展,说白了就是在原来spring的配置基础上，基于最新的java特性，把配置项写在了java文件中，通过一些程序来动态的控制，实现了简化配置，简化插件引入流程，从而可以让我们构建一个spring项目变得更加的快速

## 为什么要用
传统spring项目中会产生各种配置文件,比如web项目中，还需要配置启动的servelt,修改web.xml，还有orm框架，spring事务、各种日志等等要配置。
如果能提供一个"服务"帮助我们进行一些默认的初始化配置，将很大程度提高开发效率，springboot就是这种扩展，内置了大量默认配置,tomcat、jetty、underdow等中间等，开箱即用

## SpringBoot Starter简介
经常在springboot项目的pom.xml依赖里有spring-boot-starter-web、mybatis-spring-boot-starter等模块,实际上这些Starter本身就是一个独立的maven项目，里面包含了所依赖的jar包，并且在该项目中写好各个依赖的关系，这样的话，再引入starter时就不用自己手动配置了(也可以定制自己的starter)

## 自动配置原理简介
[参考原文链接](https://www.cnblogs.com/trgl/p/7353782.html)  
+ 关键字
    1. 配置文件META-INF/spring.factories：实际上遵循了springboot提供的一些接口，配置具体实现的实现类,打开该文件可以看到是Key-value形式的配置,一般key是springboot、spring的接口名或注解名,value就是其接口和注解的具体实现类了
    2. 观察者模式,根据META-INF/spring.factories下默认提供的一些监听器接口(具体是什么东西在监听springboot启动有待研究)，在启动springboot时: 
        1. 遍历这些监听器并发出第一次通知(started()方法)
        2. 创建springboot最终使用的Envirnoment运行环境
        3. 再次发出通知(environmentPrepared()方法),发出springboot运行环境准备就绪的消息
        4. 最后推断出，springboot到底创建什么样的ApplicaionContext,是web应用还是什么应用,并根据之前准备好的Environment提供给这个ApplicaionContext
        5. 再次借助Spring-FactoriesLoader,查找所有对ApplicaionContext进行进一步处理的监听器,并进行通知(contextPrepared()方法)
        6. 根据用户注解等配置形式的配置内容,整合到上述准备完毕的ApplicatonContext中(核心)
        7. 最后使用一组监听器发布通知，ApplicationContext已经加载完毕，各位可以结束手头的工作了
        8. 调用ApplicationContext的refresh()完成最终启动。

+ 总结  
    springboot本质上，还是spring的概念。所谓的自动配置，只是从以往的开发经验和场景中抽取出来的一些固化的、约定俗成的规则,需要开发者遵循默认规则，springboot中这些默认的启动方式才会有作用        
                  