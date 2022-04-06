# SQL (Structured Query Language)
* 구조화된 질의 언어
* 서버<===(질의, 응답)==>클라이언트
### SQL 작성법
1. 대소문자는 구분하지 않음 / 조회 및 비밀번호는 구분함
2. 단어 단위로 띄어쓰기, 줄바꿈 상관 없음
3. 절별로 줄바꿈 권장
4. 키워드는 대문자, 그외(테이블명, 컬럼명, ...) 소문자 권장
5. 탭, 공백, 줄바꿈 사용하여 가독성 높임

> ## SQL의 종류
### DQL(Data Query Language)
* 데이터 검색, 조회
  * SELECT

### DDL(Data Difinition Language)
* 테이블 생성, 수정
  * CREATE
  * ALTER
  * DROP

### DML(Data Manipulation Language)
* 행 추가, 수정, 삭제
  * INSERT
  * UPDATE
  * DELETE

### DCL(Data Control Language)
* 권한 부여, 제거
  * GRANT
  * REVOKE
  
### TCL(Transaction Contrl Language)
* DML에 의한 변경 관리
  * COMMIT
  * ROLLBACK
  * SAVEPOINT
---
> ## CREATE 문

### CREATE USER 문
* 계정 생성
```sql
CREATE USER 계정명
IDENTIFIED BY 비밀번호;
-- 추가 옵션
-- ...
```
* 계정은 대소문자 구분하지 않음
* 비밀번호는 대소문자 구분
* 계정 생성에는 권한이 필요

### CREATE TABLE 문
* 테이블 생성
```sql
CREATE TABLE emp
(
-- 사원들을 구별할 수 있는 고유한 키로 사원번호(empno)컬럼을 설정
    EMPNO NUMBER(4) CONSTRAINT PK_EMP PRIMARY KEY,  --PRIMARY KEY(PK) == 고유키
    ENAME VARCHAR2(10),
    JOB VARCHAR2(9),
    MGR NUMBER(4), 
    HIREDATE DATE, 
    SAL NUMBER(7,2), 
    COMM NUMBER(7,2),
    DEPTNO NUMBER(2) CONSTRAINT FK_DEPTNO REFERENCES DEPT  --부서테이블(dept)의 부서번호(deptno)를 참조
);
```
> ## ALTER 문
### ALTER USER 문
* 계정을 수정
```sql
ALTER USER hr 
IDENTIFIED BY lion
ACCOUNT UNLOCK;;
-- hr계정의 비밀번호를 lion으로 변경 + 잠금 상태 해제
```
> ## DROP 문
### DROP USER 문
* 계정을 삭제
* 삭제 할 떄, CASCADE 옵션은 계정이 소유하는 객체(스키마)들까지 같이 삭제
```sql
DROP USER scott CASCADE;
```
---
> ## GRANT 문
* "롤이나 권한"을 "사용자"에 부여
* "권한"을 "롤"에 부여
```sql
GRANT RESOURCE, CONNECT TO scott;
```
### 롤(ROLE)
* 다양한 권한 <==(부여, 제거)==> 다수 사용자
  1. 롤 생성 
  2. 롤에 권한 부여
  3. 사용자에게 롤 부여

> ## REVOKE 문
* 부여된 권한이나 롤을 제거
```sql
REVOKE RESOURCE, CONNECT FROM scott;
```
> ## INSERT


---
> ## SELECT 문
* DQL(Query)
* 대상 : 하나 이상의 테이블, 뷰
* 데이터를 가져오는 데 사용

### clause(절) 작성, 처리 순서
```sql
WITH        --1 (생략가능)
SELECT      --6
FROM        --2
WHERE       --3 (생략가능)
GROUP BY    --4 (생략가능)
HAVING      --5 (생략가능)
ORDER BY    --7 (생략가능)
```
### SELECT 절에서 사용하는 키워드
* DISTINCT : 컬럼에 중복된 내용 배제
* ALL : 중복된 내용도 모두 조회 (생략되어 있음)
* AS : 컬럼의 별칭(alias)을 부여 (생략할 수 있음)

### SELECT절 & FROM 절 
* 테이블 또는 뷰
```sql
SELECT * --모든 정보
FROM emp;
--FROM 스키마.테이블명;

SELECT ename
        , job
FROM emp;
-- emp 테이블에서 ename, job 컬럼만 조회
```
* 문자열 합치기
  * || 연산자
  * concat(a, b) : a와 b 문자열을 합침
```sql
SELECT ename || ' ' ||job AS "Name_Job"
--SELECT concat(concat(ename, ' '), job) "Name_Job"
--'SMITH CLERK'의 형태로 "Name_Job" 이름의 컬럼 생성 (AS 생략 가능)
FROM emp;
-- emp 테이블에서 ename, job 컬럼만 조회
```
* 숫자 연산 & null 값 처리
  * \+ 연산자
  * NVL(expr1, expr2) : expr1이 널일때 expr2로 변환
  * NVL2(expr1, expr2, expr3) : expr1이 널이 아니면 expr2, 널이면 expr3로 변환
```sql
SELECT comm
        , NVL(comm, 0) -- comm이 null이면 0으로 출력
        , sal + NVL(comm, 0) -- sal과 NVL(comm, 0)덧셈 연산
FROM emp;
```

### WHERE 절
* 조건을 묻는 절
```sql
SELECT *
FROM emp
WHERE deptno = 10;
-- deptno 가 10인 값만 조회
```
* 날짜 비교
```sql
SELECT ibsadate, name
FROM insa
WHERE SUBSTR(ibsadate, 0, 2) = '98';
--WHERE ibsadate BETWEEN '1998.1.1' AND '1998.12.31';
--WHERE ibsadate >= '1998.1.1' AND ibsadate <= '1998.12.31';
--WHERE ibsadate >= '1998-01-01' AND ibsadate <= '1998-12-31';
--WHERE ibsadate >= '98/01/01' AND ibsadate <= '98/12/31';
-- YY/MM/dd형태인 날짜 ibsadate 컬럼에서 98년도에 해당되는 조건을 묻는 절들
```

### 연산자
* 비교 연산자  
  * = : 같은
  * !=, <>, ^= : 같지 않은
  * \>=, <=, >, < : 작거나 같은, ...
* 논리 연산자
  * NOT 연산자 : 부정 연산자
  * AND 연산자
    * true AND true : true
    * true AND false : false
    * true AND unknown : unknown
    * false AND false : false
    * false AND unknown : false
    * unknown AND unknown : unkonwn  
  * OR 연산자
    * true AND true : true
    * true AND false : true
    * true AND unknown : true
    * false AND false : false
    * false AND unknown : unkonwn
    * unknown AND unknown : unkonwn
* SQL 연산자
  * [NOT] IN(list) : list 값 중 같은 값이 있는지
  * [NOT] BETWEEN a AND b : a ~ b 값인지
  * IS [NOT] NULL : 널 값 인지
  * LIKE
    * 와일드카드로 일치하는 문자 판단
    * % : 갯수 상관 없음
    * _ : 한 개의 문자를 대신
### NULL 값
* 아직 정해지지 않은 값
* '', 0 과는 의미가 다름
* null값 확인 시, = 비교연산자 사용하지 않음
* IS NULL 연산자 사용

### ORDER BY 절
* 정렬을 위한 절
* ASC : 오름차순 (생략 시 기본)
* DESC : 내림차순
```sql
SELECT deptno, empno, ename, hiredate
FROM emp  
ORDER BY deptno , hiredate ;
ORDER BY deptno ASC, hiredate DESC;
-- 1차 정렬 : deptno 부서별로 1차 오름차순 정렬
-- 2차 정렬 : 입사일자를 기준으로 내림차순 정렬
```

### WITH 절
* 서브 쿼리
  * SQL 문 부속된 또다른 SQL문
  * 연산자 오른쪽에 위치
  * ()로 묶음
```sql
WITH temp AS (
    -- 서브쿼리(subquery)
    SELECT deptno, ename, sal + NVL(comm, 0) pay
    FROM emp
    WHERE deptno =30
)
SELECT t.* 
FROM temp t -- t 테이블의 별칭 선언
WHERE pay BETWEEN 1000 AND 2000;
```
* 인라인 뷰(inline view)
  * FROM절 안에 서브쿼리
```sql
SELECT t.*
FROM (
    SELECT deptno, ename, sal + NVL(comm, 0) pay
    FROM emp
    WHERE deptno =30
) t
WHERE t.pay BETWEEN 1000 AND 2000;
```

> ## 함수

### NVL(exp1, exp2)
* exp1의 값이 널일 때, exp2로 변환
### NVL2(exp1, exp2, exp3)
* exp1의 값이 널이 아닐 때 exp2, 널일 때 exp3로 변환

### SUBSTR(char, pos, [ length ])
* char문자열에 pos위치부터 length길이만큼 출력
* pos이 음수면 뒤에서 부터
### TO_CHAR(date, [ format, [ nlsparm ] ])
* 날짜를 포맷에 맞춰 출력
### EXTRACT(datetime)
* datetime이나 interval 값으로 특정 날짜/시간 정보를 추출
### REGEXP_LIKE(char, pattern, [ match_option ])
* 정규표현식으로 해당되는 문자열 평가

> ## Data Dictionary

* 메타 데이터(META DATA)
* 테이블 + 뷰의 집합
* 데이터베이스의 정보를 제공하는 역할
* DB생성 > SYS 계정 생성 > SYS 스키마 생성 > 내부에 테이블로 구성
### 접두사 종류
* dba_ : DB 전체에 포함되는 모든 객체에 대한 '자세한' 정보
* all_ : 자신이 생성한 객체 + 권한이 있는 객체 중 볼 수 있는 정보를
* user_ : 자신이 생성한 객체 정보
* V$_ : DB의 성능분석 / 통계 정보를 제공
