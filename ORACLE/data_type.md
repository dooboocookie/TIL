# DATA TYPE(자료형)
> ## 문자

### CHAR [ ( size [ BYTE ¦ CHAR ] ) ]
* 고정 길이, 바이트단위 문자 자료형
* size 생략 시, 1 byte
* BYTE | CHAR 단위 생략 시, BYTE

### NCHAR [ ( size ) ]
* 고정 길이, 유니코드 단위 문자 자료형
* size 생략 시, 1 문자

### VARCHAR2 [ ( size [ BYTE ¦ CHAR ] ) ]
* 가변 길이, 바이트단위 문자 자료형
* size 생략 시, 4000 byte(최대)
* BYTE | CHAR 단위 생략 시, BYTE 

### NVARCHAR2 [ ( size ) ]
* 고정 길이, 유니코드 단위 문자 자료형
* size 생략 시, 4000 byte(최대)


<table>
  <tr>
    <td ></td>
    <td colspan="2">바이트</td>
    <td colspan="2">유니코드(문자)</td>
  </tr>
  <tr>
    <td></td>
    <td>타입</td>
    <td>범위</td>
    <td>타입</td>
    <td>범위</td>
  </tr>
  <tr>
    <td>고정 길이</td>
    <td>CHAR</td>
    <td>1 byte ~ 2000 byte</td>
    <td>NCHAR</td> 
    <td>1 문자 ~ 2000 btye</td>
  </tr>
  <tr>
    <td>가변 길이</td>
    <td>VARCHAR2</td>
    <td>1 byte ~ 4000 byte</td>
    <td>NVARCHAR2</td> 
    <td>1 문자 ~ 4000 btye</td>
  </tr>
</table>

* 주민번호, 우편번호 같이 길이가 정해진 문자열은 고정 길이
* ID, 글 제목 같이 길이가 변하는 문자열은 가변 길이

### LONG
* 가변 길이 문자 자료형
* 최대 범위 2GB

> ## 숫자

### NUMBER[ ( p [ , s ] ) ]
* p (precision, 정확도)
  * 유효숫자의 자리수
  * 1 ~ 38 범위
* s (scale, 정밀도)
  * 반올림하여 표현할 자리수
  * -84 ~ 127 범위
* NUMBER(p) == NUMBER(p,0)
* NUMBER == NUMBER(p(최대값), s(최대값))

|NUMBER()|입력 데이터|저장 값|
|:---|:---|:---|
|NUMBER|123.141592|123.141592|
|NUMBER(3)|123.141592|123|
|NUMBER(5,2)|123.141592|123.14|
|NUMBER(3,2)|123.141592|precision 초과|
|NUMBER(3,-2)|123.141592|100|
|NUMBER(3,7)|3.14e-6|0.0000031|
|NUMBER(3,-5)|3.14e6|3100000|
