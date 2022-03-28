# 제네릭스(Generics)
* JDK1.5~
* compile-time type check : 컴파일 시 컬렉션 클래스나 메소드에 객체 타입을 체크
  * 객체 타입의 안정성 향상
  * 형변환 과정 줄임

  



> ## 제네릭 클래스 선언

### 템플릿 클래스
* 여러 타입을 다룰 수 있는 클래스
* 타입을 최상위 객체인 Object 타입으로 하여 여러 타입의 객체를 사용할 수 있게 함
```java
class Box1{
    double value;
    
    void setValue(double value){
        this.value = value;
    }
    double getValue() {
        return this.value;
    }
}

class Box2{
    int value;
    //...
}

class Box3{
    boolean value;
    //...
}

//...
```

```java
class Box{
    // Integer, Double, Boolean, ...  다양한 타입의 객체 가능
    Object value;
    
    void setValue(Object value){
        this.value = value;
    }
    Object getValue() {
        return this.value;
    }
}
```
* 객체 사용 시, 형변환 과정이 필요
* 여러 타입을 사용할 때에 안정성 떨어짐

### 제네릭 클래스
* 인스턴스 생성 시 임의의 참조형 타입을 지정하여 사용 가능한 클래스
* \<T>, \<E>, \<K, V>, ... 타입 변수(type variable)
    * 모든 참조형 타입으로 생성 가능
    * 기본형 타입은 사용이 불가 > 참조형 타입만 사용 가능 (래퍼 클래스, ...)


```java
class Box<T>{
    // Integer, Double, Boolean, ...  다양한 타입의 객체 가능
    T value;
    
    void setValue(T value){
        this.value = value;
    }
    T getValue() {
        return this.value;
    }
}
```
### 타입 제한
* \<T extends A> : A의 하위 클래스만 사용 가능

### static 멤버(필드, 메소드) X
* 'T'는 인스턴스 멤버로 간주
* Box 인스턴스를 생성 안하면, T의 타입 또한 정해지지 않음
    * Box\<A>.value와 Box\<B>.value가 다를 수 없음

### 제네릭 클래스 내, T 타입의 참조 변수
* 제네릭 타입을 배열 같은 참조 변수로 '선언' 가능
* 하지만, 제네릭 new 연산자를 통해 생성하는 것은 불가
  * new 연산자는 컴파일 시 T가 어떠한 타입인지 명확해야 함

> ## 제네릭 클래스 인스턴스 생성
```java
class Box1<T>  {}
class Box2<T> extends Box1 {}

class A {}
class B extends A {}

class Example {
    public static void main (String[] args) {
        // 기본 생성 형식
        Box1<A> obj1 = new Box1<A>();
        // 생성자 부분 타입이 추정이 가능하면 생략 가능 (JDK1.7~)
        Box1<B> obj2 = new Box1<>();
        //(==)Box1<B> obj2 = new Box1<B>();

        //제네릭 클래스 간 업캐스팅 (다형성)
        Box1<A> obj3 = new Box2<A>();

        //제네릭 타입 간 업캐스팅 불가, 제네릭 타입은 일치해야 됨
        Box1<A> obj4 = new Box1<B>(); // >Error
    }
}
```


> ## '?' 와일드 카드
 
* \<?> : 모든 클래스 타입 가능 (=)
* \<? extemds T> : T의 하위 클래스 타입만 사용 가능, 상한 지정
* \<? super T> : T의 상위 클래스 타입만 사용 가능, 하한 지정


> ## 제네릭 메소드
* 메소드 선언 시 제네릭 타입과 함께 선언하는 메소드
 
### 선언부
* 리턴자료형 앞에 선언
* [접근지정자] [기타제어자] <T> 리턴자료형 메소드(매개변수...) {[return 리턴 값;]}
```java
static <T extends A> test(ArrayList<T> list){
    //...
}
```
* 제네릭 클래스 내부에서는 static 메소드는 사용이 불가하지만,
* 제네릭 타입을 선언하면 static 메소드로 선언 가능


### 호출부
```java
<A>test(list);
```
