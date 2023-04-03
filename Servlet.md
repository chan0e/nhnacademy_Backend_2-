## Servlet

### Servlet Container 
+ 웹 컨테이너(web container, 또는 서블릿 컨테이너)는 웹 서버의 컴포넌트 중 하나로 자바 서블릿과 상호작용한다.
+ 웹 컨테이너는 서블릿의 생명주기를 관리하고, URL과 특정 서블릿을 맵핑하며 URL 요청이 올바른 접근 권한을 갖도록 보장한다.
+ 웹 컨테이너는 서블릿, 자바서버 페이지(JSP) 파일, 그리고 서버-사이드 코드가 포함된 다른 타입의 파일들에 대한 요청을 다룬다.
+ 웹 컨테이너는 서블릿 객체를 생성하고, 서블릿을 로드와 언로드하며, 요청과 응답 객체를 생성하고 관리하고, 다른 서블릿 관리 작업을 수행한다.
+ 웹 컨테이너는 웹 컴포넌트 자바 EE 아키텍처 제약을 구현하고, 보안, 병행성(concurrency), 생명주기 관리, 트랜잭션, 배포 등 다른 서비스를 포함하는 웹 컴포넌트의 실행 환경을 명세한다(specify).


### Intellij에서 maven 프로젝트 생성 방법

![image](https://user-images.githubusercontent.com/94053008/229394336-9a5ed617-85f9-4562-b6be-d6fb24ef5c00.png)





![image](https://user-images.githubusercontent.com/94053008/229394570-c1ef62eb-c440-44df-b759-0215c4bca956.png)




+ pom.xml 설정

```servlet


 <properties>
        <project.build.sourceEncoding>UTF-8</project.build.sourceEncoding>
        
        //1.8을 11로 고쳐줌
        <maven.compiler.target>11</maven.compiler.target>
        <maven.compiler.source>11</maven.compiler.source>
        <junit.version>5.9.1</junit.version>
 </properties>
```

+ web.xml 설정

```servlet

<servlet>
    <servlet-name>helloServlet</servlet-name>
    <servlet-class>com.nhnacademy.hello.HelloServlet</servlet-class>
</servlet>
    
<servlet-mapping>
    <servlet-name>helloServlet</servlet-name>
    <url-pattern>/hello</url-pattern>
</servlet-mapping>

```


## WAS(Web Application Server)
+ 주로 정적 웹 콘텐츠를 처리하는 웹서버와 구분하기 위한 용도
+ Servlet Container, EJB Container 등의 역할을 수행
+ 동적 웹 콘텐츠를 생성하기 위한 Web Application과 Server 환경을 만들어 동작시키는 기능을 제공

