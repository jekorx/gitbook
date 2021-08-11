# 跨域配置

> SpringBoot添加跨域配置有以下两种配置方法  
> 使用```addCorsMappings```方式配置跨域：要区分SpringBoot版本  
> **SpringBoot2.4之前**：```.allowedOrigins("*")```  
> **SpringBoot2.4及之后**：```.allowedOriginPatterns("*")```  

```java
@Configuration
public class WebMvcConfig extends WebMvcConfigurationSupport {
    /**
     * 跨域配置
     */
    @Override
    protected void addCorsMappings(CorsRegistry registry) {
        registry.addMapping("/**")
            // 允许跨域的源，SpringBoot2.4之前
            // .allowedOrigins("*")
            // SpringBoot2.4及之后使用allowedOriginPatterns
            .allowedOriginPatterns("*")
            // 是否允许浏览器发送Cookie
            .allowCredentials(true)
            // 客户端所要访问的资源允许使用的方法或方法列表
            .allowedMethods("OPTIONS", "HEAD", "POST", "GET", "PUT", "DELETE")
            // 正式请求的首部信息
            // x-requested-with：ajax请求
            .allowedHeaders("X-Requested-With")
            // preflight request （预检请求）的返回结果
            //（即 Access-Control-Allow-Methods 和Access-Control-Allow-Headers 提供的信息）
            // 可以被缓存多久
            .maxAge(3600);
        super.addCorsMappings(registry);
    }
}
```

```java
/**
 * 跨域访问过滤器
 */
@Component
public class CorsFilter implements Filter {

    @Override
    public void destroy() {
    }

    @Override
    public void doFilter(ServletRequest req, ServletResponse res, FilterChain chain) throws IOException, ServletException {

        HttpServletResponse response = (HttpServletResponse) res;
        HttpServletRequest request = (HttpServletRequest) req;

        // 也可以使用"*"，最好是从request中的header中获取Origin，来做配置
        response.setHeader("Access-Control-Allow-Origin", request.getHeader("Origin"));
        // 是否允许浏览器发送Cookie
        response.setHeader("Access-Control-Allow-Credentials", "true");
        // 客户端所要访问的资源允许使用的方法或方法列表
        response.setHeader("Access-Control-Allow-Methods", "OPTIONS, HEAD, POST, GET, PUT, DELETE");
        // 正式请求的首部信息
        // x-requested-with：ajax请求
        response.setHeader("Access-Control-Allow-Headers", "X-Requested-With");
        // preflight request （预检请求）的返回结果
        //（即 Access-Control-Allow-Methods 和Access-Control-Allow-Headers 提供的信息）
        // 可以被缓存多久
        response.setHeader("Access-Control-Max-Age", "3600");

        chain.doFilter(req, res);
    }

    @Override
    public void init(FilterConfig config) throws ServletException {
    }

}
```



