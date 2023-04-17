###### 사진출처 nhnacademy

## Framework 
+ 일정한 형태의 틀, 부품을 가지고 다양한 형태의 결과물을 만드는것

## Library
+ 소프트웨어를 개발하기 쉽게 어떤 기능을 제공하는 도구들


### Framework VS Library
<img width="585" alt="image" src="https://user-images.githubusercontent.com/94053008/230803567-916966cb-e437-44dd-b73a-5be1bfac0b87.png">

+ 공통점 
  - 특정 문제를 일방적인 방법으로 해결하기위한 코드 제공
  - 재활용

### Framework를 쓰는 이유
  + 기능적 요구사항과 비기능적 요구사항
  + 반복되는 기능
  + 빠른 개발


## Spring Framework
+  자바 엔터프라이즈 개발을 편하게 해주는 오픈소스 애플리케이션 프레임워크

### Spring Framework 특징
+ 경량 컨테이너로서 Spring Bean을 직접 관리
  - Spring Bean 이란 Spring IOC Container가 관리하는 자바 객체로서 Container에 의해 생명주기 관리되는 객체
  - Container Spring Bean 객체의 생성, 보관, 제거에 관한 모든일을 처리

+ POJO(Plain Old Java Object) 기반의 FrameWork
  - 특정한 인터페이스를 구현하거나 상속을 받을 필요가 없음

#### 제어 역전(IoC: Inversion of Control)
  + 제어의 주도권이 개발자가 아니라 FrameWork에 있어 필요에 따라 Spring에서 사용자의 코드를 호출한다.
  + 의존성 주입(DI: Dependency Injection)

#### 관점 지향 프로그래밍(AOP: Aspect-Oriented Programming) 을 지원
  + 복잡한 비지니스 영역의 문제와 공통된 지원 영역의 문제를 분리

#### 영속성과 관련된 다양한 서비스 지원

#### 전자정부 표준 프레임워크를 따름


## Spring Inversion of Control
### IoC(제어 역전)
  + 제어권을 프레임워크가 갖음 -> 개발자는 제어권이 없음 -> Control is Inversion
  + 제어
    - 프로그램의 흐름
    - 객체의 생성
  + IoC 관점에서 각자의 역할
    - 개발자는 프레임워크가 제공하는 설정방법을 사용하여 코드를 설정
    - 프레임워크는 이 설정을 보고 객체를 생성하고 코드가 동작하는 순서를 결정하여 실행


## Spring Bean
+ Name, Type, Object로 구성되어있음
+ Spring Framework에서 중요하게 관리하는 객체로 이해


## ApplicationContext
+ 애플리케이션에 구성 정보를 제공하기 위한 Spring 애플리케이션 내의 중앙 인터페이스

### 기능
+ 애플리케이션 구성요소에 액세스하기 위한 Bean Factory 메소드
+ 일반적인 방식으로 파일 리소스를 로드하는 기능
+ 등록된 리스너에 이벤트를 게시하는 기능
+ 국제화를 지원하기 위해 메시지를 해석하는 기능
+ 상위 컨텍스트에서 상속기능

## 의존성(Dependency)
+ 코드에서 두 모듈간의 연결, 관계
	- 의존관계(Dependency)
	  - A class가 B class를 일시적으로 참조하는 형태 

``` java
public class B {
    private int numB;
    
    public int getNumB() {
      return this.numB;
    }
}

public class A {
    private int numA;
    
    // add 메소드가 반환한 이후에는 B 클래스의 b 객체는 제거된다. 
    public int add(B b) {
      return numA + b.getNumB();
    }
}
```

- 연관관계(Association)
  - 클래스 필드로 다른 클래스의 객체를 가지고 있는 관계
``` java
public class B {
    private int numB;
    
    public int getNumB() {
      return this.numB;
    }
}

public class A {
    private int numA;
    private B b;
    
    // add 메소드가 반환한 이후에도 B 클래스의 b 객체는 여전히 남아 있다.
    public int add() {
      return numA + this.b.getNumB();
    }
}

```

  
- 집합관계(Aggregation)
  - 클래스 A와 클래스 B의 생명주기가 일치하지않는다

``` java
public class B {
    private int numB;
    
    public int getNumB() {
      return this.numB;
    }
}

public class A {
    private int numA;
    private B b;
    
    public A(B externalB) {
        this.b = externalB;
    }
}
```

- 합성관계
  - 클래스 A와 클래스 B의 생명주기가 일치한다
```java
public class B {
}

public class A {
    private B b;
    
    public A() {
        this.b = new B();
    }
}
```

## 의존성 주입(Dependency Injection)
+ DI
   - Ioc 의 패턴중에 하나
   - Object 간의 의존성을 낮춘다
   - 외부에서 객체르 생성하고 전달한다


### Dependency Inversion Princlple

![image](https://user-images.githubusercontent.com/94053008/231049905-21741e44-1db6-43e4-8b9b-0ef603a061bf.png)


+ 상위 모듈이 하위 모듈에 의존관계를 가지지 않도록 구현해야 한다
+ 추상클래스는 그 구현체의 내용에 의존관계를 가지지않는다
+ 구현체가 추상클래스에 의존관계르 가질수있다

### Spring framework Dependency Injection(Bean Wiring) 방법
+ Contructor Injection
+ Setter Injection
+ Field Injection

#### Bean값 얻기

```java

 try (ClassPathXmlApplicationContext context = new ClassPathXmlApplicationContext("beans.xml")) {
            GreetingService service = context.getBean("greetingService", GreetingService.class);
            service.greet();
       }
```


#### Contructor Injection
+ 생성자 주입 방식을 사용하여 , GreetingService 스프링 빈에 Greeter 스프링 빈을 주입하는 예제

```java
// 생성자 주입 방식을 사용하므로, 주입 대상 스프링빈에 적절한 생성자가 필요하다.
    public GreetingService(Greeter greeter) {
        this.greeter = greeter;
    }
```

``` java
  <bean id="greetingService" class="com.nhnacademy.edu.springframework.greeting.GreetingService" >
        <constructor-arg ref="koreanGreeter" />
    </bean>

```

#### Setter Injection
+ setter method를 이용하여 의존성 주입

``` java
//    final keyword 이므로 객체를 생성한뒤 greeter 변수에 값을 할당할 수 없다.
//    private final Greeter greeter;
    private Greeter greeter;

//    Setter Injection 기본 생성자가 필요하다.
    public GreetingService() {
    }
    
    public void setGreeter(Greeter greeter) {
        System.out.println("setGreeter invoked!");
        this.greeter = greeter;
    }
```


``` java
 <bean id="greetingService" class="com.nhnacademy.edu.springframework.greeting.GreetingService" >
        <property name="greeter" ref="koreanGreeter" />
    </bean>
```

#### Autowired Injection
+ autowired 속성을 사용하여 자동으로 주입
+ autowired injection 의 방식
	- byType
	- byName
	- contructor


#### byType
``` java
<!--    byType으로 autowire 를 하려면 해당되는 type 의 bean 이 1개만 존재해야 합니다.-->
<!--    <bean id="englishGreeter" class="com.nhnacademy.edu.springframework.greeting.service.EnglishGreeter" scope="singleton">-->
<!--    </bean>-->

    <bean id="koreanGreeter" class="com.nhnacademy.edu.springframework.greeting.service.KoreanGreeter" scope="prototype">
    </bean>

    <bean id="greetingService" class="com.nhnacademy.edu.springframework.greeting.GreetingService" autowire="byType">
    </bean>

```


#### byName

```xml
   <bean id="englishGreeter" class="com.nhnacademy.edu.springframework.greeting.service.EnglishGreeter" scope="singleton">
    </bean>

    <bean id="koreanGreeter" class="com.nhnacademy.edu.springframework.greeting.service.KoreanGreeter" scope="prototype">
    </bean>

     <!-- 관례적으로 set~ 하고 id 첫번째 문자를 대문자로 바꿔서 매핑해준다. 따라서 맨처음 알파벳은 소문자로 해줘야 함 이유는 관례적인것...   -->
    <bean id="greetingService" class="com.nhnacademy.edu.springframework.greeting.GreetingService" autowire="byName">
    </bean>
```

```java
public class GreetingService {
    private Greeter greeter;

    public void setKoreanGreeter(Greeter greeter) {
        System.out.println("setGreeter invoked!");
        this.greeter = greeter;
    }

    // 기본 생성자가 필요하기 때문에 아래는 주석처리
//    public GreetingService(Greeter greeter) {
//        this.greeter = greeter;
//    }

    public void greet() {
        greeter.sayHello();
    }
}
```

## Dependency Injection (Annotation)
- XML 방식으로 Bean 의존성 주입을 Annotation으로 구현

### Annotation 기반 설정
+ Annotation을 사용하려면 xml에 설정을 해줘야함

```xml
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xmlns:context="http://www.springframework.org/schema/context"
       xsi:schemaLocation="
        http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd
        http://www.springframework.org/schema/context http://www.springframework.org/schema/context/spring-context.xsd">

    <!-- annotation설정을 위해 추가-->
    <context:annotation-config/>

```

### @Required
+ 반드시 의존성이 주입되어야 함을 강제하는 Annotation
+ spinrg framework 5 부터는 deplicated 되었지만 Legacy 어플리케이션에서는 사용할수 있음

### @Autowired
+ @Target에 정의된 위치에 @Autowired Annotation을 사용할 수 있음
+ 필요한 의존 객체의 “타입"에 해당하는 빈을 찾아 주입함
	- 생성자, setter, 필드



### @Qualifier
+ @Qualifier를 지정하여 Bean의 이름을 의존성을 주입 할수 있음

```java
public class GreetingService {

    private final Greeter greeter;

    @Autowired
    public GreetingService(@Qualifier("englishGreeter") Greeter greeter) {
        this.greeter = greeter;
    }

    public boolean greet() {
        // 인터페이스의 메소드를 호출하지만 실제 구현 객체의 메소드가 실행됩니다.
        return greeter.sayHello();
    }
}

```

### @Value
+ 외부 속성을 주입하기 위해 사용
+ ex) greeter.properties에 from=Manty 라는 값이 있으면 
 Annotation을 이용해 value 값을 가져올수 있음

```java
@Value("${from}")
private String from;

```

## Java Configuration
- xml로 설정을 대체하여 java 클래스를 이용해 설정

### Bean 생성
``` java
@Configuration
public class JavaConfig {
    @Bean/*(name = "dbms")*/
    public String dbms() {
        return new String("MYSQL");
    }
}
```

+ 위의 설정은 다음의 XML 설정과 동일

``` xml
<bean id="dbms" class="java.lang.String">
        <constructor-arg type="java.lang.String" value="MYSQL" />
  </bean>

```

+ 또다른 방법
``` java
public interface BaseJavaConfig {
    @Bean
    default String dbms() {
        return new String("MYSQL");
    }
}

@Configuration
public class JavaConfig implements BaseJavaConfig{
}
```



### Bean 가져오기
#### AnnotationConfigApplicationContex
+ 생성자 파라미터로 받을수 있는 클래스
	- @Configuration 설정한 클래스
	- @Component 설정한 클래스

```java
 AnnotationConfigApplicationContext context =
                new AnnotationConfigApplicationContext("com.nhnent.edu.spring.greeting");
```



### Copponent Scan
+ @Configuration을 지정한 클래스에 @ComponentScan을 설정항 스캐닝을 활성화 할 수 있음

```java
@Configuration
@ComponentScan(basePackages = "com.nhnacademy.edu.springframework.greeting")
public class BeanConfig {
  // .. 생략 ..
}

``

## AOP(Aspect Oriented Programming)
 - 관점 지향은 어떤 로직을 기준으로 핵심적인 관점, 부가적인 관점으로 나누어서 보고 그 관점을 기준으로 모듈화
	 - crosscutting concerns: 횡단 관심사
	 - core concerns : 주요관심사



<img width="791" alt="image" src="https://user-images.githubusercontent.com/94053008/231341547-0f757143-c7cb-41ca-b291-edb0b1263bc9.png">

### AOP 주요 용어

#### Aspect
+ 하나 이상의 Pointcut과 Advice의 조합으로 만들어지는 AOP의 기본 모듈
+ Spring Framework 에서는 @Aspect를 사용하거나 XML에서 설정할 수 있음

#### Join point
+ 프로그램 실행 중의 어떤 포인트를 의미(method 실행, Exception 처리)
+ Pointcut의 후보라고 생각
+ Spring AOP 에서는 method 실행만 대상

#### Advice
+ Target에 제공할 부가기능을 담은 모듈
+ 특정 Join Point 에서 Aspect가 취하는 행동
	- ex) around, before, after

#### Pointcut
+ Advice를 적용할 Join Point를 선별하는 작업 또는 그 기능을 적용한 모듈
+ Advice는 Pointcut 표현식과 연결되고 Pointcut이 매치한 Join Point에서 실행

#### Target Object
+ 부가기능을 부여할 대상
+ 하나 이상의 Aspect로 advised 객체
+ advised object라고 부르기도함

#### Weaving
+ 다른 어플리케이션 타입이나 어드바이즈된 객체를 생성하는 객체와 관점을 연결하는 행위

![image](https://user-images.githubusercontent.com/94053008/231343736-908650b6-e048-4adc-81f7-19e52c9d5b9a.jpeg)


## Spring AOP vs @AspectJ
+ Spring Top
	- AOP 개념을 스프링 빈에 적용하기 위한것
	- Spring Bean 대상이므로 ApllicationContext가 처리
	- RunTime-Weaving
+ AspectJ
	- AOP개념을 모든 객체에 적용하기 위한것
	- 컴파일 시점, 로드시점 Weaving

### Spring AOP 설치

``` xml

<dependency>
        <groupId>org.springframework</groupId>
        <artifactId>spring-aspects</artifactId>
        <version>5.3.15</version>
    </dependency>
```


### @AspectJ (Annotation) 지원
+ 일반 java에 Annotation으로 설정하는 방식

```java

@Configuration
@EnableAspectJAutoProxy
public class AppConfig {

}
```

+ xml 설정에서 @AspectJ 지원을 활성화 하기위한 설정

```xml
<aop:aspectj-autoproxy/>
```

### Aspect 선언
+ AspectJ 지원이 활성화 된 상태에서 Bean으로 선언하고 @Aspect 로 설정하면
해당 spring-bean은 aspect가 된다.

```java

 @Aspect
@Component
public class LoggingAspect {
...
}
```

### 사용 요약

![image](https://user-images.githubusercontent.com/94053008/231343812-f1a33397-4271-4ff6-8904-8866b1ca75df.png)

### Point Cut
+ Target의 여러 Joinpoint 중에 advise를 적용할 대상을 지정하는 keyword
+ Spring AOP는 Spring-Bean의 method 실행 joinPoint만 지원

```java
@Pointcut("execution(* transfer(..))") // the pointcut expression
private void anyOldTransfer() {} // the pointcut signature
```

### Pointcut 지정자

#### execution
+ 메소드 실행 조인포인트와 매칭
+ 스프링 AOP의 주요 포인트컷 지정자

#### within
+ 주어진 타입(클래스)으로 조인 포인트 범위를 제한

#### this
+ 주어진 타입을 구현한 스프링 AOP Proxy 객체에 매칭
+ 보통 Proxy 객체를 Advice 파라미터에 바인딩하는 용도로 쓰임

#### target
+ 주어진 타입을 구현한 타겟 객체에 매칭
+ 보통 타겟 객체를 Advice 파라미터에 바인딩하는 용도로 쓰임

#### args
+ 주어진 타입의 인수들을 이용해 매칭
+ 보통 메소드 인자를 Advice 파라미터에 바인딩하는 용도로 쓰임

#### 위의 용어들에 @를 붙이면 각 뜻에 맞게 매칭 시킴

### 포인트 컷 - 조합
+ 포인트컷 표현식은 &&, ||, ! 으로 조합 가능


```java
// anyPublicOperation 포인트컷은 모든 public 메소드 실행에 매칭 됩니다.
@Pointcut("execution(public * *(..))")
private void anyPublicOperation() {} 

// inTrading 포인트컷은 com.xyz.myapp.trading 패키지 내의 메소드 실행에 매칭
@Pointcut("within(com.xyz.myapp.trading..*)")
private void inTrading() {} 

// tradingOperation 포인트컷은 com.xyz.myapp.trading 패키지 내의 퍼블릭 메소드 실행에 매칭
@Pointcut("anyPublicOperation() && inTrading()")
private void tradingOperation() {} 
```

### 포인트컷 - 표현식 예제
+ Spring AOP는 주로 execution 포인트컷 지정자를 사용
```
execution(modifiers-pattern? ret-type-pattern declaring-type-pattern?name-pattern(param-pattern) throws-pattern?)

```

+ 모든 public 메소드
```
execution(public * *(..))
```
+ get~ 으로 시작하는 모든 메소드
```
execution(* get*(..))
```
+ com.nhnent.edu.spring_core 패키지에 있는 모든 메소드
```
execution(* com.nhnent.edu.spring_core.*.*(..))
```
+com.nhnent.edu.spring_core.service.MemberService 인터페이스에 정의된 모든 메소드
```
execution(* com.nhnent.edu.spring_core.service.MemberService.*(..))
```
+ com.nhnent.edu.spring_core.service 패키지의 모든 메소드실행
```
within(com.nhnent.edu.spring_core.service.*)
```
+ TestService 프록시 구현체의 메소드 실행
```
this(com.nhnent.edu.spring_core.service.TestService)
```
+ TestService 인터페이스의 구현 객체의 메소드 실행
```
target(com.nhnent.edu.spring_core.service.TestService)
```
+ 런타임에 Serializable 타입의 단일 파라미터가 전달되는 메소드 실행 (인자값 검사 기능에 많이 사용됩니다.)
```
args(java.io.Serializable)
```
+ @Transactional 어노테이션을 가진 모든 타겟 객체의 메소드 실행
```
@target(org.springframework.transaction.annotation.Transactional)
```

## Advice

+ advice는 포인트컷과 관련하여 메소드 실행 전, 후, 전/후를 결정하기위해 사용

![image](https://user-images.githubusercontent.com/94053008/231468353-f076340b-2544-4174-a100-67ed67b9e168.png)


### @Around advice
+ Object를 반환해야 하고 첫번째 인자는 ProceedingJoinPoint 여야 함
+ pjp의 proceed를 호출하면 타겟메소드가 실행됨

``` java
@Aspect
public class AroundExample {

    @Around("com.xyz.myapp.CommonPointcuts.businessService()")
    public Object doBasicProfiling(ProceedingJoinPoint pjp) throws Throwable {
        // start stopwatch
        Object retVal = pjp.proceed();
        // stop stopwatch
        return retVal;
    }
}
```


![image](https://user-images.githubusercontent.com/94053008/231468110-82e1b35c-c023-4170-8d14-b92a6da19fc3.png)
