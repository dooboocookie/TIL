
# 연산자
> ## 비교 연산자  
* WHERE 절에서만 사용
* 숫자, 문자, 날짜를 비교
* TRUE, FALSE, NULL을 반환
### 종류
  * = : 같은
  * !=, <>, ^= : 같지 않은
  * \>=, <=, >, < : 작거나 같은, ...
  * SQL 연산자
    * ANY
    * SOME
    * ALL

> ## 논리 연산자
* WHERE 절에서만 사용
* TRUE, FALSE, NULL을 반환 
### 종류
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
> ## SQL 연산자
  * [NOT] IN(list) : list 값 중 같은 값이 있는지
  * [NOT] BETWEEN a AND b : a ~ b 값인지
  * IS [NOT] NULL : 널 값 인지
  * LIKE
    * 와일드카드로 일치하는 문자 판단
    * % : 갯수 상관 없음
    * _ : 한 개의 문자를 대신
    * EESCAPE '\'를 통해 와일드 카드(%, _)를 일반 문자로 판단하는 데 사용 
  * EXISTS 
    * WHERE(상관 서브쿼러가 존재하면 true로 반환)
    * IN으로도 표현가능
  * ALL
    * WHERE 절의 서브쿼리에 사용
    * 서브쿼리의 모든 레코드
```sql
SELECT * 
FROM emp
WHERE sal >= ALL (SELECT sal FROM emp);
-- emp테이블에서 가장 높은 sal을 가진 행 조회
```

> ## NULL 연산자
  * IS [NOT] NULL : 널 값 인지 판단하는 연산자
### NULL 값
* 아직 정해지지 않은 값
* '', 0 과는 의미가 다름
* null값 확인 시, = 비교연산자 사용하지 않음
* IS NULL 연산자 사용

> ## 연결 연산자
  * ||

> ## 산술 연산자
  * \+
  * \-
  * \*
  * \/

> ## SET(집합) 연산자
  * 컬럼 수가 그 컬럼들의 데이터 타입이 같은 두 테이블의 집합 연산을 하는 연산자

### 종류
 * UNION : 합집합
 * UNION ALL : 중복된 값들을 포함한 합집합
 * INTERSECT : 교집합
 * MINUS : 차집합
```sql
SELECT deptno, empno, ename, job
FROM emp
WHERE deptno = 20
UNION
SELECT deptno, empno, ename, job
FROM emp
WHERE job = 'MANAGER';
-- deptno = 20인 emp테이블과 job이 매니저인 emp 테이블의 합집합
```

