## Spring MVC Annotation 정리

### @Controller
+ 해당 클래스가 컨트롤러 임을 선언하는 Annotation
+ HTTP 요청을 처리하는 메서드를 정의하고, @RequestMapping과 함께 사용하여 매핑

### @RestController
+ @Controller와 유사하지만, 모든 요청에 대한 응답으로 JSON, XML 등의 데이터를 반환함
+ @ResponseBody를 생략할 수 있는 특징이 있음

### @RequestMapping
+ 요청 URL와 컨트롤러의 메서드를 매핑함
+ 메서드와 클래스에 모두 적용 가능하며, HTTP 요

### @PathVariable
+ @RequestMapping과 함께 사용되어 , URL 경로에서 변수를 추출할 때 사용
+ 변수 이름을 설정하고 메서드 파라미터에서 어노테이션을 사용하여 변수 값을 가져올 수 있음

### @ RequestParam
+ HTTP 요청 파라미터를 메서드의 파라미터로 전달할때 사용함
+ 파라미터 이름과 변수 이름을 설정하고, required 옵션을 사용하여 필수 여부를 설정할수 있음

### @ModelAttribute
+ HTTP 요청 파라미터를 객체로 변환할때 사용
+ 파라미터 이름과 객체 필드 이름이 일치하면 자동으로 매핑되며, 별도로 설정할 수 도 있음

### @RequestBody
+ HTTP 요청 본문을 메서드의 파라미터로 전달할 때 사용
+ 요청 본문의 데이터를 객체로 변환하여 사용할 수 있으며, 설정에 따라 다른 변환기를 사용할 수 있음
