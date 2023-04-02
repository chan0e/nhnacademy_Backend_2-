### JavaScript
+ 웹 서버가 아닌 클라이언트 컴퓨터에 설치된 브라우저에서 실행되는  클라이언트 스크립트 언어
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

(출처 - nhnacademy)

### use strict
+ 기존에 조용히 무시되던 에러들을 throwing 합니다.
+ JavaScript 엔진의 최적화 작업을 어렵게 만드는 실수들을 바로잡습니다. 가끔씩 엄격 모드의 코드는 비 - 엄격 모드의 동일한 코드보다 더 빨리 작동하도록 만들어짐
+ 엄격 모드는 ECMAScript의 차기 버전들에서 정의 될 문법을 금지
+ 비상식적인 문법들을 사용할 수 없도록 막아주는 역할
  - 변수의 중복선언
  - 변수의 초기화 없이 사용
  - 할당된 property 변경

```javascript
// 전체 스크립트 엄격 모드 구문
'use strict';
 var v = "Hi!  I'm a strict mode script!";
```

### 변수
  + var
    - 변수의 중복선언 가능 ( 에러발생하지 않음)

  + const (Immutable)
    - 변수 재 선언이 되지 않음
    - 변수 재할당 불가능 (할당된 객체의 내용은 변경가능)
    - 반드시 선언과 초기화를 동시에 진행

  + let (mutable)
    -  변수 재 선언이 되지 않음
    -  변수 재 할당 가능


## DOM(Document Object Model)
+ 웹 페이지를 이루는 테그들을 자바스크립트가 이용 할 수 있게끔 브라우저가 트리구조로 만든 객체 모델
+ DOM은 자체로 수행을 완료할 수 있는 것이 아니라 자바스크립트가 DOM을 제어할 수 있도록 이벤트를 발생시키거나 객체에 접근하기 위한 경로를 제공 
+ 자바스크립트는 DOM이 제공하는 메서드와 프로퍼티를 사용하여 데이터를 추출하거나 발생한 이벤트를 받아 추가적인 처리를 수행
+ html 문서를 javascript를 통해서 접근할 수 있도록 트리 구조로 구조화한 객체 모델

![image](https://user-images.githubusercontent.com/94053008/229350942-432814c6-bd13-4a5f-86b4-df82299d6925.png)

(출처 - nhnacademy)


+ create element, append element

```javascript
const divElement = document.createElement("div");
divElement.id="myDiv";
divElement.innerHTML = 'div element!';
document.body.appendChild( divElement );
const textNode = document.createTextNode('text node!');
divElement.appendChild(textNode);
const myDiv = document.getElementById("myDiv");
myDiv.setAttribute("style","color:red");
```

+ getElementsById

```javascript
const h1Element = document.createElement("h1");
h1Element.id="heading";
h1Element.innerHTML = 'H1 element!';
document.body.appendChild(h1Element);
const h1 = document.getElementById("heading");
console.log("h1:" + h1);
```

####



