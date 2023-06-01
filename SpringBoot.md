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


### Dependency Injection 방식 3가지
+ 생성자 주입
  - 생성자르 선언하면 인자에 객체 주입
  - 권장하는 방식

```java
   private final StudentRepository studentRepository;

    public NhnStudentService(StudentRepository studentRepository) {
        this.studentRepository = studentRepository;
    }
```
+ @Autowired
  - 클래스 변수에 Annotation을 설정항 객체 주입

```java
  @Autowired
    private StudentRepository studentRepository;

```
+ Setter
  - setter 메서드를 선언항 객체 주입

```java
@Autowired
    private StudentRepository studentRepository;

    public void setStudentRepository(StudentRepository studentRepository) {
        this.studentRepository = studentRepository;   
    } 
```

### Mysql 사용
#### 실습
+ mysql에 데이터를 저장하도록함
+ mysql은 docker , 원격 등 으로 실행

#### Mysql준비 -> docker

+ ARM 기반 (저자는 m2 맥북기준) 설치가 안되어있다면 다음 과정을 따라야 함
```
1. brew install --cask docker 입력
2. 도커 컨테이너 실행
3. docker run --platform linux/amd64 --name edu-mysql -e MYSQL_ROOT_PASSWORD=test -d -p3306:3306 mysql:5.7.35
4. docker exec -it edu-mysql bash
5. mysql -u root -p
6. 비밀번호 test 입력
7. create database student_test;
```

+ Mysql 실행
```
$ docker run --name edu-mysql -e MYSQL_ROOT_PASSWORD=test -d -p3306:3306 mysql:5.7.35 --character-set-server=utf8 --collation-server=utf8_general_ci
```

```
$ docker run --platform linux/amd64 --name edu-mysql -e MYSQL_ROOT_PASSWORD=test -d -p3306:3306 mysql:5.7.35 --character-set-server=utf8 --collation-server=utf8_general_ci
```

+ 접속 테스트
```
$ mysql -u root -p -P3306 -h 127.0.0.1
```
+ DB 생성
```
mysql> create database student_test;
```

#### dependency 추가

+ mysql-connector-java 추가
```
<dependency>
    <groupId>mysql</groupId>
    <artifactId>mysql-connector-java</artifactId>
    <version>5.1.48</version>
</dependency>
```

#### application.properties 설정
+ JPA 테이블 생성 및 SQL 로깅
```properties
spring.jpa.generate-ddl=true 
spring.jpa.show-sql=true
```

+ datasource
```properties
spring.datasource.driver-class-name=com.mysql.jdbc.Driver
spring.datasource.url=jdbc:mysql://localhost:3306/student_test?useSSL=false&serverTimezone=UTC&characterEncoding=UTF-8

spring.jpa.hibernate.naming.physical-strategy=org.hibernate.boot.model.naming.PhysicalNamingStrategyStandardImpl

spring.datasource.username=root
spring.datasource.password=test

```

### RestApi 개발
...

### Spring-Boot-view-template

#### Thymeleaf의 사용 -> html 렌더링
```xml
<dependency>
 <groupId>org.springframework.boot</groupId>
 <artifactId>spring-boot-starter-thymeleaf</artifactId>
</dependency>
```

+ properties
```properties
spring.thymeleaf.enabled=true
spring.thymeleaf.prefix=classpath:/templates/main/
spring.thymeleaf.suffix=.html
```

### Dependency management

![image](https://github.com/chan0e/nhnacademy_Backend3-/assets/94053008/caa6a092-d441-4712-ba3f-339012f8cebe)

### @Conditional
+ Spring Framework 4.0 부터 제공
+ 설정된 모든 Condition 인터페이스의 조건이 true인 경우 동작

#### @ConditionalOnXXX (1)
+ spring-boot 가 제공하는 @Conditional의 확장

![image](https://github.com/chan0e/nhnacademy_Backend3-/assets/94053008/5c4bc303-425a-40f8-83df-f6af789e31c6)

#### @ㅊ







