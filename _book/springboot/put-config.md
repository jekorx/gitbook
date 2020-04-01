# Put请求无法获取参数对象

> SpringBoot中使用RESTful API设计规范，如果Put请求无法将参数转为对象，以下两种配置可选。  
> springframework 版本 5.1 及之后，使用```FormContentFilter```替代```HttpPutFormContentFilter```。  

```java
@Configuration
public class WebMvcConfig extends WebMvcConfigurationSupport {
    /**
     * 解决put请求无法将参数转为对象
     * @return
     */
    @Bean
    public FormContentFilter httpPutFormContentFilter() {
        return new FormContentFilter();
    }
}
```

```java
// 使用：@Component，原理一样，开启：FormContentFilter
@Component
public class PutFilter extends FormContentFilter {
}
```

> ~~SpringBoot中使用RESTful API设计规范，如果Put请求无法将参数转为对象，以下两种配置可选。springframework 版本从 3.1 开始，到 5.1 之前，不包含 5.1 。~~

```java
@Configuration
public class WebMvcConfig extends WebMvcConfigurationSupport {
    /**
     * 解决put请求无法将参数转为对象
     * @return
     */
    @Bean
    public HttpPutFormContentFilter httpPutFormContentFilter() {
        return new HttpPutFormContentFilter();
    }
}
```

```java
// 使用：@Component，原理一样，开启：HttpPutFormContentFilter
@Component
public class PutFilter extends HttpPutFormContentFilter {
}
```



