# SpringBoot基本介绍
在spring基础上添加的一个扩展,说白了就是在原来spring的配置基础上，基于最新的java特性，把配置项写在了java文件中，通过一些程序来动态的控制，实现了简化配置，简化插件引入流程，从而可以让我们构建一个spring项目变得更加的快速

## 为什么要用
传统spring项目中会产生各种配置文件,比如web项目中，还需要配置启动的servelt,修改web.xml，还有orm框架，spring事务、各种日志等等要配置。
如果能提供一个"服务"帮助我们进行一些默认的初始化配置，将很大程度提高开发效率，springboot就是这种扩展，内置了大量默认配置,tomcat、jetty、underdow等中间等，开箱即用

## SpringBoot Starter简介
经常在springboot项目的pom.xml依赖里有spring-boot-starter-web、mybatis-spring-boot-starter等模块,实际上这些Starter本身就是一个独立的maven项目，里面包含了所依赖的jar包，并且在该项目中写好各个依赖的关系，这样的话，再引入starter时就不用自己手动配置了(也可以定制自己的starter)