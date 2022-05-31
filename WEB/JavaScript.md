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
### 노드 트리 표현

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

> ### 연산자
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
        <td></td>
        <td></td>
    </tr>
    <tr>
        <td colspan="2"></td>
    </tr>
    <tr>
        <td></td>
        <td></td>
    </tr>
    <tr>
        <td></td>
        <td></td>
    </tr>
    <tr>
        <td></td>
        <td></td>
    </tr>
    <tr>
        <td></td>
        <td></td>
    </tr>
    <tr>
        <td colspan="2"></td>
    </tr>
    <tr>
        <td></td>
        <td></td>
    </tr>
    <tr>
        <td></td>
        <td></td>
    </tr>
    <tr>
        <td></td>
        <td></td>
    </tr>
    <tr>
        <td></td>
        <td></td>
    </tr>
    <tr>
        <td colspan="2"></td>
    </tr>
    <tr>
        <td></td>
        <td></td>
    </tr>
    <tr>
        <td></td>
        <td></td>
    </tr>
    <tr>
        <td></td>
        <td></td>
    </tr>
    <tr>
        <td></td>
        <td></td>
    </tr>
</table>
