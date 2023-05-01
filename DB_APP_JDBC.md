###### 사진출처 NHNacademy

## JDBC
+ 관계형 데이터베이스에 저장된 데이터를 접근 및 조작할 수 있게 하는 Java API
+ Java 애플리케이션에서 SQL 기반 DB와 통신가능
+ DB 종류에 상관없이 사용 가능
+ DB와의 연결, 데이터 검색, 데이터 변경, 트랜잭션 처리 등 다양한 작업 수행 가능

## JDBC 구조
![image](https://user-images.githubusercontent.com/94053008/235392787-790af12d-19ee-4a61-8304-5805c4e4372c.png)


<!-- |구성요소|설명|역할| -->

| 구성요소 | 설명 |
| ---- | --- |
| Java Application | Java 응용 프로그램, Java 웹 응용프로그램 서버|
| JDBC Driver Manager | Java 응용프로그램에서 사용하는 데이터베이스에 맞는 JDBC 드라이버 로드 |
| JDBC API | Java 응용프로그램에서 데이터베이스에 연결하고 데이터를 제어할 수 있도록 하는 데이터베이스 연결 및 제어를 위한 인터페이스/클래스|
| JDBC Driver| 데이터베이스 개발사에서 만든 데이터베이스 드라이버|

## JDBC Driver Type
+ JDBC-ODBC Bridge Type
+ Native_API / Partly Java Type
+ Net-Protocol / All-Java Type
+ Native-Protocol / All-Java Type
  - 가장 많이 사용되고 있는 형태
  - 직접 DB와 통신, 순수 Java Driver라고 불림
  - Native Library 및 미들웨어 서버가 필요하지 않음
  - 가장 좋은 성능
![image](https://user-images.githubusercontent.com/94053008/235394380-850fc28c-aa59-41eb-9015-1ac5f747d01f.png)

## JDBC 아키텍쳐
+ 2-Tier 아키텍쳐
  - 클라이언트와 서버로 구분
  - 클라이언트는 사용자 인터페이스와 비즈니스 로직을 담당하고, 서버는 데이터베이스를 담당
  
+ 3-Tier 아키텍쳐
  - 클라이언트, 애플리케이션서버, 데이터베이스 서버로 구분
  - 애플리케이션 서버는 클라이언트와 데이터베이스 서버 사이에서 비즈니스 로직을 처리


## java.sql 패키지
![image](https://user-images.githubusercontent.com/94053008/235394665-4d79054f-ecaa-46f3-b9f6-5b9c18e714d7.png)


## Tier Vs Layer
+ Tier
  - 일반적으로 시스템을 물리적인 측면에서 구분하는 방법

+ Layer
  - 소프트웨어 아키텍처에서 각 계층이 수행하는 작업에 따라 구분하는 방법(논리적인 방법)
  - Presentation Layer, Business Layer, Data Access Layer와 같이 3개의 계층으로 구성
  - Presentation Layer는 사용자와 상호작용하는 UI를 담당하며, Business Layer는 비즈니스 로직을 담당하고, Data Access Layer는 데이터베이스와 상호작용하는 코드를 담당
 


