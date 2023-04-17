###### 사진출처 - nhnacademy

## MVC Model
![image](https://user-images.githubusercontent.com/94053008/232352632-01f3340e-7ad0-4b06-9152-4596743e803b.png)

## Spring MVC 에서의 Front Controller
+ Spring MVC Framework의 중심이 되는 Servlet
+ Controller로 향하는 모든 웹 요청의 entry point
+ Front Controller 디자인 패턴의 표현
![image](https://user-images.githubusercontent.com/94053008/232352662-36eeae9f-02cf-497c-8853-588cb00ab5bc.png)


## Context
+ Spring 에서 스프링이 관리하는 Bean들이 담겨져있는 컨테이너

### ROOT - CONTEXT
+ 모든 Servlet이 공유할 수 있는 Bean들이 모인 공간
+ @Repositroy, @Service, @Component, @Configuration

### SERVLET - CONTEXT
+ Servlet 각자의 Bean이 모인 공간
+ Context 내에서의 Bean들은 서로 공유될 수 없음
+ @Controller
+ Servlet 간에는 Bean을 공유할 수 없음

![image](https://user-images.githubusercontent.com/94053008/232352825-55310f68-5c89-4916-8e86-1d3a8723bfd0.png)

### Bean Factory
+ Bean 생성 및 의존관계의 설정을 담당하는 가장 기본적인 IOC Contatiner

