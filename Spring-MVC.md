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


## WebApplicationInitializer의 구조



![image](https://user-images.githubusercontent.com/94053008/232403088-df85a9c1-7259-4b99-8b83-6d6493d0f408.png)


### Controller 실습

```java
// TODO #2: `GET /login` 요청을 처리하세요.
    //          `SESSION` 이라는 쿠키가 있으면 로그인 완료 메세지 출력 (`loginSuccess.jsp`).
    //          `SESSION` 이라는 쿠키가 없으면 로그인 폼 화면 출력 (`loginForm.jsp`).

    @GetMapping("/login")

    public String login(@CookieValue(name = "SESSION" ,required = false) String session) {

        if(StringUtils.hasText(session)){
            return "loginSuccess";
        }
        return "loginForm";
    }

    // TODO #3: `POST /login` 요청을 처리하세요.
    //          `userRepository.matches(id, password)` 메서드 이용.
    //          로그인 성공 시 `SESSION` 쿠키에 session id 값 저장하고
    //          모델을 이용해서 `loginSuccess.jsp`에 세션 아이디 전달.
    //          로그인 실패 시 `/login`으로 redirect.

    @PostMapping("/login")
    public String doLogin(String id, String pwd, Model model, HttpServletRequest request , HttpServletResponse response)
    {
        if(userRepository.matches(id,pwd)){

            HttpSession httpSession = request.getSession(true);
            Cookie cookie = new Cookie("SESSION", httpSession.getId());
            response.addCookie(cookie);
            model.addAttribute("id",httpSession.getId());
            return "loginSuccess";
        }else{
            return "redirect:/login";
        }

    }

```



## 예외처리 (@ExceptionHandler)
+ Spring MVC에서 예외처리를 담당하는 Annotation 중 하나
+ Annotation을 이용해서 컨트롤러 내에서 발생한 예외를 캐치하고, 예외 발생 시 실행될 코드를 지정 할수 있음
+ method level에서 선언되며 예외처리를 담당하는 method에서 사용

> @ExceptionHandler(RuntimeExcpetion.class) 예제

```java

@ControllerAdvice
public class ExceptionHandlerController {

    @ExceptionHandler(RuntimeException.class)
    public ResponseEntity<String> handleRuntimeException(RuntimeException ex) {
        return new ResponseEntity<>(ex.getMessage(), HttpStatus.INTERNAL_SERVER_ERROR);
    }

}

```
+ ExceptionHandler에서 사용가능한 method argument
    - HttpServletRequest, HttpServletResponse, HttpSession, WebRequest
    - Locale
    - InputStream, OutputStream, Reader, Writer
    - Map, Model, ModelMap

+ ExceptionHandler에서 사용가능한 return type
    - ModelAndView, View
    - Map, Model, ModelMap
    - String
    - Void
    - @ResponseBody
    - POJO

### @ControllerAdive
+ 전역적으로 적용할 수 있는 컨트롤러를 정의할 때 사용
+ 예를 들어, 여러 컨트롤러에서 발생할 수 있는 예외를 하나의 클래스에서 처리하고자 할때 사용(공동 error 처리가능)
+ 하나의 클래스에서 처리함으로 중복된 코드를 줄이고, 코드 유지보수성을 향상시킴


## Validation
+ 입력값이 어떤 조건을 만족하는지 검증하는 작업을 의미
+ @Valid Annotation을 이용하여 Bean Validation 기능을 수행

### Bean Validation Library

API
```xml
<dependency>
    <groupId>jakarta.validation</groupId>
    <artifactId>jakarta.validation-api</artifactId>
    <version>2.0.2</version>
</dependency>
```

Implementation


```xml
<dependency>
    <groupId>org.hibernate.validator</groupId>
    <artifactId>hibernate-validator</artifactId>
    <version>6.2.3.Final</version>
</dependency>
```


![image](https://user-images.githubusercontent.com/94053008/233260234-19a50c85-4f37-4b18-91bc-2d45362b54a7.png)




> 회원가입시 입력되는 정보중 이메일 주소가 입력될때 해당메일이 유효한것인지 검증하는 예제
```java

public class SignupForm {
    @NotEmpty
    @Email
    private String email;
    ...
}

@Controller
public class SignupController {
    @PostMapping("/signup")
    public String signup(@Valid SignupForm signupForm, BindingResult bindingResult) {
        if (bindingResult.hasErrors()) {
            return "signup";
        }
        ...
    }
}

```



## Spring's Validator
+ org.springframework.validation.Validator interface를 이용한 Validation 구현

```java
public interface Validator {
	boolean supports(Class<?> clazz);
	void validate(Object target, Errors errors);
}
```

## Spring MVC Components
![image](https://user-images.githubusercontent.com/94053008/232671385-956b2056-5768-44db-bc72-da9da5ace6be.png)


## HttpMessageConverter
+ http 요청과 응답의 본문(body)에 있는 데이터를 자바 객체로 변환하거나, 자바 객체를 http 요청 또는 응답의 본문에 있는 데이터로 변환 역할을 해주는 인터페이스
+ 자바 객체를 http 요청 또는 응답의 본문에 있는 데이터로 변환하여 원격 서버와 통신할 때 사용됨
+ 예를 들어, 클라이언트에서 JSON 형식으로 데이터를 HTTP 요청의 본문에 담아 서버로 전송하고, 서버는 이를 받아서 자바 객체로 변환하여 처리할 때, HttpMessageConverter가 JSON 데이터를 자바 객체로 변환해주는 역할을 수행. 마찬가지로 서버에서 클라이언트로 응답할때도 가능


![image](https://user-images.githubusercontent.com/94053008/233266017-b363fc77-2f16-4bd4-a31c-5f05e4b74534.png)


### @EnableWebMvc
+ Spring MVC 구성요소를 활성화하는데 사용
+ WebMvcConfigurer interface를 implements해서 Spring MVC 구성을 추가로 설정할수 있음

> WebMvcConfigurer method 재정의 예제
```java
@Configuration
@EnableWebMvc
@ComponentScan(basePackages = "com.example.controller")
public class AppConfig implements WebMvcConfigurer {
    
    @Override
    public void configureViewResolvers(ViewResolverRegistry registry) {
        registry.jsp("/WEB-INF/views/", ".jsp");
    }
    
    @Override
    public void addResourceHandlers(ResourceHandlerRegistry registry) {
        registry.addResourceHandler("/resources/**").addResourceLocations("/resources/");
    }
}
```

1. configureViewResolvers method

```java
 @Override
    public void configureViewResolvers(ViewResolverRegistry registry) {
	registry.jsp("/WEB-INF/views/", ".jsp");
    }

```
+ JSP View Resolvers를 등록하는 메소드
+ 첫번째 인자로 JSP 파일이 위치하는 경로를, 두번째 인자로 JSP 파일 확장자를 받음


2. addResourceHandlers method

```java
@Override
public void addResourceHandlers(ResourceHandlerRegistry registry) {
    registry.addResourceHandler("/resources/**").addResourceLocations("/resources/");
}

```
+ 정적 자원 처리를 위한 핸들러를 등록하는 메소드
+ 첫 번째 인자로 요청 url패턴을, 두 번째 인자로 정적 자원이 위치하는 경로를 전달받아 등록
+ 즉,/resources/** 패턴으로 요청이 오면, /resources/ 경로에 위치한 정적 자원을 찾아서 응답으로 전송
+ 예를 들어, /resources/css/style.css URL로 요청이 오면, /resources/css/style.css 파일을 찾아서 응답으로 전송


### ObjectMapper
+ 이를 사용하기 위해선 Jackson 라이브러리가 프로젝트에 추가되어 있어야 함
```java
<!-- Maven을 사용하는 경우 -->
<dependency>
    <groupId>com.fasterxml.jackson.core</groupId>
    <artifactId>jackson-databind</artifactId>
    <version>2.12.4</version>
</dependency>

```

+ Java 객체를 JSON 데이터로 변환
	> 예제 코드
	
	```java
	 ObjectMapper objectMapper = new ObjectMapper();
	 
	 // Java 객체를 JSON 문자열로 변환
	 User user = new User("John", 30);
	 String jsonString = objectMapper.writeValueAsString(user);
	 System.out.println(jsonString); // {"name":"John","age":30}
	 
	 // Java 객체를 출력 스트림으로 직접 출력
	OutputStream outputStream = new FileOutputStream("user.json");
	objectMapper.writeValue(outputStream, user);
	 ```
	
+ JSON 데이터를 Java 객체로 변환
	> 예제 코드


	```java
	ObjectMapper objectMapper = new ObjectMapper();

	// JSON 문자열을 Java 객체로 변환
	String jsonString = "{\"name\":\"John\",\"age\":30}";
	User user = objectMapper.readValue(jsonString, User.class);
	System.out.println(user.getName()); // John
	System.out.println(user.getAge()); // 30

	// 입력 스트림으로부터 JSON 데이터를 읽어서 Java 객체로 변환
	InputStream inputStream = new FileInputStream("user.json");
	User user2 = objectMapper.readValue(inputStream, User.class);
	
	
+ 설정 변경
	- JSON 데이터의 직렬화/역질렬화 과정에서 사용되는 설정을 변경할 수 있음
	> 예제 코드

	```java
	
	ObjectMapper objectMapper = new ObjectMapper();

	// 직렬화 시 빈 값이 포함되지 않도록 설정
	objectMapper.setSerializationInclusion(JsonInclude.Include.NON_NULL);

	// 날짜 데이터를 "yyyy-MM-dd" 형식으로 직렬화하도록 설정
	SimpleDateFormat dateFormat = new SimpleDateFormat("yyyy-MM-dd");
	objectMapper.setDateFormat(dateFormat);

	// Java 객체를 JSON 문자열로 변환
	User user = new User("John", 30);
	String jsonString = objectMapper.writeValueAsString(user);
	System.out.println(jsonString); // {"name":"John","age":30}

	// JSON 문자열을 Java 객체로 변환
	String jsonString2 = "{\"name\":\"John\",\"age\":null}";
	User user2 = objectMapper.readValue(jsonString2, User.class);
	System.out.println(user2.getName()); // John
	System.out.println(user2.getAge()); // null
	
	
	
	
## @ResponseBody, @RequestBody, @ResponseBody

### @ResponseEntity
+ Spring Framework에서 http response을 감싸는 역할을 함(직접 http 응답을 구성할 수 있음)
+ 생성자를 이용해 응답 본문, HTTP 상태 코드, 응답헤더 등을 설정할 수 있음



### @RequestBody
+ HTTP 요청 본문을 메서드의 파라미터로 전달할 때 사용
+ 요청 본문의 데이터를 객체로 변환하여 사용할 수 있으며, 설정에 따라 다른 변환기를 사용할 수 있음

### @ResponseBody
+ java객체를 http 응답의 Body로 변환하는데 사용

## RedirectAttribute 와 FlashMapManager
+ Spring에서 사용되는 redirection 기능을 제공하는 클래스

1. RedirectAttribute
+ redirect시 데이터를 전달하기 위한 인터페이스로 redirect 시 보내고자하는 데이터를 속성형태로 저장
+ 이를 통해 리다이렉트 이후에도 데이터를 유지하고 활용할수 있음

2. FlashMapManager
+ RedirectAttribute와 유사한 기능을 제공하지만 보다 일시적인 데이터 전달에 적합
+ 일시적인 데이터란, 리다이렉트 이후 바로 사용되고 그 이후에는 필요하지 않은 데이터를 말함

> 예제 코드

```java
@Controller
public class MyController {
 
    @PostMapping("/data")
    public String handleData(
        @RequestParam("data") String data,
        RedirectAttributes redirectAttributes) {
 
        // 데이터 검증 및 처리 로직 수행
 
        redirectAttributes.addFlashAttribute("message", "Data processed successfully.");
        return "redirect:/result";
    }
 
    @GetMapping("/result")
    public String showResult

```

+ 이렇게 일시적으로 보내진 데이터는 폼에서 보여줄수 있음
> 에제 코드
```java
<div th:if="${message}" style="color: red;">
        <p>${message}</p>
</div>
```

## Thymeleaf

+ 의존 라이브러리
```xml
<dependency>
    <groupId>org.thymeleaf</groupId>
    <artifactId>thymeleaf-spring5</artifactId>
    <version>3.0.11.RELEASE</version>
</dependency>
```

+ HTML, XML, javascript, Css 등의 마크업 언어와 통합하여 서버 사이드에서 웹 애플리케이션을 개발할 수 있도록 해주는 자바 템플릿 엔진
+ 장점
	- 자바 객체를 HTML 파일에 직접 바인딩할 수 있어서 개발 생산성이 높아짐
	- 문법이 간단하고 직관적이여서 학습 곡선이 낮음
	- 다국어 지원이 내장

> 몇가지 문법들

1. 변수표현식
+ ${..} 로 표현되며 변수값을 출력하는데 사용됨

```html
<p th:text="${username}">default username</p>
```

2. 리터럴. 텍스트
+ 텍스트를 삽입하는데 사용되며 표현식 내부에서 사용
```html
<p>안녕하세요! <span th:text="${username}">default username</span>님!</p>
```

3. 반복문
```html
<table>
  <tr th:each="user : ${users}">
    <td th:text="${user.id}">1</td>
    <td th:text="${user.name}">User1</td>
    <td th:text="${user.email}">user1@example.com</td>
  </tr>
</table>
```

4. 조건문
```html
<p th:if="${isAdmin}">관리자입니다.</p>
<p th:unless="${isAdmin}">관리자가 아닙니다.</p>
```

5. 메세지 처리
+ #{..}을 사용하여 다국어 메시지를 처리할 수 있음

```html
<p th:text="#{greeting.message}">Hello, World!</p>
```


## @Value
+ org.springframework.beans.factory.annotation.Value
+ lombok에 있는 @Value랑 다른거임
	- cf) lombok.@value를 사용하면 클래스 내의 모든 필드에 대한 생성자와 Getter 메소드가 자동으로 생성
	- Setter 메소드는 생성되지 않음
	- equals.hashCode 메소드도 자동으로 생성
	- 불변 객체를 쉽게 생성
+ 스프링 빈의 필드나 생성자 파라미터에 값을 주입할때 사용
+ properties 파일 등의 외부 설정 정보를 읽어와서 해당 필드나 생성자 파라미터에 값을 주입할수 있음
> 예제 코드

```java
@Configuration
@PropertySource("classpath:some.properties")
public class PropertiesConfig {
    @Value("${key1}")
    private String key1;

    @Bean
    public List<String> keys(@Value("${key2}") String key2) {
        List<String> list = new ArrayList<>();
        list.add(key1);
        list.add(key2);

        return list;
    }

}

```



