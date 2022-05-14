# HTML5
> ## Hyper Text Markup Language
* Hyper Text : 시공간을 초월하는 텍스트
* Markup : 태그 형식
* HTML은 웹 페이지를 만들기 위한 표준 마크업 언어
* 요소(element)
    * 시작태그 + 내용 + 종료(닫기)태그
    * 내용이 없는 요소는 닫기태그가 없을 수 있음
```html
<span>내용</span>
```
> ## 기본 구조
```html
<!DOCTYPE html>
<html>
    <head>
        <meta charset="UTF-8">
        <title></title>
    </head>
    <body>
    </body>
</html>
```
* \<!DOCTYPE html>
  * ! : 선언문
  * 문서타입이 HTML이라 선언
* \<html>\</html>
  * 필수 요소
  * root(루트) 요소
  * 모든 요소의 부모 요소
* \<head>\</head>
  * html문서에 대한 정보
  * \<meta charset="UTF-8">
    * 메타 정보를 지정하는 요소
  * \<title>\</title>
    * html 문서의 제목을 지정하는 요소
    * 브라우저에 표시
* \<body>\</body>
  * 필수 요소
  * 브라우저 화면에 표시하는 내용을 담고 있는 요소
---
# 태그 소개
> ## 헤더(Headers)
* 제목을 나타내기 위한 태그
* Block 모드
* 검색엔진이 헤더 태그를 통하여 웹 페이지의 구조를 파악


<H1>이것은 제목입니다</H1>
<H2>이것은 제목입니다</H2>
<H3>이것은 제목입니다</H3>
<H4>이것은 제목입니다</H4>
<H5>이것은 제목입니다</H5>
<H6>이것은 제목입니다</H6>

```html
<H1>이것은 제목입니다</H1>
<H2>이것은 제목입니다</H2>
<H3>이것은 제목입니다</H3>
<H4>이것은 제목입니다</H4>
<H5>이것은 제목입니다</H5>
<H6>이것은 제목입니다</H6>
```

> ## \<br> Line Break
* 줄 바꿈 태그

두부<br>
쿠키<br>
```html
두부<br>
쿠키<br>
```

<>

> ## \<hr>
* 수평선 태그
<hr color="red">
<hr color="green" width="50%">
<hr color="blue" width = "30px" align="left">

```html
<hr color="red">
<hr color="green" width="50%">
<hr color="blue" width = "30px" align="left">
```

> ## \<p>\</p>  Paragraph
* 문단(단락) 태그
* Block 모드

<p>문단 1</p>
<p>문단 2</p>
<p>문단 3</p>

```html
<p>문단 1</p>
<p>문단 2</p>
<p>문단 3</p>
```

> ## \<sapn>\</span>
* 스타일을 정의하는 데 사용할 수 있는 컨테이너 

```html
<!DOCTYPE html>
<html>
  <head>
    <style>
      span {
        /* CSS */
        color : red;
        border : 1px solid blue;
      }
    </style>
  </head>
  <body>
    나는 <span>두부쿠키</span>입니다.
  </body>
</html>
```

> ## \<pre>\</pre> preformatted text
* 태그 안 내용의 공백, 개행 유지
* 고정 너비 글꼴로 표시
* 미리 형식이 지정된 텍스트 정의
<pre>
package test;

public class Test {

	public static void main(String[] args) {

	
	}//main

}//class
</pre>
```html
<pre>
package test;

public class Test {

	public static void main(String[] args) {

	
	}//main

}//class
</pre>
```
> ## 텍스트 관련 태그
1. \<b> 굵은 글꼴, 중요성X
 
나는 <b>두부쿠키</b>입니다.
```html
나는 <b>두부쿠키</b>입니다.
```

2.  \<strong> 굵은 글꼴, 중요성O

나는 <strong>두부쿠키</strong>입니다.
```html
나는 <strong>두부쿠키</strong>입니다.
```

3. \<i> 이태릭체

나는 <i>두부쿠키</i>입니다.
```html
나는 <i>두부쿠키</i>입니다.
```

4. \<mark> 마크

나는 <mark>두부쿠키</mark>입니다.
```html
나는 <mark>두부쿠키</mark>입니다.
```

5. \<samll> 작은 글꼴

나는 <small>두부쿠키</small>입니다.
```html
나는 <small>두부쿠키</small>입니다.
```

6. \<del> 취소선, 삭제된 텍스트 표시

나는 <del>두부쿠키</del>입니다.
```html
나는 <del>두부쿠키</del>입니다.
```

7. \<ins> 밑줄, 추가된 텍스트 표시

나는 <ins>두부쿠키</ins>입니다.
```html
나는 <ins>두부쿠키</ins>입니다.
```

8. 윗 첨자

re<sup>iθ</sup>
```html
re<sup>iθ</sup>
```

9. 아랫 첨자

ln(x) = log<sub>e</sub>(x)
```html
ln(x) = log<sub>e</sub>(x)
```
10. 텍스트 방향

<bdo dir = "ltr">ㄱㄴㄷㄹㅁㅂㅅ</bdo> <br>
<bdo dir = "rtl">ㄱㄴㄷㄹㅁㅂㅅ</bdo>

```html
<bdo dir = "ltr">ㄱㄴㄷㄹㅁㅂㅅ</bdo> <br>
<bdo dir = "rtl">ㄱㄴㄷㄹㅁㅂㅅ</bdo>
```

> ## \<font>\</font>

<font size = "5">폰트 사이즈는 1~7, 기본값은 3</font><br>
<font face = "궁서체">폰트 글꼴</font><br>
<font color = "green">초록색 글자들 속에 <font color = "yellow" size ="2" face = "궁서체"> 노란색</font> 글자</font>

```html
<font size = "5">폰트 사이즈는 1~7, 기본값은 3</font><br>
<font face = "궁서체">폰트 글꼴</font><br>
<font color = "green">초록색 글자들 속에 <font color = "yellow" size ="2" face = "궁서체"> 노란색</font> 글자</font>
```

> ## 인용
1. 자동 들여쓰기
<blockquote>
우사인볼트가 세계에서 왜 제일 달리기 빠른 사람인 줄 알아요?
</blockquote>

```html
<blockquote>
우사인볼트가 세계에서 왜 제일 달리기 빠른 사람인 줄 알아요?
</blockquote>
```
2. 짧은 인용

<q>끝까지 갔기 때문이에요.</q>

```html
<q>끝까지 갔기 때문이에요.</q>
```

3. 연락처 정보를 나타내는 요소 (주소, 이메일, ...)

<address>서울특별시 강남구 테헤란로</address>
<address>010-1234-5678</address>

```html
<address>서울특별시 강남구 테헤란로</address>
<address>010-1234-5678</address>
```

4. 창작물 제목

<cite>자바의 정석</cite>

```html
<cite>자바의 정석</cite>
```


> ## \<a>\</a> 링크

* 다른 문서로 이동
* href 속성
  * [URL](WEB.md#url)을 사용
  * 절대경로, 상대경로로 지정
* 기본적으로 링크 표시 색
  * 파랑색 : 방문하지 않은 링크
  * 보라색 : 방문한 링크
  * 빨강색 : 활성 상태
* target 속성 
  * 어디에서 링크된 문서를 열지 결정
    * _self : 자기 자신 창 (기본값)
    * _blank : 새 창
    * _parent : 상위 프레임
    * _top : 창의 전체 본문
* id 속성으로 지정된 요소로 이동도 가능

1. 문서(웹 페이지) 연결

<a href = "./WEB.md">WEB.md</a><br>
<a href = "https://www.naver.com/" target = "_blank">NAVER</a>

```html
<a href = "./WEB.md">WEB.md</a><br>
<a href = "https://www.naver.com/" target = "_blank">NAVER</a><br>
```

2. JavaScript 호출

<a href = "javascript:window.alert('경고창')">경고창</a><br>

```html
<a href = "javascript:window.alert('경고창')">경고창</a><br>
```

> ## \<img>
* 이미지 
* in-line 모드
* alt 속성
* src 속성
  * 이미지 경로
* width
  * 이미지 폭(크기)
  * 비율 유지

<img alt = "Ryan" src = "./img/Ryan.jpg" width = "300px">
<img alt = "Ryan" src = "./img/Ryan.jpg" width = "50%">
<img alt = "Ryan" src = "./img/Ryan.jpg">

```html
<img alt = "Ryan" src = "./img/Ryan.jpg" width = "300px">
<img alt = "Ryan" src = "./img/Ryan.jpg" width = "50%">
<img alt = "Ryan" src = "./img/Ryan.jpg">
```
