## Spring MVC Annotation 정리

### @Controller
+ 해당 클래스가 컨트롤러 임을 선언하는 Annotation
+ HTTP 요청을 처리하는 메서드를 정의하고, @RequestMapping과 함께 사용하여 매핑
+ 주로 View를 반환하지만 @responsebody를 사용하여 데이터를 반환할수 있음


### @RestController
+ @Controller와 유사하지만, 모든 요청에 대한 응답으로 JSON, XML 등의 데이터를 반환함
+ @ResponseBody를 생략할 수 있는 특징이 있음


### @RequestMapping
+ 요청 URL와 컨트롤러의 메서드를 매핑함
+ 메서드와 클래스에 모두 적용 가능하며, HTTP 요청 방식(GET, POST, PUT, DELETE 등)도 설정 가능함
+ URI 패턴과 변수를 사용할 수 있으며, 기본값으로 GET 요청에 대한 매핑을 함


```java
@Controller
public class HelloController {
 
    @RequestMapping("/hello")
    public String hello() {
        return "hello";
    }
 
}
```

### GetMapping, PostMapping,,,
+ GET과  POST 등 메서드에 바로 매핑 가능


```java
@GetMapping("/hello")
public String sayHello() {
    return "Hello, World!";
}

```
+ @RequestMapping(value="/hello", method=RequestMethod.GET)과 동일한 의미


### @PathVariable
+ @RequestMapping과 함께 사용되어 , URL 경로에서 변수를 추출할 때 사용
+ 변수 이름을 설정하고 메서드 파라미터에서 어노테이션을 사용하여 변수 값을 가져올 수 있음

```java
@GetMapping("/users/{id}")
public User getUserById(@PathVariable Long id) {
    return userService.getUserById(id);
}
```

### @RequestParam
+ HTTP 요청 파라미터를 메서드의 파라미터로 전달할때 사용함
+ 파라미터 이름과 변수 이름을 설정하고, required 옵션을 사용하여 필수 여부를 설정할수 있음

```java
 @RequestParam("name") String name
```
+ @RequestParam("name") String name은 name이라는 이름의 요청 파라미터 값을 String 타입의 name 매개변수에 바인딩

### @ModelAttribute
+ HTTP 요청 파라미터를 객체로 변환할때 사용
+ 파라미터 이름과 객체 필드 이름이 일치하면 자동으로 매핑되며, 별도로 설정할 수 도 있음
```java
@PostMapping("/purchase")
    public String purchaseSubmit(@ModelAttribute("product") Product product, 
                                 @RequestParam("paymentOption") String paymentOption) {
        // 구매 처리 로직
        return "purchase-result";
    }

```
+ 코드는 Product 객체를 생성하고 해당 객체에 HTTP 요청으로부터 전달받은 파라미터를 매핑한 후, product이라는 이름으로 컨트롤러 메서드의 파라미터로 전달해주는 역할

### @ResponseEntity
+ Spring Framework에서 http response을 감싸는 역할을 함(직접 http 응답을 구성할 수 있음)
+ 생성자를 이용해 응답 본문, HTTP 상태 코드, 응답헤더 등을 설정할 수 있음



### @RequestBody
+ HTTP 요청 본문을 메서드의 파라미터로 전달할 때 사용
+ 요청 본문의 데이터를 객체로 변환하여 사용할 수 있으며, 설정에 따라 다른 변환기를 사용할 수 있음

### @ResponseBody
+ java객체를 http 응답의 Body로 변환하는데 사용

> @ResponseEntity,@RequestBody,@ResponseBody를 사용한 예제 코드

```java
@RestController
@RequestMapping("/api")
public class UserController {
    
    @Autowired
    private UserService userService;
    
    @PostMapping("/users")
    public ResponseEntity<User> createUser(@RequestBody User user) {
        userService.addUser(user);
        return ResponseEntity.status(HttpStatus.CREATED).body(user);
    }
    
    @GetMapping("/users/{userId}")
    public ResponseEntity<User> getUserById(@PathVariable("userId") int userId) {
        User user = userService.getUserById(userId);
        if (user == null) {
            return ResponseEntity.notFound().build();
        }
        return ResponseEntity.ok(user);
    }
    
    @GetMapping("/users")
    public ResponseEntity<List<User>> getAllUsers() {
        List<User> users = userService.getAllUsers();
        if (users.isEmpty()) {
            return ResponseEntity.noContent().build();
        }
        return ResponseEntity.ok(users);
    }
}

```



### @Valid
+ 객체의 유효성 검사를 수행할 때 사용함
+ 메서드의 파라미터 앞에 붙이고, 검증 오류가 발생하면 BindingResult 객체에 저장됨

```java
@PostMapping("/login")
public String login(@Valid LoginForm loginForm, BindingResult bindingResult) {
    if (bindingResult.hasErrors()) {
        return "login";
    }
    // 로그인 로직 처리
    return "home";
}

```

### @ExceptionHandler
+ 컨트롤러 내에서 예외가 발생했을 때 처리할 메서드를 정의할 때 사용함
+ 예외 클래스를 지정하고, 해당 예외가 발생했을 때 실행될 메서드를 작성함

```java 

@ControllerAdvice
public class GlobalExceptionHandler {

    @ExceptionHandler(Exception.class)
    public ModelAndView handleAllExceptions(Exception ex) {
        ModelAndView model = new ModelAndView("error");
        model.addObject("errMsg", "An error occurred: " + ex.getMessage());
        return model;
    }
}

```

### @InitBinder
+ 요청 파라미터를 바인딩하기 전에 수행할 작업을 지정하는 Annotation
+ 컨트롤러에서 사용되는 폼 데이터 바인딩을 초기화 할수 있음
+ 주로 Validaotr를 등록하는 용도로 사용
+ setter 메서드 대신 필드에 직접 값을 주입할 수있음 

```java
@InitBinder
    void initBinder(WebDataBinder binder){
        binder.initDirectFieldAccess();
    }
```

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

+ EnableWebMvc를 사용하기위해 spring-webmvc 모듈을 프로젝트에 의존성 설정을 해야함
 - 주요기능
   - 컨트롤러(Controller): 웹 애플리케이션의 비즈니스 로직을 처리하는 컨트롤러 클래스를 작성
   - 요청 매핑(Request Mapping): URL 패턴과 컨트롤러 메서드를 매핑하여 요청을 처리
   - 모델-뷰-컨트롤러 패턴: 애플리케이션의 로직을 모델(Model)과 뷰(View), 컨트롤러(Controller)로 분리하여 개발
   - 뷰 리졸버(View Resolver): 컨트롤러에서 반환된 뷰 이름을 실제 뷰로 해석하여 렌더링
   - 데이터 바인딩(Data Binding): 클라이언트의 요청 데이터를 자바 객체에 자동으로 매핑하는 기능을 제공
   - 폼 처리(Form Handling): 폼 데이터의 검증과 바인딩을 처리하는 기능을 제공
   - 인터셉터(Interceptor): 요청 처리 전후에 로직을 실행할 수 있는 인터셉터를 설정
   - 예외 처리(Exception Handling): 예외 발생 시 처리할 수 있는 기능을 제공
   -파일 업로드 및 다운로드: 파일 업로드와 다운로드를 처리할 수 있는 기능을 제공



  

