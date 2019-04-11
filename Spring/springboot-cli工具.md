# SpringBoot CLI命令行工具的使用
Spring Boot是一个命令行工具，用于使用Spring进行快速原型搭建

## 安装
可以从Spring软件仓库下载Spring CLI分发包：  
[spring-boot-cli-1.3.0.BUILD-SNAPSHOT-bin.zip](http://repo.spring.io/snapshot/org/springframework/boot/spring-boot-cli/1.3.0.BUILD-SNAPSHOT/spring-boot-cli-1.3.0.BUILD-SNAPSHOT-bin.zip)  
[spring-boot-cli-1.3.0.BUILD-SNAPSHOT-bin.tar.gz](http://repo.spring.io/snapshot/org/springframework/boot/spring-boot-cli/1.3.0.BUILD-SNAPSHOT/spring-boot-cli-1.3.0.BUILD-SNAPSHOT-bin.tar.gz)  

## 使用
初始化新项目 --list选项为已有的能初始化项目的骨架列表依赖
```
spring init --list
```

比如需要web依赖和jpa依赖
```
spring init --dependencies=web,data-jpa myproject
```
这样就会得到myproject项目了

运行一个简单的RESTful服务  
新建一个hello.groovy文件
```
@RestController
public class HelloController {

    @RequestMapping(value = "/hello")
    public String sayHello() {
        return "Hello，Spring Boot！";
    }
}
```
然后执行下面指令，进行编译运行应用：
```
spring run hello.groovy
```