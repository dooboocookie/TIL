# 객체 지향 프로그래밍(Object Oriented Programing)

## 객체 지향 프로그래밍이란?
객체 단위로 프로그래밍 하는 기법

#### 객체 지향 언어의 장점
> 1. 새로운 코드를 작성할 때, 기존의 코드를 재사용할 수 있다.
> 2. 코드간 관계를 이용하여 유지/보수가 용이하다.
> 3. 중복된 코드를 제거하여, 실수를 줄일 수 있다.
> 4. 제어자와 메소드를 이용하여 정보를 보호 할 수 있다.


### 클래스 vs 인스턴스 vs 객체
> * 클래스 : 객체를 만들기 위한 설계도
<pre>
<code>
[접근지정자] [기타제어자] class 클래스명 [extends 수퍼클래스] [implements 인터페이스...] {
  속성
  메소드
}
public class Computer {
  public int weight;
  public int size;
  public String name;

  public void task{
  }
}
</code>
</pre>
> * 객체 : 인스턴스의 주소를 참조하는 변수 / 실제로 존재하는 사물이나 개념
> * 인스턴스 : 클래스를 인스턴스화하여 힙영역에 만든 저장공간

### 객체의 구성요소
