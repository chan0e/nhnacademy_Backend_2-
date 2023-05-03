###### 사진출처 NHNacademy
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
      - DB 연결 객체를 미리 생성해놓고 풀링하는 방식이기 때문에 필요한 시간과 자원소비를 줄임
      - 이를 통해 빠른 DB 연결 및 쿼리 실행이 가능해짐
      - 동시에 여러 클라이언트의 요청을. 처리하는 경우에도 안정적인 연결 유지
    - 단점
      - 라이브러리를 사용하는 방식은 코드가 복잡해지고 디버깅이 어려워질 수 있다.
      - DB 연결객체를 미리 생성해놓고 풀링하기 때문에 최초 연결 생성시간이 다소 길어질 수 있음
       
  - 전에는 DriverManager 클래스를 이용하여 직접 연결해줬음
    - 장점
      - 라이브러리 필요없음
      - 코드가 간결해지고 디버깅이 쉬움
      - 최초 연결 생성시간 빠름
    - 단점
      - DB 연결 객체를 생성할 때 마다 새로운 연결을 만들기 때문에 연결 생성 및 해제에 필요한 시간과 자원소비가 많아짐
      - 동시에 여러 클라이언트 요청을 처리하는 경우에 안정적인 연결을 유지하기 힘듦

      
