###### 사진출처 NHNacademy

## JDBC
+ 관계형 데이터베이스에 저장된 데이터를 접근 및 조작할 수 있게 하는 Java API
+ Java 애플리케이션에서 SQL 기반 DB와 통신가능
+ DB 종류에 상관없이 사용 가능
+ DB와의 연결, 데이터 검색, 데이터 변경, 트랜잭션 처리 등 다양한 작업 수행 가능

## JDBC 구조
![image](https://user-images.githubusercontent.com/94053008/235392787-790af12d-19ee-4a61-8304-5805c4e4372c.png)


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

## Tier Vs Layer
+ Tier
  - 일반적으로 시스템을 물리적인 측면에서 구분하는 방법

+ Layer
  - 소프트웨어 아키텍처에서 각 계층이 수행하는 작업에 따라 구분하는 방법(논리적인 방법)
  - Presentation Layer, Business Layer, Data Access Layer와 같이 3개의 계층으로 구성
  - Presentation Layer는 사용자와 상호작용하는 UI를 담당하며, Business Layer는 비즈니스 로직을 담당하고, Data Access Layer는 데이터베이스와 상호작용하는 코드를 담당
 
 
## java.sql 패키지
![image](https://user-images.githubusercontent.com/94053008/235394665-4d79054f-ecaa-46f3-b9f6-5b9c18e714d7.png)

## java.sql 객체 설명

+ DriverManager
  - JDBC 드라이버 로딩, 연결 및 끊기 등의 작업을 처리하는 클래스
 
+ Connection
   - 데이터베이스와 연결을 맺는 객체로, Statement와 PreparedStatement 객체를 생성하기위한 기반 객체
      - createStatement() 메서드를 사용해 Statement 인터페이스를 구현하는 새로운 객체를 반환함

+ Statement
  - SQL 쿼리문을 실행하고 반환하는 객체로 일반적인 쿼리 실행에 사용됨
      - executeQuery()
          + select 쿼리 수행
          + ResultSet 객체 반환
      - executeUpdate()
          + insert / update / delete 쿼리 수행
          + 성공 여부나 영향 받은 투플의 수를 int 타입으로 반환

+ PreparedStatement
  - 미리 컴파일된 SQL 쿼리문을 실행하고 결과를 반환하는 객체
  - 동적으로 쿼리를 생성할 필요가 없으므로 보안성과 성능이 뛰어남
    - setint(int parameterindex, int value), setString(...), setDate(...), setNull(...)....와 같은 값을 넣는 메소드 

+ CallableStatement
  - 저장 프로시저를 호출하기 위해 사용
  - IN, OUT, INOUT 파라미터를 

+ ResultSet
  - 쿼리 실행 결과를 담는 객체로 데이터를 반복해서 처리할 수 있음

## 사용순서
1. 드라이버를 로드
2. Connection 객체를 통해 연결
3. Statement/PreparedStatement/CallableStatement 객체를 통해 명령을 내림
4. 명령 수행으로 반한되는 결과가 있으면 ResultSet객체로 반환받고 반환받은 결과를 이용함
5. 객체들을 순서대로 close 해줌


> 예제코드
```java
private static final String driverName = "com.mysql.cj.jdbc.Driver";
    private static final String databaseURL = "jdbc:mysql://localhost/TEST";
    private static final String userNmae = "admin";
    private static final String userpwd = "1234";


    Connection connection = null;
    Statement statement = null;
    ResultSet resultSet = null;

    public void connect() {
        try {
            Class.forName(driverName);
            connection = DriverManager.getConnection(databaseURL, userNmae, userpwd);
            statement = connection.createStatement();
            String sqlQuery = "select * from emp";

            resultSet = statement.executeQuery(sqlQuery);

            while (resultSet.next()) {
                System.out.print(resultSet.getInt(1) + " ");
                System.out.print(resultSet.getString(2) + " ");
                System.out.print(resultSet.getString(3) + " ");
             
                System.out.println();

            }
            resultSet.close();
            connection.close();
            resultSet.close();

        } catch (Exception e) {
            // TODO: handle exception
            e.printStackTrace();
        }

```

### Statement와 PreparedStatement 차이점
+ 컴파일 방식의 차이
  -  Statement는 매번 실행 시에 sql 쿼리문을 실행
  -  PreparedStatements는 처음 실행 시에 sql 쿼리문을 컴파일한 이후에는 컴파일 없이 캐시에서 재사용함
  -  따라서 PreparedStatement를 사용하면 실행 속도가 더 빠름

+ 코드 가독성의 차이
  - PreparedStatement는 sql 쿼리문에 '?' 와 같은 placeholder를 사용하여 값을 나중에 채움
  - 반면 Statement는 sql 쿼리문 안에 값을 포함하여 작성해야함
  - 따라서, PreparedStatement를 사용하면 코드 가독성이 더 좋아짐

+ SQL Injection 공격 대체 방식의 차이
  - PreparedStatement는 쿼리문에 값이 들어가는 부분을 placeholder로 처리하기 때문에 공격에 이용되는것을 막음
  - 반면 Statement는 사용자 입력값이 쿼리문에 그대로 들어가기 때문에 sql 인젝션 공격에 노출될수 있음
  
## CRUD 개요
+ Create, Read, Update, Delete
+ 대부분의 컴퓨터 소프트웨어가 가지는 기본적인 데이터 처리 기능
+ 유사 용어
  - ABCD : Add, Browse, Change, Delete
  - ACID : Add, Change, Inquire, Delete
  - BREAD : Browse, Read, Edit, Add, Delete
  - VADE(R) : View, Add, Delete, Edit(트랜잭션에서 Restore 추가)
  - SIUD : Select, Insert, Update, Delete


# DataSource
+ DriverManager는 DB와의 연결을 위해 상세한 정보를 요구
+ DB와 같은 데이터 저장소에서 데이터를 읽고 쓰는데 사용되는 객체
+ DB 연결관리, 트랜잭션관리, 쿼리 실행 및 결과 처리 등의 작업을 담당
+ 연결된 DataSource는 Connection Pooling을 제공


![image](https://user-images.githubusercontent.com/94053008/235813025-850891ea-c7ee-4f2e-b45c-75ecc453c926.png)



## ConnectionPool
+ DB connection을 관리하는 객체
+ DB connection을 재사용하고 관리하여 애플리케이션의 성능을 최적화함
+ 문제는 DB 연결을 생성하고 유지하는것에 비용이 많이 듦
  - 재사용 가능한 연결 풀을 만들어 DB 연결 수를 최소화


> 연습코드
```java
import java.sql.Connection;
import java.sql.ResultSet;
import java.sql.Statement;

import org.apache.commons.dbcp2.BasicDataSource;

public class App {
    public static void main(String[] args) throws Exception {
        BasicDataSource basicDataSource = new BasicDataSource();

        try {
            basicDataSource.setDriverClassName("com.mysql.cj.jdbc.Driver");
            basicDataSource.setUrl("jdbc:mysql://localhost/Module06");
            basicDataSource.setUsername("root");
            basicDataSource.setPassword("****");
            
            System.out.println("connection success");
        } catch (Exception e) {
            // TODO: handle exception
            e.printStackTrace();
        }

        Connection conn = basicDataSource.getConnection();
        Statement statement = conn.createStatement();
        
        String sql = "select * from flight";
        ResultSet result = statement.executeQuery(sql);

        while(result.next()){
            System.out.print(result.getInt(1));
            System.out.print(result.getInt(2));
            System.out.print(result.getString(3));
            System.out.print(result.getString(4));
            System.out.print(result.getInt(5));
            System.out.println();
        }
        conn.close();
        
    }
}

```

+ 필요한 라이브러리로 commons-dbcp2,loggin,pool2,mysql-connector-j.jar이 필요함

## Apache Commons DBCP 
+ DB 연결관리 방식
  - 데이터베이스 연결을 풀링하는 방식
    - 장점
      + DB 연결 객체를 미리 생성해놓고 풀링하는 방식이기 때문에 필요한 시간과 자원소비를 줄임
      + 이를 통해 빠른 DB 연결 및 쿼리 실행이 가능해짐
      + 동시에 여러 클라이언트의 요청을. 처리하는 경우에도 안정적인 연결 유지
    - 단점
      + 라이브러리를 사용하는 방식은 코드가 복잡해지고 디버깅이 어려워질 수 있다.
      + DB 연결객체를 미리 생성해놓고 풀링하기 때문에 최초 연결 생성시간이 다소 길어질 수 있음
       
  - 전에는 DriverManager 클래스를 이용하여 직접 연결해줬음
    - 장점
      + 라이브러리 필요없음
      + 코드가 간결해지고 디버깅이 쉬움
      + 최초 연결 생성시간 빠름
    - 단점
      + DB 연결 객체를 생성할 때 마다 새로운 연결을 만들기 때문에 연결 생성 및 해제에 필요한 시간과 자원소비가 많아짐
      + 동시에 여러 클라이언트 요청을 처리하는 경우에 안정적인 연결을 유지하기 힘듦

      






