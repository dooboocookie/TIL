# 데이터베이스(DATABASE)

>## 데이터(Data)
* datum(재료, 자료, 논거)의 복수형
* 관찰에 의한 정량적, 정성적인 실제 값
* 의미를 부여한 값

>## 데이터베이스(DataBase, DB)
* Data(자료) + Base(저장소)
* 공유되어 사용될 목적으로 통합 관리되는 "데이터의 집합"
* 효과적으로 추출, 분류, 저장, 재사용

>## DBMS(DataBase Management System, 데이터베이스 관리 시스템)
* 사용자(클라이언트)와 데이터베이스(서버)를 연결

### 오라클(ORACLE)
* 썬 마이크로시스템즈에서 개발한 관계형 데이터베이스 관리 시스템
* 리눅스와 윈도우 운영 체제에서 자유롭게 사용 가능
* 비용적인 단점으로 큰 기업에서 주로 사용
* 학습에 사용할 프로그램 : Oracle 11g XE
* 버전
  * 접미사 i, g, c
	* Oracle 9i, Oracle 10i	(internet == i)
	* Oracle 11g		(grid == g)
	* Oracle 21c		(cloud == c)
  * Edition
    * EE(엔터프라이즈 에디션) : 대규모용
    * SE(스텐다드 에디션) : 소규모용
    * SEO(SE+ONE) : SE와 거의 동일, 단일 CPU환경
    * XE(익스프레스 에디션) : 무료버전 / 기능상 제한은 없다
    * PE(퍼스널 에디션) : 개인용 == 단일 사용자만 사용가능 (EE)

> ## 데이터 모델
* 데이터 베이스 시스템에 데이터를 저장하는 방식
  * 계층형, 네트워크형 데이터 모델
    * 포인터 사용
  * 관계형 데이터 모델
    * 속성값 사용
  * 객체지향적 데이터 모델
    * 객체식별자 사용
  * 관계형 데이터 모델

> ## 관계형 데이터 모델(Relationship data model)
* 현재 가장 많이 사용되는 데이터 모델
* 핵심 구성 요소
    * 릴레이션(relation)==테이블(table)==개체(entity)
      * 데이터를 저장하는 가장 작은 단위
    * 속성(attribute)==열(column)
      * 개체의 특징, 종류, 상태
      * 개체 - 속성,속성,속성,...
    * 관계(relationship)
      * 개체와 개체 간의 관계
### RDBMS
  * 관계형 데이터베이스 관리 시스템
  * Oracle, MySQL, ...

> ## 스키마(Schema)
* DB에서 테이블들의 집합
* 인스턴스(instance) : 오라클 서버 > startup(시작) ~ shutdown(종료)
* 세션(session) : 사용자 > 로그인 ~ 로그아웃
* 스키마(schema) : 특정 사용자와 관련된 객체(테이블)의 모음

> ## DBA
* DataBase + Administrator : 데이터 베이스 관리자
* 오라클 관리자 계정
  * SYS : 최상위 관리자, 모든 권한
  * SYSTEM : DB 생성 권한 X



> ## SID
* 설치된 오라클 데이터 베이스의 고유한 이름
* 오라클 무료 버전은 자동으로 XE 1개만 설치 가능


> ## SYNONYM

* 객체를 조회할 때 사용자가 소유한 객체 아니면 객체 앞에 소유자 ID(schema)를 붙여아하는 번거로움을 줄이고자 객체의 이름을 정의
  * ex ) scott.emp >> arirang
* 종류
  * PRIVATE SYNONYM : 소유자만 접근 가능 / 잘 사용 안함
  * PUBLIC SYNONYM : 모든 사용자가 접근 가능 / PUBLIC schema의 소유

* 생성
  * CREATE PUBLIC SYNONYM [스키마명.]시노님명 FOR [스키마명.]테이블명(객체명);
  * 관리자 계정에서 SYNONYM 생성
  * 소유자 계정에서 SYNONYM에게 접근할 수 있는 권한 부여
```sql
-- 관리자 계정에서
CREATE PUBLIC SYNONYM arirang
FOR scott.emp;
```
```sql
-- 소유자 계정에서
GRANT SELECT ON emp TO PUBLIC;
```

> ## dual 테이블

* SYS 계정이 소유하는 테이블(오라클 표준 테이블)
* 오직 한 행, 한 열만 담고 있는 dummy 테이블
* 일시적인 산술 연산 및 날짜 연산시 주로 사용
* PUBLIC SYNONYM으로 설정된 이름



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
