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

> ## 문법

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
