# PL/SQL

* Procedural Language extensions to SQL
* 절차적인 언어로 확장된 SQL 문
  * 변수 선언
  * 제어문
  * 예외 처리 
  * ...

### PL/SQL 종류

<table>
    <tr>
        <td>PL/SQL</td>
        <td>내용</td>
    </tr>
    <tr>
        <td>익명 프로시저<br>(Anoymous Procedure)</td>
        <td>DECLARE 절로 시작<br>필요할 때 마다 작성하여 실행</td>
    </tr>
    <tr>
        <td>저장 프로시저<br>(Stored Procedure)</td>
        <td>CREATE POCEDURE 문으로 생성<br>DB에 프로시저를 저장하여 호출하여 사용</td>
    </tr>
    <tr>
        <td>저장 함수<br>(Stored Function)</td>
        <td></td>
    </tr>
    <tr>
        <td>패키지<br>(Package)</td>
        <td></td>
    </tr>
    <tr>
        <td>트리거<br>(Trigger)</td>
        <td></td>
    </tr>
    <tr>
        <td>객체 타입<br>(Object Type)</td>
        <td></td>
    </tr>
</table>

> ## 구조

### 블록 구조
* 3개의 블록 구조
  * 선언 부분 : 변수 및 상수 선언
  * 실행 부분 : 실행 내용, 제어문, ...
  * 예외 처리 부분
* 형식

```sql
DECLARE 
-- 선언문
BEGIN 
-- 실행문
EXCEPTION
-- 예외처리
END;
```
* 블럭 내, 여러 SQL문 사용 가능
* 블럭 내, GREATEST, LEAST, DECODE, 그룹함수 사용 불가

> ## 변수

### 변수 선언
* 선언 블럭에 선언

```sql
변수명 자료형(크기);

vname VARCHAR(20);
vage NUMBER(30);
```
<table>
    <tr>
        <td>형식</td>
        <td>내용</td>
    </tr>
    <tr>
        <td>%TYPE</td>
        <td>특정 컬럼의 데이터 타입과 크기를 그대로 참조</td>
    </tr>
    <tr>
        <td>%ROWTYPE</td>
        <td>특정 테이블의 모든 컬럼의 데이터 타입과 크기를 그대로 참조<br>컬럼명을 사용하여 자료형을 참조한다</td>
    </tr>
    <tr>
        <td>RECORD</td>
        <td>테이블로 읽은 한 레코드의 값을 그대로 저장하기 위해 다른 데이터타입을 여러개 선언<br>레코드명.변수명 </td>
    </tr>
</table>

```sql
DECLARE
    v_ename emp.ename%TYPE; 
    -- emp테이블의 ename의 자료형과 크기 참조
    v_emp_row emp%ROWTYPE;
    -- emp 테이블의 컬럼들의 자료형을 참조
    TYPE deptType IS RECORED (
        v_deptno dept.deptno%TYPE,
        v_dname dept.dname%TYPE
    )
    -- 레코드 변수
BEGIN
END;

```
### 변수 초기화
* := 사용

```sql
DECLARE
    vname VARCHAR(20);
    vage NUMBER(30);
BEGIN
    vname := '두부쿠키';
    vage := 27;
END;
```
> ## 제어문
### 조건문
* 형식
```sql
IF (조건식) THEN 실행문;
[ELSIF (조건식) THEN 실행문;]
[ELSIF (조건식) THEN 실행문;]
[...]
[ELSE 실행문;]
END IF;
```
```sql
DECLARE
    vkor NUMBER(3) := 0;
    vgrade VARCHAR2(10);
BEGIN
    vkor := :bindNumber;
    
    IF (vkor >= 90 )THEN
        vgrade := '수';
    ELSIF (vkor >= 80 )THEN
        vgrade := '우';
    ELSIF (vkor >= 70 )THEN
        vgrade := '미';
    ELSIF (vkor >= 60 )THEN
        vgrade := '양';
    ELSE 
        vgrade := '가';
    END IF;
    
    DBMS_OUTPUT.PUT_LINE(vgrade);
-- 점수 입력 받아 등급을 나타내는 문
END;
```

### 반복문
* FOR 루프
```sql
FOR counter변수 IN [REVERSE] 시작값.. 끝값
LOOP
    실행문;
END LOOP;
-- counter변수가 시작 값부터 끝 값까지 반복
```
* WHILE 루프
```sql
WHILE (조건식)
LOOP
    실행문;
END LOOP;
-- 조건식이 참일 동안 반복
```
* 단순 반복
```sql
LOOP
    EXIT WHEN (조건식) -- break
END LOOP;
-- 조건식이 참일 때 break 
```

> ## 커서(CURSOR)

* PL/SQL 블럭 내의 SELECT
<table>
    <tr>
        <td>묵시적 커서</td>
        <td>따로 커서를 선언하지 않고 일반적으로 SELECT문을 사용하는 경우</td>
    </tr>
    <tr>
        <td>명시적 커서</td>
        <td>커서를 선언하여 여러행으로 되어있는 SELECT문의 결과를 읽어오기 위해 사용</td>
    </tr>
</table>

* 속성
<table>
    <tr>
        <td>%ROWCOUNT</td>
        <td>현재 커서에서 지금까지 읽힌 행의 수</td>
    </tr>
    <tr>
        <td>%FOUND</td>
        <td>읽어올 행이 있을 떄 참을 출력</td>
    </tr>
    <tr>
        <td>%NOTFOUND</td>
        <td>읽어올 행이 없을 떄 참을 출력</td>
    </tr>
    <tr>
        <td>%ISOPEN</td>
        <td>커서가 OPEN 상태이면 참을 출력</td>
    </tr>
</table>

### 묵시적 커서
```sql
BEGIN
    FOR vrow IN (SELECT empno, ename FROM emp)
    LOOP
        DBMS_OUTPUT.PUT_LINE (vrow.empno || ', ' || vrow.ename);
    END;
    -- SELECT 문의 결과 행에 대해서 empno, ename을 출력하는 FOR 문
END;
```
### 명시적 커서 
* 선언 &rarr; OPEN &rarr; FETCH &rarr; CLOSE
```sql
DECLARE
    vempno emp.empno%TYPE;
    vename emp.ename%TYPE;
    -- 1) 선언
    CURSOR emp_cursor IS (
        SELECT empno, ename
        FROM emp
        WHERE deptno = 10;
    )
BEGIN
    -- 2) OPEN : 커서를 실행
    OPEN emp_cursor
    
    LOOP
        -- 3) FETCH : 커서에서 한 행씩 받아옴
        FETCH emp_cursor 
        INTO vempno, vename
        DBMS_OUTPUT.PUT_LINE(vempno || ', ' || vename);
        EXIT WHEN emp_cursor%NOTFOUND OR emp_cusor%ROWCOUNT >= 3;
    END LOOP;
    -- 4) CLOSE
    CLOSE emp_cursor;
END;
```

> ## 저장 프로시저 (Stored Procedure)
* 자주 실행하는 업무를 프로시저로 생성하여
* 데이터 베이스 내에 저장해 호출하여 사용하는 프로시저
* 생성
```sql
CREATE [OR REPLACE] PROCEDURE 프로시저명
(
    -- 파라미터 지정 [IN : 입력 / OUT : 출력 / INOUT : 입출력]
    파라미터명1 [IN|OUT|INOUT] 자료형, --(크기 지정 X)
    파라미터명2 [IN|OUT|INOUT] 자료형,
    ...
)
IS
    -- 변수 선언부
BEGIN
    -- 실행부
EXCEPTION
    -- 예외처리부
END;
```
* 사용
  1. EXECUTE 문
  2. 익명 프로시저나 다른 저장 프로시저 안에서 
```sql
--1
EXECUTE 프로시저명;

--2
BEGIN
    프로시저명;
END;
```