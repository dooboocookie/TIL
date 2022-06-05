# JavaScript
* 객체 기반의 스크립트 프로그래밍 언어
* 목적
  * 웹페이지 사용자의 반응 처리
  * 사용자의 특정 이벤트나 입력 값을 받아서 동적으로 처리
* 용도
  * html 내용 변경
  * html 속성 변경
  * html 스타일 변경
  * html 요소 보이기 / 숨기기
  * ...
* 주로 프론트엔트 개발에서 UI / UX를 향상시키기는 목적으로 사용
  * 현재는 서버측 프로그램 개발에도 많이 사용(Node.js, ...)
* 설치 X
  * 클라이언트 브라우저에 내장되어있는 js 엔진 사용
* 자바 스크립트 표준
  * ECMAScript (에크마 스크립트) : ECMA-262
* 형식
```html
<script>
    //js 코딩 ...
</script>

<!-- 외부 .js 파일 연결 -->
<script src="test.js"></script>
```
* 외부 자바스크립트 파일 사용 시
  * html 코딩과 분리 - 유지, 보수 / 확장 용이
  * 캐싱된 js파일 - 페이지 로드 속도 향상 

> ## DOM
* Document Object Model
* HTML문서 객체 기반 표현 방식
  * \<body> \<html>태그를 JavaScript가 객체로서 접근하여 사용하는 방식


### 노드 트리 표현
* 트리 구조
* root node : \<html>

```bash
html
├── head
│   └── title
│       └── 페이지 제목 
└── body
    ├── h3
    │   └── 헤드라인 
    ├── p
    │   └── 내용..abcd... 
    └── img
```

## 데이터 타입
### document
* 브라우저가 불러낸 웹페이지를 나타냄
* 요소를 생성하거나, 가져오고, URL을 얻어오는 데, ... 사용
1. 속성
  * document.body
    * 현재 문서의 \<body> 태그를 리턴
  * document.documnetURI
    * 현재 문서의 위치를 반환
  * ...
2. 메소드
  * document.createElement()
    * 태그명을 매개변수로 받아, 요소를 만드는 메소드
  * document.getElementById()
    * 아이디명에 해당되는 element를 반환
  * document.querySelector()
    * 선택자에 해당되는 첫 element를 반환
  * document.querySelectorAll()
    * 선택자에 해당되는 element NodeList를 반환
  * document.write()
    * 문서에 작성하는 메소드
  * ...
### element
* 요소 또는 요소에 대한 node를 의미
1. 속성
  * element.innerHTML
    * 해당 요소의 내용을 HTML로 반환
  * element.innerText
    * 해당 요소의 내용을 text로 반환
  * element.nextElementSibling
    * 해당 요소의 다음 형제 요소를 반환
2. 메소드
  * element.append()
    * 해당 요소의 자식으로 노드 객체나 문자열을 삽입하는 메소드

### node
* 노드를 나타내는 객체
1. 속성
  * node.nextSibling
    * 다음으로 오는 형제 node를 반환
  * node.parentElement
    * 부모 노드에 오는 element를 반환
2. 메소드
  * node.appendChild()
    * 해당 노드에 자식으로 노드나 요소를 삽입하는 메소드
  * node.cloneNode()
    * 해당 노드를 복제한 노드를 반ㄴ환하는 메소드

### nodeList
* element의 배열(집합)
* item은 index를 통해서 접근
  * list.item(1)
  * list[i]


> ## 연산자
<table>
    <tr>
        <td colspan="2">산술연산자</td>
    </tr>
    <tr>
        <td>+</td>
        <td>덧셈 연산자</td>
    </tr>
    <tr>
        <td>-</td>
        <td>뺄셈 연산자</td>
    </tr>
    <tr>
        <td>*</td>
        <td>곱셈 연산자</td>
    </tr>
    <tr>
        <td>/</td>
        <td>나눗셈 연산자</td>
    </tr>
    <tr>
        <td>%</td>
        <td>나머지 연산자</td>
    </tr>
    <tr>
        <td>**</td>
        <td>제곱 연산자</td>
    </tr>
    <tr>
        <td colspan="2">증감 연산자</td>
    </tr>
    <tr>
        <td>++</td>
        <td>1 증가</td>
    </tr>
    <tr>
        <td>--</td>
        <td>1 감소</td>
    </tr>
    <tr>
        <td colspan="2">대입(할당) 연산자</td>
    </tr>
    <tr>
        <td>=</td>
        <td>대입 연산자 / 우항의 값을 좌항에 대입</td>
    </tr>
    <tr>
        <td>+=</td>
        <td>좌항에 값에 우항을 더한 값을 좌항에 대입</td>
    </tr>
    <tr>
        <td>-=</td>
        <td>좌항에 값에 우항을 더한 값을 좌항에 대입</td>
    </tr>
    <tr>
        <td>...</td>
        <td>*=, /=, %=, **=</td>
    </tr>
    <tr>
        <td colspan="2">비교 연산자</td>
    </tr>
    <tr>
        <td>==</td>
        <td>같은지 비교 / 타입은 비교하지 않음</td>
    </tr>
    <tr>
        <td>===</td>
        <td>같읁비 비교 / 타입도 비교</td>
    </tr>
    <tr>
        <td>>, < <br>>=, <=</td>
        <td>좌항 우항의 값 크기를 비교</td>
    </tr>
    <tr>
        <td>!=</td>
        <td>같지 않으면 true 반환</td>
    </tr>
    <tr>
        <td colspan="2">논리 연산자</td>
    </tr>
    <tr>
        <td>&&</td>
        <td>and</td>
    </tr>
    <tr>
        <td>||</td>
        <td>or</td>
    </tr>
    <tr>
        <td>!</td>
        <td>not</td>
    </tr>
    <tr>
    <tr>
        <td colspan="2">타입 연산자</td>
    </tr>
    <tr>
        <td>typeof</td>
        <td>대상의 타입을 나타내는 연산자</td>
    </tr>
    <tr>
        <td>a instanceof b</td>
        <td>b의 프로토타입이 a객체의 프로토타입 체인에 있는지</td>
    </tr>
    <tr>
        <td colspan="2">비트 연산자</td>
    </tr>
    <tr>
        <td>...</td>
        <td>& | ~  ^ << >> >>></td>
    </tr>
</table>

---

> # 자료형
<table>
<tr>
  <td>String</td>
  <td>
    문자열 데이터
    <br>요소(16비트,부호없는정수)의 집합
    <br>요소 하나당 string 한 자리, 인덱스(0 ~)
  </td>
</tr>
<tr>
  <td>Number</td>
  <td>
    숫자 데이터  
    <br>&pm;(2^53-1)까지의 수
    <br>정수, 실수 모두
    <br>&pm;Infinity, NaN 값 포함
  </td>
</tr>
<tr>
  <td>Boolean</td>
  <td>true / false 값을 가지는 자료형</td>
</tr>
<tr>
  <td>BigInt</td>
  <td>
    큰 정수를 임의의 정밀도로 갖는 자료형
  </td>
</tr>
<tr>
  <td>undefined</td>
  <td>
    선언된 변수에 할당하지 않은 변수에 자동으로 할당되는 값
  </td>
</tr>
<tr>
  <td>null</td>
  <td>
    의도적으로 비어있는 값을 나타냄
  </td>
</tr>
<tr>
  <td>Object</td>
  <td>
    관련된 데이터(속성)과 함수(메소드)의 집합
    <br>객체
  </td>
</tr>
</table>

### typeof 연산자
* 대상의 타입을 반환하는 연산자
  * typeof()함수도 가능
```javascript
console.log(typeof 100); //umber
console.log(typeof 3.14); //number
console.log(typeof "abc"); //string
console.log(typeof undefinded); //indefined
console.log(typeof null); //object
```

> ## String
* 문자열 자료형
* ""(큰따옴표), ''(작은 따옴표) 사이에 내용
  * var text = "abcd";
* 0개 이상의 문자 집합
* 연결
  * \+
  * concat()
### String관련된 유용한 함수
* String.trim()
  * 문자열 좌, 우 끝에 공백을 지움
* String.replace(searchString, replacement)
  * 문자열에서 일치하는 문자열을 찾아 대체
  * 매개변수
    * searchString : 찾는 문자열이나 정규표현식
    * replacement : 대체할 문자열
  * 리턴
    * String
    * 변경된 문자열
* String.substring(from, to) / String.slice(from, to)
  * 문자열의 원하는 위치 값에 문자(열)을 반환하는 함수
  * 매개변수
    * from : 시작 인덱스 (0부터 시작)
    * to : 끝 인덱스, 이 인덱스 이전까지 리턴
  * 리턴
    * String
    * 해당 인덱스의 문자열
* String.split(pattern)
  * 매개변수를 구분자로 문자열을 나누는 함수
  * 매개변수
    * 구분자로 사용할 문자열이나, 정규표현식
  * 리턴
    * Array(object)
    * 구분자로 나누어진 문자열의 배열을 반환
* padStart() / padEnd()
  * 정해진 자리만큼 채우고 문자열로 반환하는 함수
* startWith() / endWith()
  * 대상 문자열에 인자값이 시작하는지/끝나는지 판별하여 boolean값 반환하는 함수
* includes()
  * 대상 문자열에 인자값이 있는지 판별하여 boolean 값을 반환하는 함수

### 정규표현식
* string에서 특정 규칙으로 된 문자 조합을 찾기 위한 패턴
* //사이에 정규표현식 패턴 표시
* 변경자(modifier)
  * i : 대소문자 구분 X
  * g : 전체 문자열에서 모두 검색
  * m : 여러 줄 검색
* 선언 및 할당
```javascript
const pattern  = /hong/ig 
//대소문자 구분 없이 hong 모두 검색하기 위한 정규표현식 
```


> ## 변수 선언
1. var
* function-scoped
  * 블럭 안팍에서 같은 기억공간
* `hoisiting`시 자동으로 undefined로 초기화
  * 인터프리터가 변수의 메모리를 선언 전에 미리 할당함
* 변수 중복 선언 가능
```javascript
var test1 = 1;
var test1 = 10; //에러 없음

test2 = 100;
console.log('test2 = '+test2);
var test2; // 에러 없음(hoisting)
```

2. let
* block-scoped
  * 블럭안에서 할당한 값은 블럭 안에서만 유효
* `hoisting`시 변수를 자동으로 초기화하지 않음
  * block-scoped 단위로 호이스팅이 일어남
  * 변수 선언 전 변수에 할당 시 > [`tdz`](https://ui.toast.com/weekly-pick/ko_20191014)
* 변수를 중복으로 선언 불가 

```javascript
let test1 = 1;
let test1 = 100; // SyntaxError

test2 = 100;
let test2; // ReferenceError
```


3. const
* block-scooped
* let과 대부분 비슷한 규칙을 가짐
* 상수
  * 선언과 동시에 할당
  * 재할당 불가

```javascript
const test1; // Missing initializer in const declaration

const test2 = 3.14;
test2 = 3.141592 // SyntaxError
```
