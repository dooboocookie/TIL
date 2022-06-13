# jQuery

* <a href="https://jquery.com/">jQuery</a> : javaScript 라이브러리
* 브라우저 종류 상관 없이 사용 가능

> ## 사용 목적
1. HTML 문서 탐색 및 조작
2. 이벤트 처리
3. 애니메이션
4. Ajax와 같은 작업
5. ...


> ## 연결 방법
  * jQeury 다운로드 [(링크)](https://jquery.com/download/)
     * 압축 - 대역폭을 절약하고 프로덕션 성능을 향상
       * jquery-3.6.0.min.js
     * 비압축 - 개발 또는 디버깅 중에 자주 사용
       * jquery-3.6.0.js
  * CDN(Content Delivery Network)로 구글 라이브러리 같은 곳에서 로드하여 사용
```html
<script src="https://ajax.googleapis.com/ajax/libs/jquery/3.6.0/jquery.min.js"></script>
```
  
> ## 기본 구문
```javascript
$("jQeury Selector(선택자)").액션();
```
### jQeury Wrapper
  * $ (== jQuery == window.jQuery == window)
  * `요소 객체`나 `제이쿼리 선택자(문자열)`을 매개변수로 받음
  * `요소 객체`를 반환하여 그 대상이 하는 액션으로써 메소드들을 호출할 수 있게 함

1. jQeury Selector
* `css 선택자`보다 더 다양한 표현으로 선택자를 설정할 수 있음
* 문자열로서 `요소 객체`를 지칠할 수 있게 함

2. 액션(action())
* jQuer Wrapper에서 반환된 `요소 객체`가 어떤 작업을 하도록 하는 메소드

### 체이닝
* 한 `요소 객체`에 여러 속성이나 메소드를 이을 수 있따
```javascript
$("div")
  .children("p.first") // div의 자식 요소 중 해당 선택자를 얻어옴
    .css({"color":"red"}) // 그 얻어온 요소의 css 속성을 바꿈
  .end() //.children("p.first") 체이닝 끊음
  .find("span") // div의  후손 요소 중 span 태크를 찾음
    .css({"color":"blue"})
```

> ## jQuery Selector

### 기본선택자

<table>
    <tr>
        <th>선택자</th>
        <th>내용</th>
    </tr>
    <tr>
        <td>*</td>
        <td>모든 요소를 나타내는 선택자</td>
    </tr>
    <tr>
        <td>#아이디명</td>
        <td>해당 아이디를 갖는 요소를 나타내는 선택자</td>
    </tr>
    <tr>
        <td>.클래스명</td>
        <td>해당 클래스를 갖는 요소들을 나타내는 선택자</td>
    </tr>
    <tr>
        <td>태그명</td>
        <td>해당 태그명을 갖는 요소들을 나타내는 선택자</td>
    </tr>
</table>

### 기본 필터

<table>  
    <tr>
        <td colspan='2' align="center">기본 필터 선택자</td>
    </tr>
    <tr>
        <td>:first</td>
        <td>해당 요소들 중 첫번째의 요소를 나타내는 선택자</td>
    </tr>
    <tr>
        <td>:last</td>
        <td>해당 요소들 중 마지막의 요소를 나타내는 선택자</td>
    </tr>
    <tr>
        <td>:even</td>
        <td>해당 요소들 중 index가 짝수인 요소를 나타내는 선택자</td>
    </tr>
    <tr>
        <td>:odd</td>
        <td>해당 요소들 중 index가 홀수인 요소를 나타내는 선택자</td>
    </tr>
    <tr>
        <td>:root</td>
        <td>< html>요소를 나타내는 선택자</td>
    </tr>
    <tr>
        <td>:header</td>
        <td> < h1> ~ < h6>요소를 나타내는 선택자</td>
    </tr>
    <tr>
        <td>:empty</td>
        <td>자식 노드가 없는 요소를 나타내는 선택자</td>
    </tr>
    <tr>
        <td>:parent</td>
        <td>어떤 요소의 부모인 요소를 나타내는 선택자</td>
    </tr>
</table>

### 자식 선택자

<table>  
    <tr>
        <td colspan=2  align="center">자식 선택자</td>
    </tr>
    <tr>
        <td>:first-child<br>:last-child</td>
        <td>해당 요소들 중 어떤 요소의 첫(마지막) 자식 요소인 경우를 나타내는 선택자<b</td>
    </tr>
    <tr>
        <td>:first-of-child<br>:last-of-child</td>
        <td>어떤 요소의 자식 요소의 해당 요소 중 처음(마지막)인 것을 나타내는 선택자</td>
    </tr>
    <tr>
        <td>:nth-child(n)<br>:nth-last-child(n)</td>
        <td>해당 요소들 중 어떤 요소의 n번째(뒤에서 n번째) 자식 요소인 경우를 나타내는 선택자<b</td>
    </tr>
    <tr>
        <td>:nth-of-type(n)<br>:nth-last-of-type(n)</td>
        <td>어떤 요소의 자식 요소의 해당 요소 중 n번째(뒤에서 n번째)인 것을 나타내는 선택자</td>
    </tr>
    <tr>
        <td>:only-child</td>
        <td>해당 요소들 중 어떤 요소의 유일한 자식 요소인 경우를 나타내는 선택자</td>
    </tr>
    <tr>
        <td>:only-of-type</td>
        <td>어떤 요소의 자식 요소의 해당 요소 가 유일한 경우를 나타내는 선택자</td>
    </tr>
</table>

### 계층 선택자

<table>  
    <tr>
        <td colspan="2" align="center">계층 선택자</td>
    </tr>
    <tr>
        <td>></td>
        <td>부모선택자 > 자식선택자 : 직계 자식 요소를 나타내는 선택자</td>
    </tr>
    <tr>
        <td>(공백)</td>
        <td>조상선택자 자손선택자 : 해당되는 모든 자손</td>
    </tr>
    <tr>
        <td>+</td>
        <td>선택자 + 선택자 : 바로 다음에 오는 형제레벨의 요소인 경우를 나타내는 선택자</td>
    </tr>
    <tr>
        <td>~</td>
        <td>선택자 ~ 선택자 : 형제레벨의 요소들 중 다음의 오는 경우를 나타내는 선택자</td>
    </tr>
</table>

### 함수 필터 선택자

<table>
    <tr>
        <td colspan="2" align="center">함수 필터 선택자</td>
    </tr>
    <tr>
        <td>:eq(idx)</td>
        <td>선택된 요소들 중 idx번째 요소를 나타내는 선택자</td>
    </tr>
    <tr>
        <td>:gt(idx)</td>
        <td>선택된 요소들 중 idx번째보다 나중에 오는 요소를 나타내는 선택자</td>
    </tr>
    <tr>
        <td>:lt(idx)</td>
        <td>선택된 요소들 중 idx번째보다 나중에 오는 요소를 나타내는 선택자</td>
    </tr>
    <tr>
        <td>:not(selector)</td>
        <td>입력된 selector를 제외한 요소를 나타내는 선택자</td>
    </tr>
    <tr>
        <td>:animated</td>
        <td>애니메이션이 실행되고 있는 요소를 나타내는 선택자</td>
    </tr>
    <tr>
        <td>:has(selector)</td>
        <td>해당 selector 자식으로 갖는 요소를 나타내는 선택자</td>
    </tr>
    <tr>
        <td>:contains(str)</td>
        <td>해당 str(문자열)을 자식으로 갖는 요소를 나타내는 선택자</td>
    </tr>
</table>

### visiblity 필터 선택자

<table>
    <tr>
        <td colspan="2" align="center">visiblity 필터 선택자</td>
    </tr>
    <tr>
        <td>:hidden</td>
        <td>hidden 상태인 요소를 나타내는 선택자</td>
    </tr>
    <tr>
        <td>:visible</td>
        <td>visible 상태인 요소를 나타내는 선택자</td>
    </tr>
</table>

### 입력 폼 선택자

<table>
    <tr>
        <td colspan="2" align="center">입력 폼 필터 선택자</td>
    </tr>
    <tr>
        <td>:input</td>
        <td>입력하는 요소(input, textarea, button)요소를 나타내는 선택자</td>
    </tr>
    <tr>
        <td>:text</td>
        <td>input요소 중 type이 text인 요소를 나타내는 선택자</td>
    </tr>
    <tr>
        <td>:button</td>
        <td>input요소 중 type이 button인 요소와 button요소를 나타내는 선택자</td>
    </tr>
    <tr>
        <td>:checked</td>
        <td>체크된 요소를 선택하는 선택자</td>
    </tr>
    <tr>
        <td>:selected</td>
        <td>선택된 요소를 선택하는 선택자</td>
    </tr>
    <tr>
        <td>:focus</td>
        <td>포커스가된 요소를 선택하는 선택자</td>
    </tr>
    <tr>
        <td>:disabled</td>
        <td>비활성화된 요소를 선택하는 선택자</td>
    </tr>
    <tr>
        <td>:enabled</td>
        <td>비활성화된 요소를 선택하는 선택자</td>
    </tr>
</table>

### 속성 선택자

<table>
<tr align=center>
  <td>[속성명=속성값]</td>
</tr>
<tr>
  <td>
      1. 속성값 생략 : 속성값에 상관없이 해당 속성을 갖는 요소 선택<br>
      2. = : 해당 속성값이 일치하는 요소 선택<br>
      3. *= : 해당 속성값이 포함된 속성값을 가진 요소 선택<br>
      4. ^= : 해당 속성값으로 시작하는 속성값을 가진 요소 선택<br>
      5. $= : 해당 속성값으로 끝나는 속성값을 가진 요소 선택<br>
      6. ~= : 해당 속성값이 (앞뒤 공백을 포함하여) 포함된 속성값을 가진 요소 선택<br>
      7. != : 해당 속성값을 갖지 않는 요소 선택<br>
      8. |= : 해당 속성값이거나 시작하는 요소 선택<br>
  </td>
</tr>
</table>

> ## Effect

<table>
  <tr>
    <td>duration</td>
    <td>
      애니메이션이 실행되는 시간을 설정하는 매개변수
      <br>Number:밀리세컨드 
      <br>String:"slow"==600ms, "fast"==200ms, default==400ms</td>
  </tr>
  <tr>
    <td>easing</td>
    <td>
      애니메이션이 진행하는 속도를 설정하는 매개변수
      <br>"linear" : 선형적으로 변화
    </td>
  </tr>
  <tr>
    <td>complete</td>
    <td>콜백함수 : 애니메이션이 종료된 후 실행되는 메소드</td>
  </tr>
</table>

### basics
* .show([duration [, easing] [, complete]])
  * 해당 `요소`를 `display`를 보이게 하는 메소드 
* .hide([duration [, easing] [, complete]])
  * 해당 `요소`를 `display`를 none값으로 하는 메소드
* .toggle([duration [, easing] [, complete]])
  * 해당 `요소`를 show와 hide상태로 번갈아 지정하는 메소드


### fading 
* .fadeIn( [duration ] [, easing ] [, complete ] )
  * 해당 `요소`를 `display`를 페이드 인하며 천천히 보이게 하는 메소드 
* .fadeOut( [duration ] [, easing ] [, complete ] )
  * 해당 `요소`를 `display`를 페이드 아웃하며 천천히 none값으로 하는 메소드 
* .fadeTo( duration, opacity [, easing ] [, complete ] )
  * 해당 `요소`를 투명도를 천천히 바꾸는 메소드 
* .fadeToggle( [duration ] [, easing ] [, complete ] )
  * 해당 `요소`를 번갈아가며 페이드 인 페이드 아웃 지정하는 메소드 


### Sliding
* .slideUp( [duration ] [, easing ] [, complete ] )
  * 해당 `요소`를 `display`를 위로 슬라이딩해 none값으로 하는 메소드 
* .slideDown( [duration ] [, easing ] [, complete ] )
  * 해당 `요소`를 `display`를 아래로 슬라이딩해 보이게 하는 메소드 
* .slideToggle( [duration ] [, easing ] [, complete ] )
  * 해당 `요소`를 slideDown slideUp 번갈아하는 메소드


### .animate({params}, duration, callback)

* {params}
  * `css 속성`을 정의하는 매개변수
  * 요소가 해당 값을 바뀌는 과정
  * 상대 값으로도 지정가능
    * 값이 `+=` 보다 커지거나 `-=` 보다 작아지게

#### 애니메이션 대기열
* 순차적으로 .animate() 처리
```javascript
$("div")
  .animate({height:"300px"},"slow") //A
  .animate({width:"300px"},"slow") //B
  .animate({height:"100px"},"slow") //C
  .animate({width:"100px"},"slow") //D
```
* 애니메이션 대기열 == 큐 == FIFO구조
  * A>B>C>D 순서로 처리
* .stop(stopAll,goToEnd) 메소드 :  애니메이션 중지
  * stopAll
    * true : 대기열 뒤에 애니메이션들까지 전부 중지
    * false : 대기열 뒤에 애니메이션들은 큐에 남아있음, 기본값
  * goToEnd
    * 현재 애니메이션을 즉시 완료할 수 있는 여부 지정 매개변수
    * true : 현재 애니메이션을 중지하고 완료상태로 보냄
    * false : 현재 애니메이션을 중지하고 중지된 시점의 값 유지, 기본값


```html
<button id="start">start</button>
<button id="stopff">stop(f,f)</button>
<button id="stopft">stop(f,t)</button>
<button id="stoptf">stop(t,f)</button>
<button id="stoptt">stop(t,t)</button>

<div style="background-color: aqua; width: 200px; height: 100px; position:absolute;">HELLO</div>

<script>
  $("#start").click(function () {
    //대기열 큐
    $("div")
        .animate({left:"200px"},5000) // 1
        .animate({fontSize:"3em"},5000); // 2
  });

  $("#stopff").click(function () {
    $("div").stop(false, false);
    // 1 애니메이션 처리할때 stopff 버튼 클릭 -> 1번 애니메이션만 중지 / 2번은 큐에 남아있음
  });
  $("#stopft").click(function () {
    $("div").stop(false, true);
    // 1 애니메이션 처리할 때 stopft 버튼 클릭 -> 1번 애니메이션 중지(완료상태) / 2번은 큐에 남아있음
  });
  $("#stoptf").click(function () {
    $("div").stop(true, false);
    // 1 애니메이션 처리할 떄 stoptf 버튼 클릭-> 1번 애니메이션 중지 / 2번 애니메이션도 중지
  });
  $("#stoptt").click(function () {
    $("div").stop(true, true);
    // 1 애니메이션 처리할 때 stopft 버튼 클릭 -> 1번 애니메이션 중지(완료상태) / 2번 애니메이션도 중지
  });
</script>
```

![stop()이미지](img/animate_stip().gif)


> ##  `요소`에 대한 메소드
### 자식 노드를 가져오거나 입력하는 메소드
1. .text()
* 매개변수 넣을 시, 해당 요소 자식으로 text로 입력
* 매개변수 생략 시, 해당 요소 자식 text 값을 반환
2. .html()
* 매개변수 넣을 시, 해당 요소 자식으로 html로 입력
* 매개변수 생략 시, 해당 요소 자식 html 값을 반환
3. .val()
* 매개변수 넣을 시, 해당 요소 value 입력
* 매개변수 생략 시, 해당 요소의 value 반환

### 요소의 `속성`에 대한 메소드
1. attr(속성, 값)
* 속성, 값 모두 입력 시, 해당 속성의 값 입력
  속성만 입력 시, 해당 속성의 값을 반환

### 요소 추가하는 메소드
1. A.append(B)
* A 요소 객체의 자식 맨뒤에 B를 추가하는 메소드
2. A.appendTo(B)
* A 요소 객체를 B의 자식 맨 뒤에 추가하는 메소드
1. A.prepend(B)
* A 요소 객체의 자식 맨뒤에 B를 추가하는 메소드
2. A.prependTo(B)
* A 요소 객체를 B의 자식 맨 뒤에 추가하는 메소드
3.  