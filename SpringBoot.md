## SpringBoot
+ Java 기반의 오픈 소스 프레임워크로 독립적인 실행 가능한 애플리케이션을 쉽게 개발하기 위한 도구
+ 기존의 SpringFramework를 편리하게 사용할 수 있도록 해줌
+ 애플리케이션의 설정, 구성, 배포 등을 간편하게 처리할 수 있도록 도움

### 주요 특징
+ 간결한설정
  - Annotation 기반의 설정 방식을 제공하므로 XML설정 파일을 작성할 필요가 없음
+ 내장된 서버
  - Tomcat,Jetty와 같은 웹서버가 내장되어있어 웹 서버 따로 설치 필요가 없음
  - 애플리케이션을 실행하기 위해 JAR 파일을 실행하면 됨
+ 자동 구성
  - Classpath기반의 설정을 사용하여 애플리케이션의 구성을 자동으로 처리함
+ 스타터 패키지
  - 특정 기술 스택이나 기능을 지원하기 위한 의존성을 한데 묶어 미리 구성된 패키지로 스타터 패키지 개념을 제공
+ 운영환경 관리
  - 로깅,보안,모니터링 등의 운영 관련 기능을 지원
  - 애플리케이션의 구성을 외부환경 변수를 통해 설정가능

### 자동생성 코드 살펴보기 - pom.xml
#### spring-boot-starter-parent
```xml
   <parent>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-parent</artifactId>
        <version>2.7.12</version>
        <relativePath/> <!-- lookup parent from repository -->
    </parent>
```
+ 전체 프로젝트의 버전정보를 관리
+ BOM에 시루된 정보로 3rd Party 라이브러리 호환성을 보장
+ 프로젝트의 dependency에는 버전 정보를 기술하지않음

#### spring-boot-starter-{기술명}
+ 스프링의 다른 기능을 사용하고 싶으면 기술명으로 대부분 작성할 수 있음


### Annotation을 포함한 Meta Annotation
+ @EnalbeAutoConfiguration
  - 자동설정 기능을 활성화
  - claaspath에 라이브러리가 존재하면 자동으로 Bean 을 설정

+ @ComponentScan
  - basePackage하위의 컴포넌트를 스캔하여 Bean 등록

+ @SpringBootConfiguration
  - 설정된 클래스 파일은 설정(java config)으로 사용할 수 있음

+ @SpringBootApplication에 들어가보면 확인할수있다

![image](https://github.com/chan0e/nhnacademy_Backend3-/assets/94053008/dfeee2e4-6181-4788-8320-a2bd0bf6c032)



