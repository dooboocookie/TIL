# 오라클 함수
* 복잡한 쿼리문을 간단히
* 데이터 값을 조작
* 기능
  * 데이터 계산
  * 데이터 변경
  * 그룹의 결과를 출력(그룹 함수)
  * 날짜 형식 변경
  * 데이터 타입 변경

### 유형
|유형|내용|
|:---:|:---|
|단일행함수<br>(Single-row)|각 행을 대상으로 함수를 적용하여 각 행에 대한 결과를 반환|
|그룹함수<br>(Group, 복수행)|여러 행을 그룹으로 하여 그룹별로 결과를 하나 반환|

> # 단일행 함수

>## 숫자 함수

### ROUND(number[, m])
* number 숫자에 대해서 반올림한 결과를 반환
* m은 반올림할 자리를 의미
* 10^(-m)자리 수 까지 표현
* m 생략 시, 0 > 즉 1의 자리까지 표현 > 소수점 첫째 자리에서 반올림
```sql
SELECT ROUND(3.141592) --3
    , ROUND(3.141592, 2) --3.14
    , ROUND(123.141592,-1) --120  
FROM dual;
```

### TRUNC(number [, m])
* number 숫자에 대해서 절삭한 결과를 반환
* m은 절삭할 자리를 의미
* 10^(-m)자리 수 까지 표현
* m 생략 시, 0 > 즉 1의 자리까지 표현 > 소수점 첫째 자리부터 절삭
* FLOOR(number) : 소수점 첫째자리에서 절삭
```sql
SELECT TRUNC(3.541592) --3
    , TRUNC(3.146592, 2) --3.14
    , TRUNC(125.141592,-1) --120  
FROM dual;
```
### CEIL(number)
* number 숫자에 대해서 올림한 결과를 반환
* 소수점 첫째자리에서 올림
```sql
SELECT CEIL(3.141592) --4
    , CEIL(3.141592*100)/100 --3.15
    , CEIL(123.141592/10)*10 --130  
FROM dual;
```
### MOD(num1, num2)
* num1을 num2로 나누었을 떄 나머지 값을 반환하는 함수
* num1 - (num2 * FLOOR(num1 / num2)) 계산으로 나머지를 구함
  * REMAINDER()의 경우 버림대신 반올림으로 계산하는 함수

### SIGN(number)
* number 양수면 1 반환
* number 음수면 -1 반환
* number 0이면 0 반환

### ABS(number)
* number의절대값을 반환

> ## 문자 함수

### UPPER(char)
* 대문자로 변환

### LOWER(char)
* 소문자로 변환

### INITCAP(cahr)
* 첫글자만 대문자로 변환

### LENGTH(char)
* 문자열의 길이를 반환

> ### NVL(exp1, exp2)
* exp1의 값이 널일 때, exp2로 변환

> ### NVL2(exp1, exp2, exp3)
* exp1의 값이 널이 아닐 때 exp2, 널일 때 exp3로 변환

> ### SUBSTR(char, pos, [ length ])
* char문자열에 pos위치부터 length길이만큼 출력
* pos이 음수면 뒤에서 부터

> ### TO_CHAR(date, [ format, [ nlsparm ] ])
* 날짜를 포맷에 맞춰 출력

> ### EXTRACT(datetime)
* datetime이나 interval 값으로 특정 날짜/시간 정보를 추출

> ### REGEXP_LIKE(char, pattern, [ match_option ])
* 정규표현식으로 해당되는 문자열 평가

> ### UPPER(char)
* 대문자로 변환

> ### CONCAT(char1, char2)
* 두 문자열을 합쳐 하나의 문자열로 변환

> ### REPLACE(char1, char2, char)
* char1 문자열 중 char2를 char3로 대체하여 문자열로 변환

> ### SYSDATE
* 시스템의 날짜 정보를 가져오는 함수
  
> ### CURRENT_DATE
* 시스템의 현자 날짜 정보를 가져오는 함수
> ### CURRENT_TIMESTAMP
* 시스템의 현재 타임스탬프 날짜 정보를 가져오는 함수

> ### VSIZE()
* 입력된 자료의 크기를 출력하는 함수
  * 한글 1문자 == 3바이트
  * 영문 1문자 == 1바이트
  * 숫자 == 2바이트 


