# Spring Framework

> ## 좋은 객체 지향 설계

### 객체 지향 프로그래밍

* 속성과 행위가 정의된 `객체`들의 모임을 파악
* 각각의 객체는 메시지를 주고 받고, 데이터를 처리(협력)
* 유연하고 변경에 용이
* 객체 지향 프로그램의 특징
  * 캡슐화
  * 상속성
  * 추상화
  * `다형성`

### 역할과 구현을 분리

* `역할과 구현`으로 구분하면 단순, 유연해짐 
  * ex.연극에서 배역에 따라 배우가 달라질 수 있는 것
* `인터페이스`
  * 역할
  * 클라이언트는 역할(인터페이스)만 알고, 내부구조(구현체)에 의존적이지 않아야 함
* `구현체`
  * 인터페이스를 구현한 클래스

### 다형성

* 클라이언트는 인터페이스에 의존하고, 실행 시점에서 유연하게 변경 가능해야 함
* 클라이언트를 변경하지 않고, 서버의 구현 기능을 유연하게 변경할 수 있어야함

### SOLID 5가지 원칙

1. SRP(Single Responsibility Principle)
   * 단일 책임 원칙
   * 한 클래스는 하나의 책임을 가져야 함
     * `변경`에 대한 파급 효과가 적어야 함

2. `OCP(Open/Closed Principle)`
   * 개방 폐쇄 원칙
   * 확장에는 열려 있고, 변경에는 닫혀 있어야 함
     * 인터페이스(역할)를 구현한 기능을 구현체를 통하여 확장
     * 클라이언트는 인터페이스를 의존하여 변경을 하지 않아야 함

3. LSP(Liskov Substitution Principle)

    * 리스코프 치환 원칙
    * 객체는 정확성을 깨뜨리지 않으면서 하위 객체로 바꿀 수 있어야 함
      * 컴파일 영역의 문제가 아님
      * ex. 자동차에서 엑셀은 앞으로 가는 기능 &rarr; 이 기능이 깨지면 안됨

4. ISP(Interface Segregation Principle)
    * 인터페이스 분리 원칙
      * 하나의 범용 인터페이스 X &rarr; 특정 클라이언트를 위한 인터페이스 여러개

5. `DIP(Dependency Inversion Principle)`
    * 구체화에 의존 X &rarr; 추상화(인터페이스, 역할)에 의존 O
    * 이 원칙을 따라야, `변경에 유연`한 프로그래밍을 할 수 있음

#### 다형성을 통한 주입

1. MemberRepository 인터페이스를 구현한 두 클래스

```java
interface MemberRepository {}

class MemoryMemberRepository implements MemberRepository {}

class JpaMemberRepository implements MemberRepository {}
```

2. `다형성`을 이용, MemoryMembeRepository를 MemberRepository 타입에 초기화

```java
class MemberSerivce() {
    MemberReository memberRepository = new MemoryMemberRepository();
}
```
3. JpaMemberRepository로 대체
```java
class MemberSerivce() {
    MemberReository memberRepository = new JpaMemberRepository();
}
```
* 클라이언트 코드가 역할(MemberRepository)와 구현(MemoryMemberRepository) 둘 다 의존함
* DIP, OCP를 지키지 못함
  * 스프링의 DI 컨테이너를 통하여 의존관계 주입을 하여 해결


> ## 스프링 컨테이너, 스프링 빈

### 스프링 팩토리를 이용한 빈 객체 생성

### DI

### IoC

> ## 싱글톤



> ## 컴포넌트 스캔과 의존관계 자동 주입


> ## 빈 생명주기, 빈 스코프
