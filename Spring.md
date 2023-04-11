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

```java
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
