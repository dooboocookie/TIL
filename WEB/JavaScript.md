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
        <td colspan="2"비교 연산자</td>
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
