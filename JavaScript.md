### JavaScript
+웹 서버가 아닌 클라이언트 컴퓨터에 설치된 브라우저에서 실행되는  클라이언트 스크립트 언어
+ 웹 페이지에 기능을 더해 동적인 HTML 페이지를 만들 수 있음

+ WEB API
  - javascript 언어자체에는 포함되지 않지만 브라우져가 이해할 수 있는 API 입니다.
    
+ 개발자 도구 ( 콘솔)
  - 윈도우
    - Ctrl + Shift +J
  - MAC
    - CMD + Option  + J

+ console 명령어
  - console.log("hello")
  - console log clear
  - clear()
  - console.table([0,1,2,3,4,5,6,7,8,9,10])
  - 시간측정


```javascript

console.time("sum");
let sum = 0;
for(let i=0; i<1000; i++){
    sum = sum + i;
}
console.timeEnd("sum");

```

### script를 포함하는 방법

+ head에 script를 포함하는 방법


```javascript
<html>
    <head>
       <script src="main2.js"></script>
    </head>

    <body>
        <h1> hello world </h1>
    </body>

</html>

```

html 문서가 로딩되기전에 실행



+ body 직전에 호출하는 방법

```javascript
<html>
    <head>

    </head>

    <body>
        <h1> hello world </h1>
        <script src="main2.js"></script>
    </body>

</html>

```
+ 사용자가 빠르게 기본적인 html 문서를 볼 수 있음
+ html문서와 javascript 의존성이 있다면(UI) 정상적인 화면을 제공해주기 위해서 서버에서 해당 javascript를 다운로드 후 실행하는 딜레이가 발생

+ async
  - 일반 스크립트에 async 속성이 존재하면 HTML 구문 분석 중에도 스크립트를 가져오며, 사용 가능해지는 즉시 평가를 수행

+ defer 
  - 브라우저가 스크립트를 문서 분석 이후에,  DOMContentLoaded 발생 이전에 실행해야 함을 나타내는 불리언 속성
  - defer 속성을 가진 스크립트는 자신의 평가가 끝나기 전까지 DOMContentLoaded 이벤트의 발생을 막음.

![image](https://user-images.githubusercontent.com/94053008/229350536-f9eb33ad-6c22-4f9d-8e6f-2a29bfbfeedc.png)



