# 열거형(enums)

* 상관된 상수들을 열거하여, 편리하게 선언 및 사용하기 위한 자료형
* JDK1.5~
* 열거형의 상위 클래스 : java.lang.Enum 클래스
* 상수를 나타내는 표현이 표준화되어 팀작업에 용이(ex. 성별, 동서남북, ...)

> ## 열거형 선언
```java
enum Card {CLOVER, HEART, DIAMOND, SPADE}
```
enum 열거형명 {상수명, 상수명, 상수명, 상수명, ...}

> ## 열거형 사용
* 코드에서 의미하는 바가 명확히 보여, 가독성이 좋음
```java
Card card = Card.CLOVER;

switch (card) {
    case CLOVER:break;
    case HEART:break;
    case DIAMOND:break;
    case SPADE:break;
}
```
### ordinal()
* 열거형 상수의 순서를 반환하는 메소드
* 매개변수 : X
* 리턴타입 : int (0번부터 몇 번째 상수인지 반환)

### toString() 
* 열거형 상수의 이름을 반환
* 매개변수 : X
* 리턴타입 : String (name()도 같은 리턴값을 가짐)
