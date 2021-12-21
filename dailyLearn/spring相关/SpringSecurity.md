# Spring Security

## Spring Security简介

1. 认证：你是谁

2. 授权：你可以做什么

### WebSecurityConfigurerAdapter

三个顶级配置项构建器的构建重载回调方法：

```java
protected void configure(AuthenticationManagerBuilder auth) throws Exception {
    this.disableLocalConfigureAuthenticationBldr = true;
}
```

```java
public void configure(WebSecurity web) throws Exception {}
```

```java
protected void configure(HttpSecurity http) throws Exception {
    this.logger.debug("Using default configure(HttpSecurity). If subclassed this will potentially override subclass configure(HttpSecurity).");
    //通过authorizeRequests方法来请求权限配置，返回一个url拦截器，调用提供的anyReuqest(),antMatchers()和regexMatcers()方法来匹配系统的URL
    ((HttpSecurity)((HttpSecurity)((AuthorizedUrl)http.authorizeRequests()
    //对http所有请求必须通过授权认证才可以访问
        .anyRequest()).authenticated()
        .and())
    .formLogin().and()).httpBasic();
}
```

安全配置类去覆盖configure方法，可以自定义一些功能

如：自定义表单登录页

```java
@EnableWebSecurity
public class WebSecurityConfig extends WebSecurityConfigurerAdapter {

    @Override
    protected void configure(HttpSecurity http) throws Exception {
        http.authorizeRequests()
                .anyRequest().authenticated()
                .and()
                .formLogin()
                    .loginPage("/myLogin.html")
                    .permitAll()
                    .and()
                .csrf().disable();
    }
}
```

在这里，详细解释一下@EnableWebSecurity

```java
@Retention(RetentionPolicy.RUNTIME)
@Target({ElementType.TYPE})
@Documented
//激活了@import注解中包含的配置类
//WebSecurityConfiguration web安全配置
//SpringWebMvcImportSelector判断当前环境是否包含spring mvc
@Import({WebSecurityConfiguration.class, SpringWebMvcImportSelector.class, OAuth2ImportSelector.class})
//配置认证信息
@EnableGlobalAuthentication
@Configuration
public @interface EnableWebSecurity {
    boolean debug() default false;
}
```

在WebSecurityConfiguration中，有核心拦截器：springSecurityFilterChain

```java
    @Bean(
        name = {"springSecurityFilterChain"}
    )
    public Filter springSecurityFilterChain() throws Exception {
        boolean hasConfigurers = this.webSecurityConfigurers != null && !this.webSecurityConfigurers.isEmpty();
        if (!hasConfigurers) {
            WebSecurityConfigurerAdapter adapter = (WebSecurityConfigurerAdapter)this.objectObjectPostProcessor.postProcess(new WebSecurityConfigurerAdapter() {
            });
            this.webSecurity.apply(adapter);
        }

        return (Filter)this.webSecurity.build();
    }
```

### 自动登录与自动注销

#### 自动登录有两种方式
