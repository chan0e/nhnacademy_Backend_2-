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

## Spring MVC Components
![image](https://user-images.githubusercontent.com/94053008/232671385-956b2056-5768-44db-bc72-da9da5ace6be.png)

## @Value
+ org.springframework.beans.factory.annotation.Value
+ lombok에 있는 Value랑 다른거임



