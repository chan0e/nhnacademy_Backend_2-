###### JPA 실습은 h2 db를 사용함

## JPA(Java Persistence API)
+ 자바 애플리케이션과 관계형 데이터베이스 간의 데이터를 영속적으로 저장하고 검색하기 위한 자바표준 ORM
+ 객체 지향 애플리케이션의 데이터와 관계형 데이터베이스의 데이터를 매핑하여 객체와 테이블간의 변환 작업을 자동으로 처리
+ 여러가지 ORM 프레임워크의 표준 인터페이스로서 대표적으로 Hibernate, EclipseLink 등과 같은 구현체가 있음

+ 특징 및 장점
   - 객체와 데이터베이스 간의 매핑을 자동으로 처리해줌으로써 생산성을 향상
   - 객체 지향 개념을 그대로 유지하며 데이터를 조작할 수 있어 개발자의 코드 이해도를 높임
   - DB에 종속되지않는 플랫폼 간 이식성을 제공
   - 성능 최적화 기능을 제공하여 효율적인 데이터 액세스를 가능하게 함
   
   
   
   
## Spring + JAP 설정
+ @EnableJpaRepositories 어노테이션을 

```java
@EnableJpaRepositories(basePackageClasses = RepositoryBase.class)
@Configuration
public class JpaConfig {
    @Bean
    public LocalContainerEntityManagerFactoryBean entityManagerFactory(DataSource dataSource) {
        LocalContainerEntityManagerFactoryBean emf = new LocalContainerEntityManagerFactoryBean();
        emf.setDataSource(dataSource);
        emf.setPackagesToScan("com.nhnacademy.springjpa.entity");
        emf.setJpaVendorAdapter(jpaVendorAdapters());
        emf.setJpaProperties(jpaProperties());

        return emf;
    }


    //어떤 db를 쓸지 결정해줌
    private JpaVendorAdapter jpaVendorAdapters() {
        HibernateJpaVendorAdapter hibernateJpaVendorAdapter = new HibernateJpaVendorAdapter();
        hibernateJpaVendorAdapter.setDatabase(Database.H2);

        return hibernateJpaVendorAdapter;
    }


    //hibernate 속성값을 지정해줌
    private Properties jpaProperties() {
        Properties jpaProperties = new Properties();
        jpaProperties.setProperty("hibernate.show_sql", "false");
        jpaProperties.setProperty("hibernate.format_sql", "true");
        jpaProperties.setProperty("hibernate.use_sql_comments", "true");
        jpaProperties.setProperty("hibernate.globally_quoted_identifiers", "true");
        jpaProperties.setProperty("hibernate.temp.use_jdbc_metadata_defaults", "false");

        return jpaProperties;
    }

    @Bean
    public PlatformTransactionManager transactionManager(EntityManagerFactory entityManagerFactory) {
        JpaTransactionManager transactionManager = new JpaTransactionManager();
        transactionManager.setEntityManagerFactory(entityManagerFactory);

        return transactionManager;
    }

}
```

```xml
<dependencyManagement>
    <dependencies>
        <dependency>
            <groupId>org.springframework.data</groupId>
            <artifactId>spring-data-bom</artifactId>
            <version>2021.2.0</version>
            <scope>import</scope>
            <type>pom</type>
        </dependency>
    </dependencies>
</dependencyManagement>
```

```xml
<dependency>
    <groupId>org.springframework.data</groupId>
    <artifactId>spring-data-jpa</artifactId>
</dependency>
```

## EntityManager
+ 엔터티의 저장,수정,삭제,조회 등 엔터티와 관련된 모든일을 처리하는 관리자

```java
public interface EntityManager {
    public <T> T find(Class<T> entityClass, Object primaryKey);
    public <T> T find(Class<T> entityClass, Object primaryKey, Map<String, Object> properties); 
    public <T> T find(Class<T> entityClass, Object primaryKey, LockModeType lockMode);
    public <T> T find(Class<T> entityClass, Object primaryKey, LockModeType lockMode, Map<String, Object> properties);

    public void persist(Object entity);

    public <T> T merge(T entity);

    public void remove(Object entity);

    // ...

}
```

## EntityManagerFactory
+ EntityManager를 생성하는 팩토리
+ EntityManager는 필요할때마다 계속 생성함
```java
public interface EntityManagerFactory {
  public EntityManager createEntityManager();
  public EntityManager createEntityManager(Map map);
  public EntityManager createEntityManager(SynchronizationType synchronizationType);
  public EntityManager createEntityManager(SynchronizationType synchronizationType, Map map);

  // ...

}
```

## JPA/Hibernate Logging

### SQL
+ JPA properties

```properties
hibernate.show-sql=true
hibernate.format_sql=true
```
+ logback logger
```xml
<logger name="org.hibernate.SQL" level="debug" additivity="false">
    <appender-ref ref="console" />
</logger>
```

### binding parameters
```xml
<logger name="org.hibernate.type.descriptor.sql.BasicBinder" level="trace" additivity="false">
    <appender-ref ref="console" />
</logger>
```


## Entity Mapping
+ Entity 클래스에 DB 테이블과, 컬럼, 기본 키, 외래 키 등을 설정하는것

### Annotations
+ @Entity : JPA가 관리할 객체임을 명시
+ @Table : 맵핑할 DB 테이블 명 지정
+ @Id : PK 맵핑
+ @Column : 필드와 컬럼 이름 맵핑(생략가능 -> 변수명과 DB 필드명이 같은경우에 해당)
+ @Temporal : 날짜 타입 맵핑
+ @Transient : 특정 필드를 컬럼에 맵핑하지 않을 경우에 지정
   - cf.) java 8 date/time (LocalTime, LocalDate, ZonedDateTime) 타입은 @Temporal을 붙           이지 않음.
+ @GeneratedValue : 엔티티의 기본키 값을 자동으로 생성하기 위해 사용
   - @GeneratedValue(strategy = GenerationType.IDENTITY) 
      - 자동 증가기능을 사용하여 기본키 값을 생성함          
   - @GeneratedValue(strategy = GenerationType.SEQUENCE)
      - DB 시퀀스를 사용하여 기본키 값을 생성
      - 이 전략은 시퀀스를 지원하는 DB에서만 사용할수있음
   - @GeneratedValue(strategy = GenerationType.TABLE)
      - 별도의 키 생성용 테이블을 사용하여 기본 키 값을 생성
   - @GeneratedValue(strategy = GenerationType.AUTO)
      - JPA 구현체가 가장 적합한 전략을 선택하여 기본 키 값을 생성

+ @IdClass : 복합 키를 구성하는 여러개의 필드를 별도의 식별자 클래스로 지정, @Id를 사용해 복합키 필드와 엔티티 클래스간의 매핑을 함

