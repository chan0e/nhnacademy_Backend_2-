평가

## 기술요구사항
+ View 는 Thymeleaf 로 개발합니다.
+ Data Access Layer 는 MyBatis 또는 JPA 를 결정하여 사용합니다. 혼용하지 않습니다.
+ Spring Boot 를 사용합니다.
+ Test Code 는 작성해야 합니다. (Coverage 최대한 높게)
+ @DataJpaTest, @WebMvcTest , @SpringBootTest 를 최대한 사용합니다.


## 요구사항

### 회원관리
+ 등록된 사용자는 ID/PW 인증 및 oauth 인증으로 로그인 할 수 있습니다.
+ 회원가입은 회원 가입 버튼을 클릭해서 진행합니다.
+ 회원가입시 계정정보(id,email,password)를 입력하여 저장합니다.
+ github.com의 이메일과 동일한 경우, github.com의 oauth 인증으로도 로그인 가능합니다.

### 프로젝트
+ 사용자는 Project 를 생성할 수 있습니다.
+ Project를 생성한 사용자는 Project 의 관리자 입니다.
+ Project는 프로젝트 이름, 상태(활성, 휴면, 종료) 를 가집니다.
+ Project 관리자는 멤버를 등록할 수 있습니다.
+ Project 멤버는 회원관리에서 가입한 회원만 가능합니다.
+ Project 멤버는 자신이 속한 Project 목록만 확인할 수 있습니다.
+ Project 멤버는 Task 를 등록, 수정, 삭제 할 수 있습니다.
+ Project 멤버는 Task 의 목록 및 내용을 확인 할 수 있습니다.
+ Project 멤버는 Project 에 Tag, MileStone 을 등록, 수정, 삭제 할 수 있습니다.
+ Project 에 등록한 Tag, MileStone 을 Task에 설정 할 수 있습니다.
+ Tag : Task 에 설정할 속성입니다. Task에 1개이상의 Tag 를 설정할 수 있습니다.
+ MileStone : Project 진척 상황을 나타내는 이정표입니다. Task 에 한개의 MileStone 을 설정할 수 있습니다.
+ Tag, MileStone 는 프로젝트 멤버에 의해 삭제될 수 있으며 설정된 Task 는 Tag, MileStone이 제거됩니다.
+ Project 멤버는 Task 에 Comment 를 생성할 수 있습니다.

+ Comment 를 생성한 사용자는 Comment 를 수정, 삭제 할 수 있습니다.
+ Task-Api, Project, Task, Comment 의 구조는 다음과 같습니다.

![image](https://github.com/chan0e/nhnacademy_Backend3-/assets/94053008/624bb0d1-d902-46c0-bf7c-aea5dbe4f10d)

### 설계
![image](https://github.com/chan0e/nhnacademy_Backend3-/assets/94053008/238c3557-2b28-4d49-b098-c9e8e4949147)

+ gateway 는 모든 서비스 요청을 받으며 프레젠테이션 기능을 담당합니다.
+ TemplateEngine(Thymeleaf) 사용하여 화면을 표시합니다.
+ 데이터는 AccountApi, TaskApi 를 RestTempate으로 호출하여 받아 옵니다.
+ 화면정보를 표시할때 AccountApi, TaskApi 를 조합해서 제공할 수 있어야 합니다.
+ gateway 는 사용자의 인증을 담당합니다.
+ 인증 세션은 gateway 서버에서 redis 를 사용하여 관리합니다.
+ 인증 데이터는 Account-Api 를 사용합니다.
+ AccountApi 는 멤버의 정보를 관리합니다.
+ ProjectApi 는 Project, Task, Comment, Tag 를 관리 합니다.

### Account-api
+ 인증처리는 GateWay 에 위임합니다.
+ (RestApi) Project, Task, Comment, Tag, MileStone 정보를 관리하는 API 를 제공합니다.

### 산출물
+ ERD
+ DDL ( 데이터베이스는 ERD, DDL 과 일치해야 합니다. )
+ 실행가능한 소스코드
+ java -jar 로 실행가능해야 합니다.
+ *.http 파일 생성
+ REST-API 실행 요청 및 결과 문서


### 품질평가
+ 정적 분석기(Sonar Qube)
