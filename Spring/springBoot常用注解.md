# SpringBoot常用注解说明

## 核心注解
+ @Configuration
> org.springframework.context.annotation.Configuration  

    这是Spring 3.0添加的一个注解，用来代替applicationContext.xml配置文件，这个注解支持了所在类中使用代码来进行配置。  
    + 相关注解
        + @Bean  
        用来代替XML配置文件里面<bean ...>相关的配置
        + @Import
        用来引入额外的@Configuration修饰的配置类
        + @ImportResource
        如果有些通过类的注册方式配置不了的，可以通过这个注解引入额外的 XML 配置文件，有些老的配置文件无法通过 @Configuration 方式配置的非常管用
        + @SpringBootConfiguration
        这个注解就是 @Configuration 注解的变体，只是用来修饰是 Spring Boot 配置而已，或者可利于 Spring Boot 后续的扩展
+ @ComponentScan
>org.springframework.context.annotation.ComponentScan

    这是 Spring 3.1 添加的一个注解，用来代替配置文件中的 component-scan 配置，开启组件扫描，即自动扫描包路径下的 @Component 注解进行注册 bean 实例到 context 中。

    另外，@ComponentScans 是可重复注解，即可以配置多个，用来配置注册不同的子包
+ @EnableAutoConfiguration
>org.springframework.boot.autoconfigure.EnableAutoConfiguration
看全路径就知道，这是自 Spring Boot 诞生时添加的注解，用来提供自动配置，上面的两个都是 spring-context 包下的，不属于 Spring Boot

## 其它注解
+ @SpringBootApplication  
实际上包含了上面的三个核心注解,通常用于主类上
+ @Profiles
Spring Profiles提供了一种隔离应用程序配置的方式，并让这些配置只能在特定的环境下生效。任何@Component或@Configuration都能被@Profile标记，从而限制加载它的时机。
```
@Configuration
@Profile("production")
public class ProductionConfiguration {
// ...
}
```
+ @ResponseBody  
表示该方法的返回结果直接写入HTTP response body中  
一般在异步获取数据时使用，在使用@RequestMapping后，返回值通常解析为跳转路径，加上@responsebody后返回结果不会被解析为跳转路径，而是直接写入HTTP response body中。比如异步获取json数据，加上@responsebody后，会直接返回json数据。

+ @Component  
泛指组件，当组件不好归类的时候，我们可以使用这个注解进行标注。一般公共的方法我会用上这个注解。

+ @RequestParam
用在方法的参数前面
```
@RequestParam String a =request.getParameter("a");
```

+ @PathVariable
路径变量,restful风格中常用
```
RequestMapping("user/get/mac/{macAddress}")
public String getByMacAddress(@PathVariable String macAddress){
//do something;
}
```

+ @Value  
在application.properties或application.yml配置中获取值注入到代码中
```
// 对应配置文件中的配置（观察） 
    @Value("${spring.datasource.url}")
    private String url;

    @Value("${spring.datasource.username}")
    private String userName;

    @Value("${spring.datasource.password}")
    private String password;

    @Value("${spring.datasource.driver-class-name}")
    private String className;

```


