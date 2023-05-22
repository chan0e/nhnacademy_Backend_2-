## Login
+ 개인이 자신을 식별하고 인증하여 컴픁 시스템에 엑세스하느 절차

## Authentication
+ 사용자의 신원을 확인하고 인증하는 과정으로, 사용자가 제공한 정보를 기반으로 신뢰성 있는 접근 권한을 부여하는 것

## 비밀번호 저장방법

### 단방향 해시 함수(One-Way Hash Function)
+ 임의의 길이를 갖는 임의의 데이터를 고정된 길이의 데이터를 매핑하는 단방향 함수
  - 일방향성
  - 고정된 출력길이
  - 충돌 저항성

+ 단방향 해시 함수의 문제점
  - 인식가능성
    + 동일한 메시지는 동일하 다이제스트를 갖음

  - 속도
    + 해시 함수의 빠른 처리속도로 인해 공격자는 매우 빠른속도로 임의의 문자열의 다이제스트와 해킹할 대상의 다이제스트를 비교할 수 있음

+ 단방향 해시 함수 보완하기
  - salt
    + 단방향 해시 함수에서 다이제스트를 생성할때 추가되는 바이트 단위의 임의의 문자열
  - Key Stretching
    + 해시 함수를 반복 적용하여 비밀번호와 같은 키를 강력하게 만들어 보안을 강화하고, 무차별 대입 공격을 어렵게 만드는 기술

+ Cookie와 Session
  - 저장 위치
    - session :  세션은 서버 측에 정보를 저장하고 관리. 고유한 세션 식별자를 클라이언트에게 제공하고 이 식별자르 통해 서벙 저장된 사용자                   데이터에 접근
    - Cookie : 쿠키는 클라이언트 측에 저장되며, 브라우저가 쿠키를 관리하고 필요에 따라 서버에 전송



### Spring-Security
+ Spring 기반 애플리케이션을 위해 선언적 보안 기능을 제공하는 프레임워크
+ Servlet Filter(Servlet 기반 애플리케이션) 및 AOP 기반
+ 

.... 중간 개념들은 좀더 공부후 작성예정....



## 인증기본 개념

### Authentication 

![image](https://github.com/chan0e/nhnacademy_Backend3-/assets/94053008/ae7f22e3-e4c1-4e27-b3bc-5b4506f754e1)



### Authorization

### SecurityContext
+ ThreadLocal에 SecurityContext저장