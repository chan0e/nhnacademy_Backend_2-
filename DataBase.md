### 데이터베이스 개요

+ 데이터(Data)

  현실 세계로부터 단순한 관찰이나 측정을 통해서 수집된 사실이나 값
  
+ 정보(Information)

  어떤 상황에 대한 적절한 의사 결정을 할 수 있게하는 지식으로서 유효한 데이터의 해석 또는 데이터간의 관계
  
+ 정보는 데이터를 처리해서 얻어진 결과

### 데이터 베이스
+ 같은 데이터가 다른 목적을 가진 여러 응용에 중복되어 사용될 수 있다는 공용 개념의 기초
  - 통합된 데이터(Integerated Data)
  - 저장된 데이터(Stored Data)
  - 운영 데이터(Operational Data)
  - 공용 데이터(Shared Data)


+ 통합 저장된 운영 데이터로서의 특징
  - 실시간 접근성(Real-time Accessibility)
  - 지속적인 변화(Continuous Evolution)
  - 동시 사용(Concurrency Sharing)
  - 내용 참조(Content Reference)


### 데이터베이스 관리 시스템(DBMS, Database Management System)

+ 데이터의 방대한 집합체를 유지 관리하고 이용하는데 도움을 주도록 설계된 소프트웨어
+ 데이터의 종속성과 중복성의 문제를 해결하기 위해 제안된 시스템 

![image](https://user-images.githubusercontent.com/94053008/226253719-47b1568e-ca6b-4189-8ec3-572002e4e9ee.png)

(사진출처 - NHN academy)

### 데이터베이스 관리 시스템의 기능

+ 데이터 정의 기능
  - 데이터 모델과 데이터베이스를 물리적 저장 장치에 저장하는데 필요한 명세 포함
  - 논리적 구조와 물리적 구조의 매핑을 명세
  
+ 데이터 조작 기능
  - 사용자와 데이터베이스 사이의 인터페이스를 위한 수단 제공
  
+ 데이터 제어 기능
  - 데이터의 갱신, 삽입, 삭제 작업이 정확히 실행되며, 무결성 제공
  - 보안과 권한 검사
  - 동시 사용자에 대한 병행성 제어


#### 데이터 모델

![image](https://user-images.githubusercontent.com/94053008/226254629-d09cbdc5-f07d-4f80-be5d-ec830b26d333.png)

+ 데이터 또는 정보를 설명하기 위한 표기법
  - 데이터의 구조(Structure of the Data)
  - 데이터에 대한 작업(Operations on the Data)
  - 데이터에 대한 제약 조건(Constraints on the Data)

+ 주요 데이터 모델
  - 관계 데이터 모델(Relational Data Model)
  - 반정형 데이터 모델(Semi-Structured-data Model)
 
 
 
 #### 트랜잭션(ACID)
 
 + Atmoicity
 + Consistency
 + Isoloation
 + Durability


 

