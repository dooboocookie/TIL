# CSS 

* Cascading Style Sheets
* html의 요소가 표시되는 방법, 문서의 스타일을 지정하는 언어


> ## 형식
* \<head>의 \<style> 태그 안에서 선언
* .css 파일을 stylesheet로 \<link>로 연결해서 사용
```css
선택자 {
  속성 : 값;
  속성 : 값;
  ...
}
/* 선택자를 여러 개 줄 수 있음*/
선택자1, 선택자2 {
  속성 : 값;
  속성 : 값;
}
```
## 선택자
<table>
<thead>
	<th>종류</th>
	<th>표현</th>
	<th>설명</th>
</thead>
<tr>
	<td>전체</td>
	<td>*</td>
	<td>html문서 내에 모든 요소에 적용하기 위한 선택자</td>
</tr>
<tr>
	<td>태그</td>
	<td>태그명</td>
	<td>선택한 태그 모두에 적용하는 선택자</td>
</tr>
<tr>
	<td>ID</td>
	<td>#아이디명</td>
	<td>해당 id명을 갖는 요소에 스타일 적용</td>
</tr>
<tr>
	<td>Class</td>
	<td>.클래스명</td>
	<td>해당 class에 해당되는 요소들에 스타일 적용</td>
</tr>
<tr>
	<td rowspan="4">복합</td>
	<td>요소.클래스명</td>
  <td>해당 요소 중 클래스명이 일치하는 요소들에 스타일 적용</td>
</tr>
<tr>
	<td>조상선택자 후손선택자</td>
	<td>조상 선택자에 후손 요소들 중 후손선택자와 일치하는 요소에 스타일 적용</td>
</tr>
<tr>
	<td>부모선택자 > 자식선택자</td>
	<td>부모 선택자에 자식 요소중 자식 선택자와 일치하는 요소에 스타일 적용</td>
	<td></td>
</tr>
<tr>
	<td>형제요소 +(~) 형제요소</td>
	<td>인접(+)하거나 형제되는(~)요소를 선택</td>
</tr>
<tr>
	<td>가상 클래스</td>
	<td>요소:가상클래스</td>
	<td>해당되는 요소의 특정 상태나 구조적으로 특정 요소에만 스타일을 적용</td>
</tr>
</table>


### 가상 클래스 

<table>

<thead><tr><td colspan="2">동적 선택자</td></tr></thead>
<tr>
	<td>:link</td>
	<td>방문하지 않은 상태의 링크</td>
</tr>
<tr>
	<td>:visited</td>
	<td>이미 방문한 링크</td>
</tr>
<tr>
	<td>:hover</td>
	<td>해당 요소에 마우스가 올라온 상태</td>
</tr>
<tr>
	<td>:active</td>
	<td>해당 요소가 선택된 상태/td>
</tr>
<tr>
	<td>:focus</td>
	<td>해당 요소에 포커스된 상태</td>
</tr>
<thead><tr><td colspan="2">구조 가상 클래스</td></tr></thead>
<tr>
	<td>:nth-child(n)</td>
	<td>부모의 n번째 자식 중 일치하는 요소</td>
</tr>
<tr>
	<td>:nth-of-type(n)</td>
	<td>부모의 타입이 일치하는 자식 중 n번째 요소</td>
</tr>
<tr>
	<td>:first-child</td>
	<td>첫번쨰 자식 요소</td>
</tr>
<tr>
	<td>:last-child</td>
	<td>마지막 자식 요소</td>
</tr>
<thead><tr><td colspan="2">가상 요소</td></tr></thead>
<tr>
	<td>::before</td>
	<td>해당 요소 앞 공간을 선택</td>
</tr>
<tr>
	<td>::after</td>
	<td>해당 요소 뒤 공간을 선택</td>
</tr>
<thead><tr><td colspan="2">부정 선택자</td></tr></thead>
<tr>
	<td>:not()</td>
	<td>()의 선택자를 제외하고 선택</td>
</tr>
</table>


---
### 인라인 CSS 적용 방법 
  * 해당 요소의 sytle 속성으로 적용
```html
<div style="background-color:red;"></div>
```


> ## 색 지정

1. 표준 색상명 (140개)
2. rgb(0~255,0~255,0~255)
   - red/green/blue 색의 3원소
3. #rrggbb	
   - HEX == 16진수
4. rgba(0~255,0~255,0~255,alpha 투명도 0.0~1.0)
5. hsl 
	- hue(색조) 0~360 : 0(빨강) / 120(초록) / 240(파랑) 
	- saturation(채도) 0~100% 
	- lightness(밝기) 0(검정)~100(흰색)%
```css
선택자 {
  
  속성 : red;
  
  속성 : #rrggbb;
  
  속성 : rgb(255,255,255);
  
  속성 : rgba(255,255,255,0.5);
  
  속성 : hsl(0,100%,50%);
}
```

> ## display 속성
### inline 모드
* 앞, 뒤 개행 X
* 다른 요소들과 한 라인에 배치
* Content가 차지하는 양만큼만 공간 차지
* inline 요소
  * \<span>
  * \<a>
  * \<button>
  * ...

### block 모드
* 앞, 뒤 개행 O
* 다른 요소들과 다른 라인에 배치
* block의 높이, 너비, 안/밖의 여백을 줄 수 있음
  * 높이 속성 : height
  * 너비 속성 : width
  * 안쪽 여백 : padding
  * 바깥 여백 : margin
* block  요소
  * \<div>
  * \<p>
  * \<h1>~\<h5>
  * ...

### none
* 해당 컨텐츠를 보여지 않게 함
* visibility:hidden과 차이
  * diplay:none; - 콘텐츠가 차지하는 공간을 없앰
  * visbility:hiddenl - 콘텐츠가 차지하는 공간을 유지하고 보이지만 않음

> ## 박스 모델 (box model)
<img src="img/img_css_boxmodel.png" width="600px">


* Content
  * 실질적인 내용을 담고 있는 영역
  * width
    * 너비
    * 기본 값 : 부모의 너비
  * height
    * 높이
    * 기본 값 : 콘텐츠의 양
* padding  
  * 안쪽 여백
    * 컨텐츠(텍스트, 이미지, ...)와 영역 사이에 간격
* border 
  * 테두리
* margin
  * 바깥 여백
    * 요소 영역 바깥쪽으로 갖는 여백


> ## float 속성


<table>
    <caption>플로팅 관련 속성</caption>
    <tr>
        <td>float</td>
        <td>'뜨다'라는 의미<br>요소를 플로팅해서 어디에 보여줄 지를 결정</td>
    </tr>
    <tr>
        <td>overflow</td>
        <td>float된 요소가 부모 요소의 영역보다 클 때, 흘러 넘치는 상황에서 어떻게 보여줄 지 결정</td>
    </tr>
    <tr>
        <td>clear</td>
        <td>해당 위치에 부유를 제거하여 float된 요소 다음에 오는 요소가 float요소 밑에 깔리지 않게 하는 속성</td>
    </tr>
</table>


* float(둥둥 뜨다)
* 요소의 위치, 레이아웃을 배치하기 위해 사용
* 값
  * none : 기본 값
  * left : 띄운 요소를 왼쪽에 배치
  * right: 띄운 요소를 오른쪽에 배치

### 문제점
1. float 속성을 사용
2. 컨테이너의 height이 기본값이면 컨텐츠의 양만큼 지정
3. 컨텐츠들이 다 float되면 overflow발생

#### &rarr; 해결
1. 컨테이너에 overflow속성을 auto나 hidden을 줘서 넘친 속성만큼 컨테이너의 높이를 줘야 함
2. 의사 요소(::before  / :: after)에 clear속성을 준다
 
 


### 이미지 플로팅
* \<img>에 style 속성의 float 값
* 부모 태그의 영역에서 위치할 곳을 지정

<p style="border:1px solid; padding">
	<img alt="Ryan" src="./img/Ryan.jpg" style="width:70px; float: right;">
	Lorem ipsum dolor sit amet, consectetur adipisicing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. 
</p>
<p style="border:1px solid;">
	<img alt="Ryan" src="./img/Ryan.jpg" style="width:70px; float: left;">
	Lorem ipsum dolor sit amet, consectetur adipisicing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. 
</p>

```html
<!-- style 속성으로 적용 -->
<p style="border:1px solid;">
	<img alt="Ryan" src="./img/Ryan.jpg" style="width:70px; float: right;">
	Lorem ipsum dolor sit amet, consectetur adipisicing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. 
</p>
<p style="border:1px solid;">
	<img alt="Ryan" src="./img/Ryan.jpg" style="width:70px; float: left;">
	Lorem ipsum dolor sit amet, consectetur adipisicing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. 
</p>
```

> ## overflow 속성


> ## 반응형 웹
* 다양한 장치에서 페이지를 보기 좋게 디자인하는 것
### 뷰포트 (ViewPort)
  * \<meta name="viewport" content="width=device-width, initial-scale=1.0">
  * width=device-width
    * 디바이스의 너비로 너비를 맞춤
  * initial-scale=1.0
    * 초기 화면 배율을 설정
    * 0.0~1.0의 백분율

### 반응형 텍스트 크기
* vw(viewport width)
  * 1vw == 뷰포트의 1%
    * 뷰포트 50cm의 1vw == 0.5cm

### 미디어 쿼리
* 미디어 쿼리를 이용해서 화면 조건에 따라 다른 레이아웃 표현
* @media 조건 {}
  * 조건
    * min-width : 최소 너비
    * max-width : 최대 너비
    * only screen : 화면에 표시될 때만 적용

```CSS
nav {
  float : left;
  width : 20%;
}
article {
  float : left;
  width : 60%
}
aside {
  float : left;
  width : 20%;
}
@media only screen and (max-width:600px){
  nav, article{
    width : 100%
  }
  aside{
    display : none;
  }
}
```
* 600px 이상에서
<img src="img/mediaquery1.png">

* 600px 이하에서
<img src="img/mediaquery2.png">


>## position


>## 정렬
### 수직 정렬
1. 블럭 모드를 컨테이너에 대하여 가운데 정렬
```css
div{
  margin: 0 auto;
  /* left, right 마진을 자동으로줘서 가운데 정렬*/
}
```
2. 텍스트를 가운데 정렬
```css
p{
  text-align: center;
  /* 요소 안의 텍스트를 가운데 정렬 */
}
```
