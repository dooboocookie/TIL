# 타임리프

## 서버 사이드 렌더링(SSR)
* jsp 같이 서버에서 동적으로 HTML의 정보를 렌더링하기 위함

## 네츄럴 템플릿
* 타임리프는 HTML 태그를 유지한 상태
* 태그의 속성으로 타임리프 문법을 적용
* HTML을 직접 열어도 브라우저가 속성을 인식하지 못한 상태로 태그를 유지하며 열림

## 타임리프 선언
```html
<html xmlns:th="http://www.thymeleaf.org">
</html>
```

## 텍스트
```html
<!--타임리프-->
<span th:text="${data}"></span>
<span> [[${data}]]</span>

<!--렌더링 결과-->
<span>data 어트리뷰트에 할당된 내용</span>
<span>data 어트리뷰트에 할당된 내용</span>
```
* 기본적으로 이스케이프 th:text는 이스케이프 처리가 되어 `<` `>`는 HTML엔티티로 렌더링 된다

```html

<!--타임리프-->
<span th:text="${data}"></span>
<span> [[${data}]]</span>
<span th:utext="${data}"></span>
<span> [(${data})]</span>

<!--어트리뷰트로 "<b>Hello</b>이 있을 떄 렌더링 결과-->
<span>&lt;b&gt;Hello&lt;/b&gt;</span>
<span>&lt;b&gt;Hello&lt;/b&gt;</span>
<span><b>Hello</b></span>
<span><b>Hello</b></span>
```
* 여러 태그들이 들어가면 혼란이 있을 수 있기 떄문에, 기본적으로는 이스케이프 처리를 하는 th:text를 사용해야 한다


## 변수
* `SpringEL`표현식을 사용하여 변수를 표현할 수 있음

```java
${data}
```

* Object의 프로퍼티 접근법
  * member.id
  * member.['id']
  * member.getId()
    * 모두 `member`의 `id`필드를 조회하는 표현식

* List 컬렉션의 요소 접근
  * list[0]
    * `list`의 `0번째 요소` 조회하는 표현식

* Map 컬렉션의 밸류 접근
  * map['memberA']
    * `map`의 `memberA`의 밸류를 조회하는 표현식

## 기본 객체

<table>
<tr>
    <td>HttpServletRequest</td>
    <td>${#request}</td>
</tr>
<tr>
    <td>HttpServletResponse</td>
    <td>${#response}</td>
</tr>
<tr>
    <td>HttpSession</td>
    <td>${#session}</td>
</tr>
<tr>
    <td>ServletContext</td>
    <td>${#sevletContext}</td>
</tr>
<tr>
    <td>Locale</td>
    <td>${#locale}</td>
</tr>
</table>

* 파라미터 접근
  * 파라미터 접근은 기본적으로 `HttpServletRequest`객체에서 getParameter()로 접근해야하 함
  * ${param.파라미터명}

* 세션 접근
  * ${session.세션명}

