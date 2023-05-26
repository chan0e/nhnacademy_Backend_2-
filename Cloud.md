###### Microsoft Azure로 실습을 함

## Cloud Computing
+ 인터넷을 통해 리소스와 서비스를 제공하는 컴퓨팅 모델
+ 데이터 센터에서 물리적인 서버 대신 가상화된 리소스를 사용하여 사용자에게 서비스를 제공
+ 사용자는 필요한 컴퓨팅 리소스를 유연하게 확장하거나 축소할 수 있으며, 인터넷에 접속하는 어떤 장소에서나 액세스할 수 있음

### Service Models

##### IaaS(Infrastructure as a Service)
+ 서버,스토리지,네트워크 등을 가상화하여 제공하는 서비스
+ 사용자는 가상 머신, 스토리지, 네트워크 등의 인프라 리소스를 필요에 따라 조정하고 관리
+ 관련된 프로토콜
    -  TCP/IP : 가상 머신과 호스트 간의 통신을 위해 사용
    -  SSH(Secure Shell) : 원격으로 가상 머신에 접속하여 관리하기위한 프로토콜
    -  API Protocol : API를 통해 리소스 관리 및 제어를 위해 사용

##### PaaS(Platform as a Service)
+ 응용 프로그램 개발 및 배포를 위한 플랫폼을 제공하는 서비스
+ 개발자는 애플리케이션 개발에 필요한 환경(OS, DB. Tool)등을 관리하지 않아도됨
+ 관련된 프로토콜
    - HTTP(Hypertext Transfer Protocol) : 애플리케이션과 사용자 간의 통신에 사용됨
    - API Protocol : 애플리케이션 배포, DB 엑세스, 인증 등을 위한 API 제공

##### Saas(Software as a Service)
+ 소프트웨어 애플리케이션을 인터넷을 통해 제공하는 서비스
+ 사용자는 인터넷 브라우저 또는 애플리케이션을 통해 소프트웨어에 엑세스하고 사용할 수 있음
+ 관련된 프로토콜
    - HTTP
    - HTTPS : 보안통신을위한 프로토콜로 데이터의 안전한 전송을 보장
    - SMTP : 이메일 전송을 처리하기 위한 프로토콜


## Docker
+ 컨테이너를 관리하는 플랫폼
+ 다양한 프로그램, 실행환경을 컨테이너로 추상화하고 동일한 인터페이스를 제공하여 프로그램의 배포 및 관리를 단순하게 해줌

### Container
+ 애플리케이션과 해당 애플리케이션을 실행하는 환경을 포함한 가볍고 독립적인 실행 단위
+ 컨테이너는 격리된 환경에서 동작하며, 호스트 시스템과는 독립적으로 리소스를 관리하여 애플리케이션을 보다 효율적으로 실행하고 배포할 수 있게 해줌

![image](https://github.com/chan0e/nhnacademy_Backend3-/assets/94053008/616ece52-4225-4df4-8a93-227ca2799528)
###### 사진출처 https://cultivo-hy.github.io/docker/image/usage/2019/03/14/Docker정리/

+ 운영체제 수준에서 가상화를 실시하여 다수의 컨테이너를 OS 커널에서 직접 구동
+ 따라서 훨씬 가볍고 운영체제 커널을 공유하며, 시작이 빠르고 메모리를 적게 차지

### Image
+ 컨테이너 실행에 필요한 파일과 설정값등을 포함하고 있는 것으로 상태값을 가지지 않고 변하지 않음
+ 컨테이너는 이미지를 실행한 상태라고 볼수 있고 추가되거나 변하는 값은 컨테이너에 저장
+ 같은 이미지에서 여러개의 컨테이너를 생성할 수 있음

###### 리눅스환경에서 DOCKER실습을 하였고 Intellij에서 나온 war 파일을 가지고 배포해보는 연습을 해봤다
###### DB는 link를 이용해서 연결해주는걸로 알고있는데 지금 실습에서는 내가 사용해보지않음
### 실습
+ 처음에 로컬파일에 있는 war파일을 가상머신 주소에 있는 파일위치로 scp를 이용해 복사해줌
+ Docker tomcat 다운로드(프로젝트내에서 돌린 tomcat 버전과 맞춰줘야함... 이걸로 삽질 5시간정도 했다.)
```
sudo docker pull tomcat:9
```
+ image로 잘 올라갔나 확인
```
sudo docker images
```

+ Dockerfile을 만들어줌
```vi
FROM tomcat:9
RUN rm -rf /usr/local/tomcat/webapps/ROOT
ENV JAVA_OPTS='-Dspring.profiles.active=local'
COPY ./ROOT.war /usr/local/tomcat/webapps/ROOT.war
CMD ["catalina.sh", "run"]
```

+ Dockerfile에 있는 경로에서 도커파일을 my-war-app빌드해줌 -> image로 올라감
```
sudo docker build -t my-war-app .
```
+ 실행해줌 포트는 8080
```
sudo docker run -d --name=myapp -p 8080:8080 my-war-app
```

+ 잘 올라갔는지 확인
```
sudo docker ps
```
+ 마지막으로 Docker hub로 push 해줌

