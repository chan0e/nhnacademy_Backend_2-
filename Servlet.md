###### 사진출처 - nhnacademy

## Servlet

### Servlet Container 
+ 웹 컨테이너(web container, 또는 서블릿 컨테이너)는 웹 서버의 컴포넌트 중 하나로 자바 서블릿과 상호작용한다.
+ 웹 컨테이너는 서블릿의 생명주기를 관리하고, URL과 특정 서블릿을 맵핑하며 URL 요청이 올바른 접근 권한을 갖도록 보장한다.
+ 웹 컨테이너는 서블릿, 자바서버 페이지(JSP) 파일, 그리고 서버-사이드 코드가 포함된 다른 타입의 파일들에 대한 요청을 다룬다.
+ 웹 컨테이너는 서블릿 객체를 생성하고, 서블릿을 로드와 언로드하며, 요청과 응답 객체를 생성하고 관리하고, 다른 서블릿 관리 작업을 수행한다.
+ 웹 컨테이너는 웹 컴포넌트 자바 EE 아키텍처 제약을 구현하고, 보안, 병행성(concurrency), 생명주기 관리, 트랜잭션, 배포 등 다른 서비스를 포함하는 웹 컴포넌트의 실행 환경을 명세한다(specify).


![image](https://user-images.githubusercontent.com/94053008/229395839-36fc630b-3e60-44f8-92b4-cf6a751c1239.gif)

Servlet Lifecycle (이미지 출처: oracle.com'Java Servlet API Specification')












### Intellij에서 maven 프로젝트 생성 방법

![image](https://user-images.githubusercontent.com/94053008/229394336-9a5ed617-85f9-4562-b6be-d6fb24ef5c00.png)





![image](https://user-images.githubusercontent.com/94053008/229394570-c1ef62eb-c440-44df-b759-0215c4bca956.png)




+ pom.xml 설정

```servlet


 <properties>
        <project.build.sourceEncoding>UTF-8</project.build.sourceEncoding>
        
        //java EE 8 을 선택해서 하면 1.8로 되어있음
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

## Java logging

## Cookie

## Session


## RequestDispatch
+ 현재의 요청에 대한 정보를 저장했다가 다른 자원(servelt, jsp, html 등) 으로 전달(forward, include) 하는기능을 제공

> RequestDispatcher는 같은 웹 애플리케이션 내에서 다른 리소스로 요청을 전달하거나 포함하는 데 사용되는 객체 
이는 Servlet API의 일부이며 웹 애플리케이션에서 Model-View-Controller (MVC) 아키텍처를 구현하는 데 일반적으로 사용

RequestDispatcher 인터페이스는 forward()와 include() 두 가지 메서드를 제공 
 - forward() 메서드는 JSP 페이지와 같은 다른 리소스로 제어를 전송하는 데 사용 
 - include() 메서드는 다른 리소스의 출력을 현재 페이지의 출력에 포함시키는 데 사용

즉, RequestDispatcher는 다른 페이지나 서블릿으로 현재 요청을 보내거나 다른 페이지나 서블릿의 출력을 현재 페이지에 포함시키는 데 사용. 
이를 통해 웹 애플리케이션에서 유연한 처리가 가능해지며, 코드의 재사용성이 높아짐


```javascript
RequestDispatcher rd = request.getRequestDispatcher("/login");

//사용
rd.forward(request, response);

rd.include(request, response);

```

- browser 새로고침 -> request 객체가 유지됨

## Servlet Filter
+ 지정한 URL 패턴에 해당하는 요청에 대해
  - 서블릿 실행 전 후에
  - 해당 요청이나 응답에 공통적으로 적용할 작업을 수행하는 객체
+ 필터 체인 형태로 제공

![AyxEp2j8B4hCLKXAJCvEByelpKjnpi_9Br8eAKhCAmPAfUQLS4MxPUQKf1Of6CR2cKP0Pd1gKLbEQaai5vU6Kr5-UN5gaIOIKq7NJW6BHiDO1Jqx1OG6974a3KR8De4bu9OXYUkXsW1JWYmED0W0](https://user-images.githubusercontent.com/94053008/229658299-3257707a-7355-470d-b1f4-055fc58ba30e.png)

>Filter는 일종의 체인 형태로 동작합니다. 
클라이언트가 서버에 요청을 보내면, 이 요청은 Filter 체인의 맨 앞에서부터 순차적으로 각 Filter를 거치며 필터링됩니다. 
필터링은 일반적으로 요청과 응답의 헤더와 바디를 수정하거나, 인증과 권한 부여를 위한 처리, 요청과 응답에 대한 로깅 등의 작업을 수행

>Filter는 다음과 같은 장점을 제공
 - 중복 코드 제거: 여러 서블릿에서 공통으로 사용되는 코드를 Filter로 분리하여 중복을 제거할 수 있습니다.
 - 보안 강화: Filter를 이용하여 모든 요청에 대한 보안 검사나 인증 처리 등을 통합적으로 수행할 수 있습니다.
 - 코드 가독성 향상: 서블릿 코드에서 비즈니스 로직과 관계 없는 처리를 Filter로 분리하여 코드 가독성을 향상시킬 수 있습니다.

```javascript
public class CharacterEncodingFilter implements Filter {

    private  String encoding;

    @Override
    public void init(FilterConfig filterConfig) throws ServletException {
        Filter.super.init(filterConfig);
        encoding = filterConfig.getInitParameter("encoding");
    }

    @Override
    public void doFilter(ServletRequest servletRequest, ServletResponse servletResponse, FilterChain filterChain) throws IOException, ServletException {
            servletRequest.setCharacterEncoding(encoding);
            filterChain.doFilter(servletRequest,servletResponse);
            servletResponse.setCharacterEncoding(encoding);

    }
}
```

+ web.xm 설정

```
<filter>
    <filter-name>characterEncodingFilter</filter-name>
    <filter-class>com.nhnacademy.hello.filter.CharacterEncodingFilter</filter-class>
    <init-param>
        <param-name>encoding</param-name>
        <param-value>UTF-8</param-value>
    </init-param>
</filter>

<filter-mapping>
    <filter-name>characterEncodingFilter</filter-name>
    <url-pattern>/*</url-pattern>
</filter-mapping>
```

+ Filter를 이용해 로그인 여부 처리도 가능


## Listener
+ Servlet Container가 수행한 특정한 이벤트를 감지하여
그 이벤트 대해 별도의 작업을 수행하는 객체

![image](https://user-images.githubusercontent.com/94053008/229667887-390ebe30-2c83-463e-8963-2baf35d36a40.png)



## Form
```html
<form method='post' action='/login' enctype=''>
<!-- ... -->
</form>
```

### enc-type: HTML form content-type
+ 폼 데이터가 서버로 제출될 때 해당 데이터가 인코딩되는 방법을 명시
+ method='post' 일 때만 사용할 수 있음

### 속성값
+ application/x-www-form-urlencoded
  - default
  - key=value&key=value&...
  - 모든 데이터(문자)은 서버로 보내기 전에 인코딩됨을 명시함.
+ multipart/form-data
  - 모든 문자를 인코딩하지 않음을 명시함.
  - 파일이나 ASCII가 아닌 문자열, 바이너리 데이터 전송 시 multipart/form-data를 사용
  - multipart/form-data의 컨텐트는 multipart MIME 데이터의 모든 규칙을 따름
+ text/plain
  - 공백 문자(space)는 "+" 기호로 변환하지만, 나머지 문자는 모두 인코딩되지 않음을 명시함.

### MIME (Multipurpose Internet Mail Extensions)
+ 전자 우편을 위한 인터넷 표준 포맷 이메일 메세지의 형식을 확장해서 ASCII 이외의 문자셋으로 표현된 텍스트를 지원함
+ 오디오, 비디오, 이미지, 애플리케이션 프로그램 등을 첨부할 수 있도록 하기 위한 인터넷 표준
+ MIME 형식의 이메일 메세지는 SMTP나 POP, IMAP과 같은 표준 프로토콜로 전송

```
MIME(Multipurpose Internet Mail Extensions) 타입은 웹에서 파일의 형식을 구분하기 위해 사용

자주사용하는 MIME TYPE

- text/html : HTML 문서를 나타내는 MIME 타입입니다. 웹 브라우저에서 HTML 문서를 받을 때 사용
- text/plain : 일반 텍스트를 나타내는 MIME 타입입니다. 예를 들어, 서블릿에서 출력하는 일반 텍스트 메시지를 브라우저에서 받을 때 사용
- image/jpeg : JPEG 형식의 이미지를 나타내는 MIME 타입입니다. 웹 페이지에서 이미지를 보여줄 때 사용
- image/png : PNG 형식의 이미지를 나타내는 MIME 타입입니다. JPEG 대신 PNG를 사용하면 이미지의 투명도와 압축률이 더 좋아지는 등의 이점이 있음
- application/pdf : PDF 문서를 나타내는 MIME 타입입니다. 웹 페이지에서 PDF 문서를 보여줄 때 사용
- application/json : JSON 데이터를 나타내는 MIME 타입입니다. 웹 페이지에서 JSON 데이터를 전송하거나 받을 때 사용
- application/xml : XML 데이터를 나타내는 MIME 타입입니다. 웹 페이지에서 XML 데이터를 전송하거나 받을 때 사용
- application/octet-stream : 이진 파일을 나타내는 MIME 타입입니다. 예를 들어, 파일 다운로드 기능을 구현할 때 사용

위와 같은 MIME 타입은 서블릿과 JSP에서 응답(Response)을 생성할 때 Content-Type 헤더에 설정하여 클라이언트(웹 브라우저)가 올바르게 인식하도록 해야 함

```


## JSP
+ HTML 
