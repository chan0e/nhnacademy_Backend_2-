## OSI 계층 구조
![OSI_계층구조](https://user-images.githubusercontent.com/94053008/223013555-203274fc-ffb7-47d1-b8fa-7f401e2527f9.png)


Link: http://wiki.hash.kr/index.php/응용계층

## L7 응용계층
+ 실제 네트워크 애플리케이션(프로세스)들이 다루는 영역
+ 이용자의 적용 업무를 처리하는데 필요한 모든 기능을 이용자측에서 정의하고. 처리하는 부분
+ 대표적인 프로토콜
   - HTTP, DHCP, SMTP, FTP
   - DNS

<img width="641" alt="image" src="https://user-images.githubusercontent.com/94053008/223012076-9686c33a-cec9-4e9a-bfc0-3755a1342e19.png">

### DNS (Domain Name System)
 + 일종의 주소록
 + 분산 DB
   - 도메인 이름, IP 등을 서비스


### 지원하는 기능 - 레코드 타입
 + A: 도메인에 대한 IP 응답
 + NS: 특정 도메인의 Name Server 정보 응답
 + CNAME: canonical name 설정
 + MX: 도메인의 메일 수신 서버 주소를 응답
 + TXT: 임의 문자열 부가 정보 관리, SPF, DKIM 용으로도 사용
 + SRV: IP 외에 Port 번호까지 서비스 가능



### DNS QUERY FLOW
<img width="596" alt="image-1" src="https://user-images.githubusercontent.com/94053008/223012978-cbf27374-6c6c-4d95-aa5c-bfe59d9c778d.png">

 + Local DNS에 캐싱이 되어 있는 경우는 바로 응답
 + 캐싱이 되어 있지 않은 경우에는 Root, TLD, Authoratative DNS 순서에 질의하여 결과 응답


## L4 전송계층
 + 3계층인 네트워크 계층가 데이터를 전달할때 데이터가 제대로 도착했는지 확인
 + 데이터가 최종적으로 도착할 애플리케이션이 무엇인지 식별


### TCP / UDP 통신
 + TCP(Transmission Control Protocol)
   - 3-wat handshake를 사용해서 데이터를 보냄 (신뢰성)
   - Port Number로 데이터의 목적지를 구분함 (식별성)

 + UDP(User Datagram Protocol)
   - 데이터를 전송할때 바로 보내줌으로 전송속도가 빠름


## L3 네트워크계층
 + 데이터를 전송, 경로를 결정한다.

<img width="998" alt="image-2" src="https://user-images.githubusercontent.com/94053008/223033974-64892a92-4751-4348-9f81-ba05bc214bad.png">


## L2 링크계층
 + 인정합 네트웤 노드낄 데이터를 전송하는 기능과 절차를 제공
 + 물리 계층에서 발생할 수 있는 오류를 감지하고 수정 (대표적 Ethernet)

<img width="1077" alt="images-redgem92-post-1504c0db-a218-4a3d-8ab5-415a252638d7-image" src="https://user-images.githubusercontent.com/94053008/223313934-ecc70d3b-d47d-4d94-b8c4-c96bcf573fa8.png">

## 데이터 링크 주요기능

   <img width="1059" alt="images-redgem92-post-84b196ac-bdfb-406a-8019-09a3f91cac08-image" src="https://user-images.githubusercontent.com/94053008/223314356-dc818ff0-35f9-420a-8089-becd2991fa4b.png">

+ 네트워크 계층에서 구성되는 데이터의 단위를 Datagram 이라고 한다.
   - Header : 목적지, 출발지 주소 그리고 데이터 내용을 정의
   - Trailer : 비트의 에러를 감지

+ 회선제어, 흐름제어, 오류제어 3가지 기능이 존재
 

