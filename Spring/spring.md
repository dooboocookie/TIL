# 스프링 프레임워크
* 자바 기반의 웹 프레임워크


> ## POJO (Plain Old Java Object)
* `무거운 객체`를 만들어 코드의 가독성, 확장성, 유지보수가 떨어지는 단점을 보안하기 위해 등장한 개념
* EJB (EnterpriseJavaBeans)
  * `getter/setter`로 구성된 순수한 형태의 기본 클래스
```java
public class Score{
    private int kor;
    private int eng;
    private int mat;

    public int getKor() {return kor;}
    public void setKor(int kor) {this.kor = kor;}

    public int getEng() {return eng;}
    public void setEng(int eng) {this.eng = eng;}

    public int getMat() {return mat;}
    public void setMat(int mat) {this.mat = mat;}
}
```
* 조건
    1. 특정 규약(API)에 종속되지 않음
    2. 특정 환경에 종속되지 않음
    3. 객체 지향적 원리에 충실

> ## AOP (Apect Oriented Programming)
* 관점 지향 프로그래밍
* 모듈에서 사용하는 공통적인 기능을 분리
    1. 스프링 프레임워크 : DI, AOP
    2. 스프링 시큐리티 : 세션 (인증 권한)
    3. 스프링 배치 : 페이지 모듈화
    4. 스프링 인터그레이션 : 시스템간 연동을 위한 메시징 프레임워크
    5. 스프링 소셜 : 소셜 네트워크 연동
    6. ...
* 모듈은 상속/구현 관계 없이, 기능을 분리하여 관리하기 위함

> ## DI (DependencyInjection)
* 의존성 주입

### 강한 결합
* 객체를 다른 `객체 안`에서 생성하는 것은 강한 결합도(높은 의존성)를 가짐
* 하나의 객체의 변경 &rarr; 다른 객체의 변경

```java
public class RecordViewImpl implements RecordView{
    private RecordImpl record = new RecordImpl();
}
```


### 약한 결합
* `외부에서` 객체를 생성하여 객체를 주입
* 생성자를 통한 주입
```java
public class RecordViewImpl implements RecordView{

    private RecordImpl record;
    //[생성자 DI(의존성 주입) 방식
    public RecordViewImpl(RecordImpl record){
        super();
        this.record= record;
    }
}
```
* 프로퍼티를 통한 주입
```java
public class RecordViewImpl implements RecordView{
    //프로퍼티 방식
    public void setRecord(RecordImpl record){
        this.record = record;
    }
}
```   

> ## IoC (Inversion Of Control)
* 제어 역전
  * 스프링 프레임워크가 `개발자의 코드를 호출`

### Bean(빈) 객체
* 스프링 컨테이너가 관리하는 객체
  * 이 빈들을 관리하는 컨테이너를 `BeanFactory`라고 함

### BeanFactory
* Bean 관리(생성, 조회, 반환)

### ApplicationContext
* Bean 관리(생성, 조회, 반환)
* BeanFactory에서 부가기능을 추가
  * 국제화가 지원하는 텍스트 메시지 관리
  * 이미지 등 파일 자원을 로드할 수 있음
  * 리스너로등록된 빈에게 이벤트 발생을 알림

### 연결
```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xsi:schemaLocation="http://www.springframework.org/schema/beans
           http://www.springframework.org/schema/beans/spring-beans-3.0.xsd">

    <bean id="record" class="di.RecordImpl"></bean>

    <bean id="rvi" class="di.RecordViewImpl">
        <constructor-arg ref="record"></constructor-arg>
    </bean>

</beans>
```
* class 속성으로 풀네임을 줘 빈 객체를 id속성의 명을 가진 빈 객체를 생성
```xml
<bean id="record" class="di.RecordImpl"></bean>
```
* 생성자를 통한 주입
* 빈 객체 생성 후 constructor-arg 태그로 주입 
1. ref 속성 
```xml
<bean id="rvi" class="di.RecordViewImpl">
    <constructor-arg ref="record"></constructor-arg>
</bean> 
```
2. ref 태그 
```xml
<bean id="rvi" class="di.RecordViewImpl">
    <constructor-arg>
        <ref bean="record"/>
    </constructor-arg>
</bean>
```
* 프로퍼티를 통한 주입
  * setter 메소드명의 'set'을 생략하고 첫 글자를 소문자로 바꿈
```xml
<bean id="rvi" class="di.RecordViewImpl">
    <property name="record" ref="record"></property>
</bean>
```
### 호출
* 위에서 만든 `applicationContext.xml` xml 파일로 `GenericXmlApplicationContext` 객체 생성 하여 스프링 컨테이너 안에 Bean 객체 생성
```java
class Test {
    public static void main(String[] args) {
        String resourceLocations = "applicationContext.xml";
        
        GenericXmlApplicationContext ctx = new GenericXmlApplicationContext(resourceLocations);

        RecordViewImpl rvi = (RecordViewImpl) ctx.getBean("rvi");
    }
}
```
변경사항을 등록해보겠습니다.
