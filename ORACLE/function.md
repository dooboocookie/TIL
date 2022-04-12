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

# 단일행 함수

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

### CONCAT(char1, char2)
* 두 문자열을 합쳐 하나의 문자열로 변환
* || 결합 연산자와 비슷한 역할을 함
  
```sql
SELECT CONCAT('두부','쿠키') --'두부쿠키'
FROM dual;
```

### SUBSTR(char, pos, [ length ])
* char문자열에 pos위치부터 length길이만큼 출력
* pos이 음수면 뒤에서 부터


### INSTR(char1, char2 [, pos [, occurrence]])
* char1문자열에서 지정한 문자 char2를 찾아서 위치를 숫자로 반환
* pos은 검색 시작 위치 (양수면 좌측부터, 음수면 우측부터)
* occurrence번째 검색된 위치를 반환
```sql
SELECT INSTR('abcdabcdabcd', 'bc') -- 2
    , INSTR('abcdabcdabcd', 'bc', 3) -- 6
    , INSTR('abcdabcdabcd', 'bc', 3, 2) -- 10
    , INSTR('abcdabcdabcd', 'bc', -1, 1) -- 10
FROM dual;
```

### RPAD (expr1, n [, expr2] ) / LPAD
* 문자열 길이를 n으로 고정하고, expr1을 출력 후 남는 공간은 expr2로 채운다
* RPAD는 우측, LPAD는 좌측

### ASCII 코드값
* ASCII(char) : 문자를 아스키코드값으로 변환
* CHR(n) : n의 아스키코드값을 갖는 문자로 변환

### REPLACE(char1, char2, char)
* char1 문자열 중 char2를 char3로 대체하여 문자열로 변환

### REGEXP_LIKE(char, pattern, [ match_option ])
* 정규표현식으로 해당되는 문자열 평가

### VSIZE()
* 입력된 자료의 크기를 출력하는 함수
  * 한글 1문자 == 3바이트
  * 영문 1문자 == 1바이트
  * 숫자 == 2바이트 

>## 날짜 함수
### DATETIME 종류
|종류|내용|
|:---|:---|
|SYSDATE|시스템의 날짜 정보를 가져오는 함수| 
|CURRENT_DATE|시스템의 현재 날짜 정보를 가져오는 함수|
|CURRENT_TIMESTAMP|시스템의 현재 타임스탬프 날짜 정보를 가져오는 함수|
|EXTRACT(datetime)|datetime이나 interval 값으로 특정 날짜/시간 정보를 추출|


### TRUNC(date)
* 날짜 데이터를 특정위치를 절삭하는 함수
```sql
SELECT CURRENT_TIMESTAMP,
    TRUNC(CURRENT_TIMESTAMP), 
    -- 시간 정보를 절삭 / 00:00:00
    TRUNC(CURRENT_TIMESTAMP, 'DD'), 
    -- 일까지 출력 시 밑으로 절삭 / 00:00:00
    TRUNC(CURRENT_TIMESTAMP, 'MM'), 
    -- 월까지 출력 일 밑으로 절삭 / 22/04/01
    TRUNC(CURRENT_TIMESTAMP, 'YY'), 
    -- 년까지 출력 월 밑으로 절삭 / 22/01/01
    TRUNC(CURRENT_TIMESTAMP, 'DAY') 
    -- 요일 / 그 주의 첫날(일요일) 22/04/03
FROM dual;
```
### ROUND(date)
* 날짜 데이터의 특정위치를 반올림하는 함수
* 형식은 TRUNC()와 동일

### 날짜 연산
|연산|결과|
|:---|:---|
|날짜 - 날짜| = 숫자 (차이 일수)|
|날짜 ± 숫자| = 날짜 (숫자만큼 전(후) 날짜)|
|날짜 ± 숫자/24| = 날짜 (숫자만큼의 시간 차이)|

### MONTHS_BETWEEN(date1,date2)
* 두 날짜에 월의 차이를 반환
```sql
SELECT MONTHS_BETWEEN(SYSDATE, hiredate), -- 고용일로부터 지난 개월수
  MONTHS_BETWEEN(hiredate , SYSDATE)/12 -- 년수 계산
FROM emp;
```

### ADD_MONTHS(date, month)
* 날짜의 개월수를 더한 날짜를 출력
  * 1월 31일, 2월 28일, 4월 30일 같이 월의 마지막 날에서 연산 시 해당 월에 마지막 날로 계산 
```sql
SELECT ADD_MONTHS(TO_DATE('02-28-2022', 'MM-DD-YYYY'),  1),  -- 3월31일
  ADD_MONTHS(TO_DATE('02-27-2022', 'MM-DD-YYYY'),  1)  -- 3월27일
FROM dual;
```
### LAST_DAY()
* 해당 월의 마지막 날짜를 반환

### NEXT_DAY()
* 해당 요일의 돌아오는 날짜를 반환


> ## 형변환 함수

### TO_CHAR(date [, 'fmt' [, 'nlsparam'])
* 날짜를 포맷에 맞춰 문자열 출력

|기호|내용|기호|내용|
|:---:|:---|:---:|:---|
|년|Y,YY,YYY,YYYY,RR,RRRR,...|월|MM, MONTH, MON|
|일|DD(일/월) D(일/주) DDD(일/년)|요일|DY, DAY|
|시|HH, HH12, HH24|분|MI|
|초|SS, SSSSS|오전<br>오후|AM, PM|

```sql
SELECT TO_CHAR(SYSDATE, 'YYYY') -- '2022' 문자열로 출력
FROM dual;
```
### TO_DATE( char [, 'fmt' [, 'nlsparam']])
* 문자열을 포맷에 맞춰 날짜형으로 변환하는 함수
```sql
SELECT TO_DATE('2022.04.11'), -- 22/02/11(날짜형)
  TO_DATE('04.11.2022', 'MM,DD,YYYY'), --22/02/11(날짜형)
  TO_DATE('2022.04', 'YYYY.MM'), --22/04/01 : 일 입력 안하면 1일로 변환
  TO_DATE('11', 'DD') -- 22/04/11 : 년, 월 입력 안하면 해당년 해당월로 변환
FROM dual;
```

### TO_CHAR(number [,'fmt' [, 'nlsparam']])
* 숫자를 포맷에 맞춰 문자열로 변환하는 함수

|기호|내용|기호|내용|
|:---:|:---|:---:|:---|
|9|숫자|0|숫자, 공백 시 0으로 채움|
|,|쉼표 표기||.|소수점 표기|
|L|local currency symbol|||
```sql
SELECT TO_CHAR(1234567, '9,999,999'), -- '1,234,567' 
  TO_CHAR(1234567, 'L9,999,999.99'), -- '￦1,234,567.00'
  TO_CHAR(12, '0999') -- '0012'
FROM dual;
```


### TO_NUMBER()
* 문자를 숫자로 변환
* 숫자만 있는 문자열은 묵시적으로 숫자로 취급하기에 잘 사용은 안함

> ## NULL 처리 함수
### NVL(exp1, exp2)
* exp1의 값이 널일 때, exp2로 변환

### NVL2(exp1, exp2, exp3)
* exp1의 값이 널이 아닐 때 exp2, 널일 때 exp3로 변환

### NULLIF(expr1, expr2)
* 두 인자 값을 비교
* 같으면 NULL 반환
* 다르면 expr1 반환

### COALESCE(expr [, expr , ...])
* 순차적으로 인자 값에 대하여 NULL 체크
* NULL이 아닌 값 중 가장 처음 순서의 인자 반환


> ## IF문 역할하는 함수

### DECODE(expr, search1, result1 [, search2, result2,...][, default]);
* 다른 언어의 IF문과 같은은 역할을 함
  * PL/SQL에서 사용하기 위해 만들어진 함수
* 조건을 =(같다) 비교만 가능
* default (if문으로 따지면 else)를 안주면 null
```java
if (x ==1) return 'A';
else if (x==10)  return 'B';
else if (x==12) return 'C';
else if (x==14) return 'D';
else return 'E';  
```
* 자바에서의 IF문을 DECODE()로 표현해보면..
```sql
SELECT DECODE(x, 1,A, 10,B, 12,C, 14,D, E)
FROM dual;
```

### CASE
* DECODE보다 더 개선된 함수
* 형식
```sql
SELECT CASE x
    WHEN 1 THEN 'A'
    WHEN 10 THEN 'B'
    WHEN 12 THEN 'C'
    WHEN 14 THEN 'D'
    ELSE 'E'
  END
FROM dual; 
```
* 비교, 산술, 관계 연산자 사용 가능
```sql
SELECT emp.*,  
    CASE
    WHEN deptno IN (10, 20) THEN 'A팀'
    ELSE 'B팀'
  END AS "팀명"
FROM emp; 
-- deptno가 10, 20인 사원은 A팀 나머지는 B팀
```

> ## 순위 함수 (TOP_N)
### ROWNUM
* 함수 아님
* 오라클 내부에서 사용되는 의사 컬럼(pseudo column)
* SELECT문으로 조회된 행들의 순서번호

### RANK
* 그룹 내 순위를 계산하여 NUMBER타입으로 순위를 반환
* 중복 순위 계산
```sql
RANK ( ) OVER ([PARITION BY 절] ORDER BY절 )
```

### DENSE_RANK()
* 그룹 내 순위를 계산하여 NUMBER타입으로 순위를 반환
* 중복 순위 계산 안함
```sql
DENSE_RANK ( ) OVER ([PARITION BY 절] ORDER BY절 )
```

### ROW_NUMBER()
* 정렬된 결과에 대해 순번을 NUMBER타입으로 반환
* 같은 순위도 순번이 다름
```sql
ROW_NUMBER( ) OVER ([PARITION BY 절] ORDER BY절 )
```
```sql
-- deptno 별 sal이 TOP 2인 정보 조회
SELECT t.*
FROM (SELECT  emp.*, RANK() OVER(PARTITION BY deptno ORDER BY sal DESC) seq FROM emp) t
WHERE seq <= 2;

SELECT t.*
FROM (SELECT  emp.*, DENSE_RANK() OVER(PARTITION BY deptno ORDER BY sal DESC) seq FROM emp) t
WHERE seq <= 2;

SELECT t.*
FROM (SELECT  emp.*, ROW_NUMBER() OVER(PARTITION BY deptno ORDER BY sal DESC) seq FROM emp) t
WHERE seq <= 2;
```

### PERCENT_RANK()
* 첫 행을 0 마지막 행을 1로 순번을 비율로 나타냄


# 그룹 함수

* 그룹의 인풋을 하나의 결과로 출력
* SELECT절이나 HAVING절에 사용
* HAVING절은 그룹을 제한
* GROUP BY절은 행을 그룹
* 그룹 함수와 행이 여러개인 일반 컬럼을 같이 조회할 수 없음

### COUNT()
* 컬럼의 갯수를 출력
* DISTINCT : 중복 제거
* ALL (기본 값) : 중복 포함
* \* : 널을 포함한 행

```sql
SELECT  COUNT(*)
FROM emp
WHERE deptno =10;
-- deptno가 10인 레코드 수 / 3

SELECT  COUNT(DISTINCT deptno)
FROM emp;
-- 중복을 제외한 deptno컬럼의 수 / 3(10, 20, 30)
```

### SUM()
* (NULL 제외) 합을 출력

### AVG()
* (NULL 제외) 평균을 출력

### MAX()
* (NULL 제외) 최대값을 출력

### MIN()
* (NULL 제외) 최소값을 출력

### STDDEV()
* (NULL 제외) 표준편차를 출력

### VARIANCE()
* (NULL 제외) 분산을 출력
