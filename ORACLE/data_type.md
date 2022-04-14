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

### NUMBER [ ( p [ , s ] ) ]
* p (precision, 정확도)
  * 표현할 유효숫자의 자리수
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

### FLOAT [ ( p ) ]
* 숫자 자료형
* p는 binary digit의 자리수

> ## 날짜
### DATE
* 날짜, 시간 정보를 갖는 자료형
* 고정길이 7 byte
* 세기, 년, 월, 월, 일, 시, 분, 초 저장

### TIMESTAMP [ ( n ) ]
* DATE타입에서 확장된 자료형
* 밀리초까지 저장
* n은 밀리초의 자리수
  * 생략 시, 6

> ## ROWID
* pseudo column(의사 컬럼)
  * 오라클 내부적으로 사용되는 컬럼
* 행에 대한 유니크한 식별자 역할
* ROWNUM, UROWID, ...
<table>
  <tr>
    <th colspan="4">AAAE5fAAEAAAAFMAAA</th>
  </tr>
  <tr>
    <td>ROWID</td>
    <td>의미</td>
    <td>크기</td>
    <td>내용</td>
  </tr>
  <tr>
    <td>AAAE5f</td>
    <td>Object 번호</td>
    <td>32bits</td>
    <td>객체 생성시 부여되는 유니크한 식별번호</td> 
  </tr>
  <tr>
    <td>AAE</td>
    <td>Relative file 번호</td>
    <td>10bits</td>
    <td>서로 다른 tablespace에 속해 있는 경우 식별하기 위한 번호</td> 
  </tr>  
  <tr>
    <td>AAAAFM</td>
    <td>Block 번호</td>
    <td>22bits</td>
    <td>해당 Block의 번호</td> 
  </tr>  
  <tr>
    <td>AAA</td>
    <td>Row 번호</td>
    <td>26bits</td>
    <td>Row의 일련번호, row가 생성될 때 순서대로 매김</td> 
  </tr>
</table>

> ## 그 외

### RAW
* 다른 시스템으로 이동 시, 오라클에 의해서 관리될 수 없는 데이터를 저장
  * 텍스트, 이미지, 동영상, ...
  * 2진 데이터
* ~ 2000 byte

### LONG RAW
* 다른 시스템으로 이동 시, 오라클에 의해서 관리될 수 없는 데이터를 저장
  * 텍스트, 이미지, 동영상, ...
  * 2진 데이터
* ~2GB

### BFILE
* 2GB 이상의 2진데이터 저장 시 사용

### LOB
* Large Object
  * 2GB 이상
* BLOB : 2진 데이터
* CLOB : 문자 데이터
* NCLOB : 유니코드 문자 데이터
