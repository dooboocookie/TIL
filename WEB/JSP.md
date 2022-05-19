# JSP (Java Server Page)

> ## \<form>\</form>

* html 태그
* 웹 페이지의 입력 양식을 의미
* 요소
  * name 
    * 폼의 이름
    * 데이터의 이름으로 지정
  * action
    * 데이터가 전송되는 백엔드 URL 
  * method
    * get : 쿼리스트링 &rarr; ?name속성값=입력값&...
      * 보안 취약
      * 기본 값
    * post : http 내부 저장 전송
      * 보안 안정적

> ## \<input>\<input>

* 입력하기 위한 태그
* 요소
  * type
    * 입력 종류 
    * 텍스트, 버튼, ...
  * name
    * 데이터 이름
  * value
    * 기본 값
<table>
    <caption>input type 종류</caption>
    <tr>
        <td>submit</td>
        <td>< form > 요소의 데이터를 서버로 전송</td>
    </tr>
    <tr>
        <td>reset</td>
        <td>< form > 의 데이터 초기화</td>
    </tr>
    <tr>
        <td>text</td>
        <td>문자 입력</td>
    </tr>
    <tr>
        <td>button</td>
        <td>버튼 형식</td>
    </tr>
    <tr>
        <td>radio</td>
        <td>라디오버튼<br>name속성이 같은 버튼끼리 그룹</td>
    </tr>
    <tr>
        <td>checkbox</td>
        <td>체그박스<br>name속성이 같은 체크박스끼리 그룹, 중복 가능</td>
    </tr>
    <tr>
        <td>file</td>
        <td>파일 첨부<br>multiple속성으로 여러 파일 선택 가능</td>
    </tr>
    <tr>
        <td>password</td>
        <td>비밀번호<br>*표로 표시</td>
    </tr>
    <tr>
        <td>date</td>
        <td>날짜 형식</td>
    </tr>

</table>
