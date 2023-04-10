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

