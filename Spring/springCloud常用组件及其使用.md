# SpringCloud常用组件及其使用
## Sentinel
流量监控组件，可以通过各种限流规则来实现流量控制，也可以通过这个组件来发现异常的服务接口(流量不正常)来实现熔断降级等
+ 启动Sentinel dashboard
+ 接入客户端  
1. 首先,引入Sentinel starter
```
    <dependency>
        <groupId>org.springframework.cloud</groupId>
        <artifactId>spring-cloud-starter-alibaba-sentinel</artifactId>
    </dependency>
```
2. 限流埋点  
    + HTTP 埋点  
    Sentinel starter 默认为所有的 HTTP 服务提供了限流埋点，如果只想对 HTTP 服务进行限流，那么只需要引入依赖，无需修改代码。

    + 自定义埋点
    如果需要对某个特定的方法进行限流或降级，可以通过 @SentinelResource 注解来完成限流的埋点，示例代码如下：
    ```
    /**
     * @SentinelResource 注解说明
     * value:资源名称(必填项,一般填接口函数名,也可以自定义名称)
     * entryType:入口类型(默认为EntryType.OUT)
     * blockHandler / blockHandlerClass:指定业务异常的处理类
     * fallback:fallback函数名称,仅针对降级功能生效(DegradeException)
     * 注意:fallback指定的函数名称需要和原方法在同一个类中,否
     * 则不会进入fallback逻辑;若blockHandler和fallback都进行
     * 了配置,遇到降级时优先会选择fallback处理
    */
    @SentinelResource(value="hello")
    public String hello() {
        return "Hello";
    }
    ```
3. 访问客户端，当访问一定次数后，刷新Sentinel dashboard会发现客户端已注册到了控制台(官方说第一次访问刷新即可在控制台看见实例。。。实际上我自己访问了多次才看见实例),在Sentinel dashboard上设置限流规则，具体参照官方文档
**注意:如果您在控制台没有找到应用，请调用一下进行了 Sentinel 埋点的 URL 或方法，因为 Sentinel 使用了 lazy load 策略。详细的排查过程请参见[Sentinel FAQ](https://github.com/alibaba/Sentinel/wiki/FAQ)**