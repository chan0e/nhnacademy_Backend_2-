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
