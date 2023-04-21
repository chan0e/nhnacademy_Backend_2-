## SonarQube
+ 코드 정적 분석을 수행하여 소프트웨어 개발 프로젝트의 코드 품질을 측정하고 보고하는 오픈 소스 도구
+ SonarQube를 사용하면 개발자는 코드 품질, 코드 취약점, 디자인 및 코드 복잡성에 대한 정보를 쉽게 이해 할 수 있음
+ 장점
  - 코드 품질 및 위약점을 쉽게 파악
  - 코드 품질을 향상시키는 방법을 제공
  - 코드 복잡성을 줄이고 유지 관리 비용을 절감
  - 코드 작성 시간을 줄임
  - 프로젝트에서 발견된 문제를 신속하게 수정할 수 있음


### 테스트 단계를 위한 플러그인
+ 빌드 수명 주기의 테스트 단계에서 애플리케이션의 단위 테스트를 실행하는 데 사용됨
```xml
<plugin>
    <groupId>org.apache.maven.plugins</groupId>
    <artifactId>maven-surefire-plugin</artifactId>
    <version>2.22.2</version>
	<configuration>
    	<!-- test skip 하려면 true 설정 -->
          <skipTests>false</skipTests>
    </configuration>
</plugin>
```

### jacoco plugin
+ java 코드의 커버리지를 체크하는 라이브러리
+ 테스트 코드를 실행 후 측정한 결과를 html, xml, csv 형태의 리포트 제공

```xml
<plugin>
    <groupId>org.jacoco</groupId>
    <artifactId>jacoco-maven-plugin</artifactId>
    <version>0.8.9</version>
    <executions>
        <execution>
            <id>jacoco-initialize</id>
            <goals>
                <goal>prepare-agent</goal>
            </goals>
        </execution>
        <execution>
            <id>jacoco-site</id>
            <phase>package</phase>
            <goals>
                <goal>report</goal>
            </goals>
        </execution>
    </executions>
</plugin>
```

### 나의 프로젝트
![image](https://user-images.githubusercontent.com/94053008/233543738-b7d52a00-7ba9-4df3-a851-49ceab3cdfbc.png)

+ 버그투성이...
+ 아직 테스트 코드를 작성안함..

