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

### @RequestBody
+ HTTP 요청 본문을 메서드의 파라미터로 전달할 때 사용
+ 요청 본문의 데이터를 객체로 변환하여 사용할 수 있으며, 설정에 따라 다른 변환기를 사용할 수 있음

### @Valid
+ 객체의 유효성 검사를 수행할 때 사용함
+ 메서드의 파라미터 앞에 붙이고, 검증 오류가 발생하면 BindingResult 객체에 저장됨

### @ExceptionHandler
+ 컨트롤러 내에서 예외가 발생했을 때 처리할 메서드를 정의할 때 사용함
+ 예외 클래스를 지정하고, 해당 예외가 발생했을 때 실행될 메서드를 작성함

### @InitBinder
+ 요청 파라미터를 바인딩하기 전에 수행할 작업을 지정하는 Annotation
+ 주로 Validaotr를 등록하는 용도로 사용


