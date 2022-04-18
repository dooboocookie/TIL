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
#  DDL (Date  Dfinition Language)
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
1. 일반적인 방법
* 형식
```sql
CREATE [GLOBAL TEMPORARY] TABLE [스키마명.]테이블명(
  컬럼명 자료형 [DEFAULT 표현식] [제약조건]
  , ...
);
```
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

2. 서브쿼리를 이용한 방법
   * 쿼리를 실행하여 그 결과의 테이블을 만드는 방법
   * 기존 테이블을 복사 후 수정해서 사용하기에 용이함
   * 테이블 구조만 복사하기 위해서 사용하기도 함
   * 제약조건은 복사 안됨(NOT NULL 제외)
  * 형식
```sql
CREATE TABLE 테이블명 [(컬럼명 [, ...])] 
```
```sql
CREATE TABLE tbl_emp10
AS (
    SELECT *
    FROM emp
    WHERE deptno=10
);
-- emp 테이블에서 deptno가 10인 레코드로만 tbl_emp10 테이블 생성
-- 컬럼명 생략 시 서브쿼리와 같은 컬럼명
```
```sql
CREATE TABLE tbl_copy
AS (
    SELECT *
    FROM emp
    WHERE 1=0 -- 항상 거짓인 조건
);
-- 테이블 레코드를 제외하고 구조만 복사
```

### 제약조건
1. 데이터의 '무결성 제약조건'(integrity constraint)'을 위해 레코드 추가, 수정, 삭제 시 적용되는 규칙
2. 테이블 삭제 방지의 역할도 함

* 데이터 무결성

<table>
  <tr>
    <td>종류</td>
    <td>내용</td>
  </tr>
  <tr>
    <td>개체 무결성<br>(Entity Integrity)</td>
    <td>릴레이션에 저장되는 튜블의 유일성을 보장하기 위한 제약조건</td>
  </tr>
  <tr>
    <td>참조 무결성<br>(Relational Integrity)</td>
    <td>릴레이션 간 데이터의 "일관성"을 보장하기 위한 제약조건</td>
  <tr>
    <td>개체 무결성<br>(Entity Integrity)</td>
    <td>컬럼의 값의 데이터 타입, 길이, 기본 키, 유일성, null허용,... 제약조건</td>
  </tr>
</table>

* 제약조건 종류
<table>
  <tr>
    <td>제약조건</td>
    <td>타입</td>
    <td>내용</td>
  </tr>
  <tr>
    <td>PRIMARY KEY (PK)</td>
    <td>P</td>
    <td>기본키(고유키, PRIMARY KEY)<br>유일한  값들로 이루어져야 함<br> NULL 허용 X</td>
  </tr>
  <tr>
    <td>FOREIGN KEY (FK)</td>
    <td>R</td>
    <td>외래키(참조키, FOREIGN KEY)<br>다른 테이블의 기본키를 참조</td>
  </tr>  
  <tr>
    <td>UNIQUE (UK)</td>
    <td>U</td>
    <td>유일성 제약조건<br>해당 컬럼에 데이터들은 중복되지 않고 유일</td>
  </tr>
  <tr>
    <td>CHECK (CK)</td>
    <td>C</td>
    <td>조건 설정</td>
  </tr>
  <tr>
    <td>NOT NULL (NN)</td>
    <td>C</td>
    <td>NULL 허용 X</td>
  </tr>
</table>

### 선언
1. 컬럼 레벨 (column level)
  * IN-LINE constraint 방법
  * CREATE TABLE 문에서 컬럼 선언 시 같은 라인에 작성
```sql
CREATE TABLE tbl_column_level
(
  -- 고유키
  empno NUMBER(4) NOT NULL CONSTRAINTS PK_TBLCOLUMNLEVEL_EMPNO PRIMARY KEY,
  -- NOT NULL
  ename VARCHAR2(20) NOT NULL,
  -- 외래키
  deptno NUMBER(2) NOT NULL CONSTRAINTS FK_TBLCOLUMNLEVEL_DEPTNO REFERENCES dept(deptno),
  -- CHECK
  kor NUMBER(3) CONSTRAINTS CK_TBLCOLUMNLEVEL_KOR CHECK (kor BETWEEN 0 AND 100),
    -- 유일성 제약조건
  email VARCHAR2(50) CONSTRAINTS UK_TBLCOLUMNLEVEL_EMAIL UNIQUE,
  city VARCHAR2(20)
);
```
2. 테이블 레벨 (table level)
  * OUT_OF_LINE constraint 방법
  * CREATE TABLE 문에서 컬럼 선언 라인과 다른 줄에 선언
    * NOT NULL은 선언 불가
  * ALTER TABLE 문으로 추가 시 사용 
```sql
CREATE TABLE tbl_table_level
(
    empno NUMBER(4) NOT NULL,
    ename VARCHAR2(20) NOT NULL,
    deptno NUMBER(2) NOT NULL,
    kor NUMBER(3),
    email VARCHAR2(50),
    city VARCHAR2(20),
    
    --PK 제약조건 설정
    CONSTRAINTS PK_TBLTABLELEVEL_empno PRIMARY KEY(empno), --복합키
    CONSTRAINTS FK_TBLTABLELEVEL_DEPTNO FOREIGN KEY(deptno) REFERENCES dept(deptno),
    CONSTRAINTS UK_TBLTABLELEVEL_EMAIL UNIQUE(email),
    CONSTRAINTS CK_TBLTABLELEVEL_KOR CHECK (kor BETWEEN 0 AND 100)
);
```

### 삭제
```sql
ALTER TABLE 테이블명
DROP PRIMARY KEY;

ALTER TABLE 테이블명
DROP CONSTRAINT 제약조건명
```
### 활성화 / 비활성화
1. 비활성화 (DISABLE)
     * 제약조건을 체크하지 않음
```sql
ALTER TABLE 테이블명
DISABLE CONSTRAINT 제악조건명 [CASCADE];
```
2. 활성화 (ENABLE)
     * 비활성화된 제약조건을 활성화
```sql
ALTER TABLE 테이블명
ENABLE CONSTRAINT 제악조건명;
```

### FOREIGN KEY 삭제 옵션
1. ON DELECT CASCADE
* 부모키 삭제 시, 참조키에 해당되는 레코드들도 삭제
```sql
ALTER TABLE tbl_emp
ADD CONSTRAINT FK_TBLEMP_DEPTNO FOREIGN KEY (deptno) REFERENCES tbl_dept (deptno) ON DELETE CASCADE;

DELETE FROM tbl_dept
WHERE deptno = 30;
```
2. ON DELECT SET NULL
* 부모키 삭제 시, 참조키에 해당되는 레코드들의 해당 컬럼은 NULL값으로 바뀜
```sql
ALTER TABLE tbl_emp
ADD CONSTRAINT FK_TBLEMP_DEPTNO FOREIGN KEY (deptno) REFERENCES tbl_dept (deptno) ON DELETE SET NULL;

DELETE FROM tbl_dept
WHERE deptno = 30;
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

### ALTER TABLE 문
* 테이블의 컬럼을 추가, 삭제, 변경에 사용
1. 추가
      *  컬럼을 추가
      *  제약조건을 추가
```sql
ALTER TABLE 테이블명
ADD (
  컬럼명 자료형 [DEFAULT 표현식] [제약조건]
  , ...
)
```
2. 수정
      * 컬럼을 수정 (한번에 한 컬럼씩 삭제)
      * 제약조건은 수정이 불가
```sql
ALTER TABLE 테이블명
MODIFY (
  컬럼명 자료형 [DEFAULT 표현식]
  , ...
)
```
3. 컬러명 변경
```sql
ALTER TABLE 테이블명
RENAME COLUMN 전_컬럼명 TO 후_컬럼명
```
4. 삭제
      * 컬럼을 삭제
      * 제약조건을 삭제
```sql
ALTER TABLE 테이블명
DROP COLUMN 컬럼명;

ALTER TABLE 테이블명
DROP [CONSTRAINT] 제약조건;
```
### RENAME
* 테이블, 뷰, ... 이름변경
```sql
RENAME 전_컬럼명 TO 후_컬럼명
```
> ## DROP 문
### DROP USER 문
* 계정을 삭제
* 삭제 할 떄, CASCADE 옵션은 계정이 소유하는 객체(스키마)들까지 같이 삭제
```sql
DROP USER scott CASCADE;
```

### DROP TABLE 문
* 테이블을 삭제
* 형식
```sql
DROP TABLE [스키마명.]테이블명 [CASCADE CONSTRAINTS] [PURGE];
```
* CASCADE CONSTRAINTS
  * 무결성 제약조건 삭제 
  * 대상 테이블의 기본키를 다른 테이블에서 참조키로 사용 중일 떄 삭제하기 위함
* PURGE
  * 완전히 삭제



# DML(Data Manipulation Language)

> ## INSERT 문
* 테이블의 행을 추가하는 문
* 추가 후 COMMIT이나 ROLLBACK 트랜잭션 처리 필수
* 형식
```sql
INSERT INTO 테이블명 [ (컬럼명,...) ] VALUES (컬럼값,...);
```
```sql
INSERT INTO dept (deptno, dname, loc) VALUES (50, 'QC', 'SEOUL');
COMMIT;
```

### 서브쿼리 INSERT 문
* 서브쿼리의 결과를 삽입
* 서브쿼리의 결과의 컬럼들과 대상 테이블의 컬럼들이 일치 해야 함
```sql
CREATE TABLE tbl_emp10
AS (SELECT * FROM emp WHERE 1=0);

INSERT INTO tbl_emp10
(
  SELECT *
  FROM emp
  WHERE deptno = 10
);
COMMIT;
-- emp 테이블에 deptno가 10인 레코드들 tbl_emp10테이블에 삽입
```

### 다중테이블 INSERT 문
1. unconditional insert all
* 조건 없이 서브쿼리의 결과 행들을 모두 추가
```sql
INSERT ALL | FIRST
  INTO 테이블1 VALUES (컬럼1,컬럼2,...)
  [INTO 테이블2 VALUES (컬럼1,컬럼2,...)]
  ...
서브쿼리;
```

2. conditional insert all
* 서브쿼리의 결과 행들 중 조건에 맞는 행들을 모두 추가
```sql
INSERT ALL
WHEN 조건1 THEN
    INTO 테이블1 VALUES(컬럼1,컬럼2,...)
WHEN 조거2 THEN
    INTO 테이블2 VALUES(컬럼1,컬럼2,...)
...
ELSE
    INTO 테이블3 VALUES(컬럼1,컬럼2,...)
서브쿼리; 
```
3. conditional firest insert
* 서브쿼리의 결과 행들 중 조건에 만족하는 첫번째 테이블에만 행 추가
```sql
INSERT FIRST
WHEN 조건1 THEN
    INTO 테이블1 VALUES(컬럼1,컬럼2,...)
WHEN 조거2 THEN
    INTO 테이블2 VALUES(컬럼1,컬럼2,...)
...
ELSE
    INTO 테이블3 VALUES(컬럼1,컬럼2,...)
서브쿼리; 
```

4. pivoting insert
* INTO 절 뒤에 오는 테이블을 모두 동일하게
```sql
INSERT ALL
[WHEN 조건 THEN]
    INTO 테이블1 VALUES(컬럼1,컬럼2,...)
    INTO 테이블1 VALUES(컬럼1,컬럼2,...)
    ...
서브쿼리; 
```

> ## UPDATE 문
* 조건에 맞는 행에 열을 수정하는 문
* 조건이 없으면 전체 행 수정
* 수정 후 COMMIT이나 ROLLBACK 트랜잭션 처리 필수
* 형식
```sql
UPDATE 테이블명 SET 컬럼 = 값[, ...] [WHERE 조건식];
```
```sql
UPDATE dept
SET loc = 'BUSAN'
WHERE deptno = 50;
COMMIT;
```


> ## DELETE 문
* 조건에 맞는 행을 삭제하는 문
* 조건이 없으면 전체 행 삭제
* 조건은 보통 중복 값이 없는 고유키(PK)로 하는 것이 일반적
* 삭제 후 OMMIT이나 ROLLBACK 트랜잭션 처리 필수
* 형식
```sql
DELETE 테이블명 [WHERE 조건식];  
```
```sql
DELETE dept
WHERE deptno = 50;
COMMIT;
```

> ## MERGE 문
1. 구조가 같은 두 테이블을 하나의 테이블로 합치는 문
2. 대량의 데이터는 쿼리문의 성능이 떨어짐으로, 나눠서 관리하던 데이터를 하나로 합칠 때 유용
* 처리
  * 매치되는 행이 존재하면 더하여 UPDATE
  * 매치되는 행이 없으면 INSERT
```sql
MERGE INTO 스키마명.테이블명
USING (서브쿼리) 
ON (조건문)  
WHEN MATCHED THEN -- UPDATE
    UPDATE SET 컬럼명 = 값 [, ...]
WHEN NOT MATCHED THEN -- INSERT
    INSERT (컬럼명[, ...]) VALUES (값 [, ...]);
```


# DCL (Data Control Language)
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


---
# SELECT 문 (Query)
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
|키워드|내용|
|:---:|:---|
|DISTINCT|컬럼에 중복된 내용 배제|
|ALL|중복된 내용도 모두 조회 (생략되어 있음)|
|AS|컬럼의 별칭(alias)을 부여 (생략할 수 있음)|

> ## SELECT절 & FROM 절 
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

### JOIN 
* 두 테이블을 연결하기 위한 문
* FROM 절에서 사용
* 두 테이블을 연결하기 위한 조건이 필요
  * WHERE절이나 ON뒤에 조건을을 붙임 

```sql
SELECT d.danme, e.*
FROM emp e JOIN dept d ON e.deptno = d.deptno;
-- emp 테이블에 없고 dept 테이블에 있는 dname이라는 컬럼을
-- d.deptno(PK) 와 e.deptno(FK)를 통해서 JOIN하여 조회
```
> ## WHERE 절
* 조건을 묻는 절
* 절안에서 연산자들을 많이 씀
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



> ## ORDER BY 절
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

> ## WITH 절
* 서브쿼리 블럭을 미리 선언하여 나중에 반복하여 사용하기 위한 절
* 하나의 WITH절에 여러개 쿼리 블럭 사용 가능
* (WITH절이 없는) SELECT 문 이 쿼리 블럭 안에 포함
* 코딩을 간결하게 함
> ## 서브 쿼리
  * SQL 문 부속된 또다른 SQL문
  * 연산자 오른쪽에 위치
  * ()로 묶음
  * ORDER BY절을 사용할 수 없음

|위치|이름|
|:---|:---|
|FROM 절|Inline view|
|WHERE 절|Nested subquery|
|parent, child관계| Correlated subquery|

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
  * 하나의 테이블 명처럼 사용되는 서브쿼리
```sql
SELECT t.*
FROM (
    SELECT deptno, ename, sal + NVL(comm, 0) pay
    FROM emp
    WHERE deptno =30
) t
WHERE t.pay BETWEEN 1000 AND 2000;
```
### 상관 서브 쿼리(Correlated subquery)  
* 일반 서브 쿼리의 경우, 결과를 메인 쿼리에서 이용 
* 상관 서브 쿼리는 서브 쿼리 안에서 메인 쿼리의 값을 이용
  * 서브쿼리에서 메인쿼리의 값 사용
  * 그 서브쿼리의 결과를 메인 쿼리에서 사용

```sql
SELECT *
FROM emp e
WHERE sal = (SELECT MAX(sal) FROM emp WHERE deptno = e.deptno);
-- 조회하려는 행의 deptno의 sal의 최대값을 조회하는 서브쿼리
```

> ## GROUP BY 절
* 레코드들의 그룹을 만들기 위한 절
* 그룹에 대한 정보를 한 행으로 표시
* 그룹 함수를 사용하는 쿼리문에서 자주 사용

```sql
SELECT MAX(sal) max_pay
FROM emp;
-- sal의 최댓값 출력

SELECT deptno,
   MAX(sal) max_pay
FROM emp
GROUP BY deptno;
-- 부서별(deptno로 그룹화) sal 최대값
```

### ROLLUP, CUBE
* GROUP BY 절에 쓰이는 연산자
* 그룹에 대해 부분합을 구하는 연산자
* ROLLUP은 (GROUP BY 컬럼 수) + 1 개의 부분합 출력
  * deptno별 - job별 부분합
  * deptno별 부분합
  * 전체의 부분합
```sql
SELECT deptno, job, count(*)
FROM emp
GROUP BY ROLLUP (deptno, job);
```
|deptno|clerk|salesman|manager|analyst|president|부분합|
|:---:|:---:|:---:|:---:|:---:|:---:|:---:|
|10|1|-|1|-|1|3|
|20|1|-|1|1|-|3|
|10|1|4|1|-|-|6|
|부분합|-|-|-|-|-|12|

* CUBE는 (GROUP BY 컬럼 수) * 2 개의 부분합 출력
  * deptno별 - job별 부분합
  * deptno별 부분합
  * job별 부분합
  * 전체의 부분합
```sql
SELECT deptno, job, count(*)
FROM emp
GROUP BY CUBE (deptno, job);
```
|deptno|clerk|salesman|manager|analyst|president|부분합|
|:---:|:---:|:---:|:---:|:---:|:---:|:---:|
|10|1|-|1|-|1|3|
|20|1|-|1|1|-|3|
|10|1|4|1|-|-|6|
|부분합|3|4|3|1|1|12|

> ## HAVING 절
* GROUP BY 절에서 그룹화한 그룹에 대한 조건을 주는 절
* 반드시 GROUP BY 뒤에 위치 (단독으로는 사용 불가)
* WHERE절과 달리 그룹 함수 같이 그룹에 대한 조건이 가능
```sql
SELECT deptno, MAX(sal) --  [5]부서번호(deptno), 최대급여(sal) 조회하고
FROM emp -- [1] emp 테이블에서
WHERE EXTRACT(YEAR FROM hiredate) = 1981; -- [2] 입사일이 81년도인 사람들을
GROUP BY deptno -- [3] 부서별로 그룹지어(deptno로 그룹화)
HAVING COUNT(*) >= 2 -- [4] 부서원수(그룹의 행 수)가 2명 이상인
ORDER BY deptno; -- [6] 부서번호로 오름차순 정렬하여 출력하라

-- [번호] 순서대로 처리
```

> ## 계층적 절의 (LEVEL)

* LEVEL
  * 의사 칼럼
  * 테이블에서 행의 LEVEL을 가리키는 일련번호
* 형식 
```sql
SELECT LEVEL {, 컬럼 [, ...]}
FROM 테이블명
WHERE 조건
START WITH 조건
CONNECT BY [PRIOR 컬럼1 비교연산자 컬럼2]|[컬럼1 비교연산자 PRIOR 컬럼2]
```
### START WITH 절
* 최상위 행을 나타내는 조건식

### CONNECT BY 절
* 계층관계를 지정하는 절
* PRIOR 연산자
  * TOP-DOWN / BOTTOM-UP 방식을 결정


|TOP-DOWN|BOTTOM-UP|
|:---|:---|
|CONNECT BY PRIOR 자식키 = 부모키|CONNECT BY PRIOR 부모키 = 자식키|
|최상위 계층부터 출력|최하위 계층부터 출력|

* LEVEL 함수

|함수|반환|
|:---|:---|
|CONNECT_BY_ISLEAF|LEAF(하위) 데이터가 없으면 1, 있으면 0을 반환|
|CONNECT_BY_ISCYCLE|ROOT(최상위) 데이터면 1, 아니면 0을 반환|
|CONNECT_BY_ROOT|해당 데이터의 ROOT 데이터 값을 반환|

### 가지 제거
* CONNECT BY 절을 통한 가지 제거
```sql
SELECT 
  LPAD(' ', (LEVEL-1)*3) || ename '계층도'
FROM emp
START WITH mgr IS NULL
CONNECT BY PRIOR empno = mgr AND ename != 'CLARK';
--'CLARK'에서 가지 제거
--'CLARK'과 그 하위 계층('CLARK'을 매니저로 두는 레코드)는 출력 안함
```
