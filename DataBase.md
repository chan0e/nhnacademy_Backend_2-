###### 실습 DB는 MySQL로 진행됨

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


### 무결성 제약조건 개요
+ 저장된 정보의 품질에 따라 데이터베이스의 품질이 결정됨

1. 개체무결성
   : 각 릴레이션의 기본키를 구성하는 속성은 NULL 값이나 중복된 값을 가질수 없음.

3. 참조무결성
   : 외래키 값은 NULL이거나 참조하는 릴레이션의 기본키 값과 동일해야 한다.
   
5. 도메인무결성
   : 속성들의 값은 정의된 도메인에 속한 값이어야 한다.


#### KEY의 개념

KEY는 데이터베이스에서 조건에 만족하는. 튜플을 찾거나 순서대로 정렬할때 다른 튜플들과 구별할 수 있는 기준이 되는 속성

+ Candidate Key
  - 유일하게 식별할 수 있는 속성들의 부분집합
  - 모든 릴레이션은 반드시 하나 이상의 후보키를 가져야함
  - 유일성과 최소성을 만족


+ Primary Key
  - 후보키 중에서 선택한 주키(Main Key)
  - 특정 튜플을 유일하게 구별하는 속성
  - NULL 값을 가질수 없고 중복된 값을 저장할 수 없음 (개체 무결성 조건)


+ Alternate Key
  - 후보키가 둘 이상일 때 기본키를 제외한 나머지 후보키들


+ Super Key
  - 한 릴레이션에 존재하는 속성들의 집합으로 구성된 키
  - 유일성은 만족하지만 최소성은 만족하지 못함

+ Foreign Key
  - 관계를 맺고 있는 두개의 릴레이션 R1, R2에서 릴레이션 R1이 참조하고 있는 릴레이션 R2의 기본키와 같은 R1 릴레이션의 속성
  - 참조되는 릴레이션의 기본키와 대응되어 참조관계를 표현하는데 중요한 키
  - 외래키로 지정되면 참조 테이블의 기본키에 없는 값은 입력할 수 없음 (참조 무결성 조건)
   
   ***
   
   ### 관계 대수
   
   - 어떻게 질의를 해석하는가에 대한 언급하는 절차적 언어

   #### 연산자
   
   
   ![image](https://user-images.githubusercontent.com/94053008/226772647-c2362fe2-7400-47c1-8463-75085ce3188e.png)
    
    (출처 - https://inpa.tistory.com/entry/DB-📚-관계-대수-관계-해석-SQL-🕵%EF%B8%8F-정리)
    
  
   + Selection : 테이블에서 데이터를 가져옴
      - 원하는 데이터를 수평적으로 도출
  
   + Projection : 테이블에서 특정한 조건을 준 데이터만 출력
      - 원하는 데이터를 수직적으로 도출함
      - 한 릴레이션의 애트리뷰트들의 부분 집합을 구함
      - 셀렉션의 결과 릴레이션에는 중복 튜플이 존재불가, 프로젝션 연산의 결과에서는 존재할 수 있음


   + Union : 중복된걸 제외하고 테이블의 합
      - 결과 릴레이션에서 중복된 튜플들은 제외됨
      - 두 테이블에 튜플의 갯수가 다르거나 도메인이 다르면 안됨


   + Intersection : 중복된것을 보여주는 테이블
      
   + Difference : A - B를 한 결과 테이블
   + Cartesian Product : A 테이블과 B 테이블의 튜플수를 곱한 테이블의 결과
   + Join : 두 테이블들과의 결합 (주키 테이블에서 외래키 테이블로 Join하는것이 속도가 빠름)
     - Theta Join, Equi Join
        - {=, <>, <=, <, >=, >} 중의 하나
        - 동등 조인은 세타 조인 중에서 비교 연산자가 = 인 조인

     - Natural Join
       
     - Outer Join
     - Semi Join
   + Division : 두 테이블과의 분할
 
 
 
 ***
 
 ### SQL 구성
 
 + 데이터 조작어(Data Manipulation Language, DML)
    - 관계 대수와 튜플 관계 해석에 기반한 질의 언어를 포함
    - DB에 튜플을 삽입, 삭제하며 수정하는 명령어를 포함
    - Select, Insert, Updata, Delete
    
  


    
 + 데이터 정의어(Data Definition Language, DDL)
    - 릴레이션 스키마를 정의하고, 삭제하고 수정하는 명령어들을 제공
    - DB에 저장될 데이터가 만족해야 할 무결정 제약조건을 명시하는 명령어와 릴레이션과 뷰 등에 접근하는 권한을 
      명시하는 명령을 포함
    - Create, Alter, Drop, Rename, Truncate


    + 생성
      - CREATE TABLE {Table Name} (
        [Column Name] [Data Type] {NULL | NOT NULL} {Column Option} {Constraint List} [Constraint definition]
        )
        
    + 수정
      - ALTER TABLE [TableName]
        {ALTER COLUMN} [COLUMN NAME] {Column Option} {ADD} (Column | Constraints} 
        {ADD Option} {DROP} (Column | Constraints} {DROP Option}
        
    + 삭제
      - DROP TABLE [TableName]

 + 데이터 제어어(Data Control Language, DCL)
    - 테이블이나 뷰 등의 데이터에 대한 사용자의 접근을 제어하는 명령어를 포함
    - Grant, Revoke, Deny
 
 
 
 ***
 My sql에 기본 DBEngine은 InnoDB, 관리자가 엔진을 다르게 바꿔주면 물리적으로 봤을때 데이터들은 각 다른 곳에서 존재하므로 키 제약조건이나 원할하게 명령어를 진행할려면
 엔진을 같게 맞춰야함
 
 
 
## 데이터베이스 설계
+ 데이터베이스의 구조와 관계를 정의하고, 데이터베이스의 요구사항을 충족시키기위해 데이터를 구성하는 프로세스
+ DB 개발과정에서 가장 중요한 단계 중 하나

## ERD(Entity-Relationship Diagram)
+ 데이터 베이스 설계를 시각화하는 도구중 하나
+ 엔티티와 엔티티 간의 관계를 표시하여 데이터베이스의 구조와 관계를 시각적으로 표현

### ERD 일반적인 절차
1. 요구사항 수집: 데이터베이스 설계를 시작하기 전에, 시스템에 필요한 데이터 요구사항을 수집 이를 통해 DB의 기능과 제약사항을 정의할 수 있음
2. 개념적 설계: 요구사항을 바탕으로 엔티티, 속성, 관계를 정의하고 이를 개념적 모델로 표현
3. 논리적 설계: 개념적 모델을 기반으로, 엔티티와 관계를 더 상세하게 정의 이를통해 DB의 정규화와 익데스 등의 요소를 결정
4. 물리적 설계: 논리적 모델을 물리적으로 구현하기위해 테이블, 필드, 제약조건 등의 구체적인 정보를 추가
5. 구현: 데이터베이스를 구현하고, 초기 데이터를 입력
6. 유지보수

### ERD 표기법
+ Entity: 사각형으로 표현
+ Attribute: 타원형으로 표현
+ Relationship: 엔티티간의 속성을 표시. 마름모로 표현
  
  
### 식별관계 와 비식별관계
+ 식별관계
  - 부모 테이블(=참조되는 테이블)의 기본키를 자식테이블(=참조하는 테이블)의 기본키로 이용하는 방법

+ 비식별관계
  - 부모 테이블(=참조되는 테이블)의 기본키를 자식테이블(=참조하는 테이블)의 외래키로 이용하는 방법

+ 차이점
  - 식별관계를 사용할 경우 반드시 부모테이블에 데이터가 존재해야만 자식테이블에 데이터를 추가 할 수 있음
  - 비식별관계는 부모 데이터가 없어도 자식 테이블에서 데이터를 추가 할 수 있음
  - 다만 비식별관계는 데이터 정합성을 보장하지 않지만 구조 변경이 자유롭고, 식별관계는 구조 변경이 자유롭지 못하지만 데이터 정합성을 보장한다.


  
## 정규화(Denormalization)
