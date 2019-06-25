---
title: 컨트롤러 없이 뷰 페이지 바로 열리도록 설정
date: 2019-06-25
categories: spring, web, WebMvc, config, addViewController
---

컨트롤러 없이 뷰 이름만으로 해당페이지가 호출되도록 처리하는 설정.

`WebMvcConfig.java 파일은 @Configuration 파일들과 같은 위치에 두고 관리하면 편리하다.
`

```java
@Configuration
public class WebMvcConfig extends WebMvcConfigurerAdapter {
    // loginForm url 접근시 loginForm html 파일이 바로 열리도록 설정 된 예제.
    @Override
    public void addViewController(ViewControllerRegistry registry) {
        registry.addViewController("loginForm").setViewName("login/loginForm");
    }
}
```