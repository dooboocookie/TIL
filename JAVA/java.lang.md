> ## java.lang 패키지
* 가장 기본이 되는 클래스를 포함
* 컴파일 시 자동으로 import java.lang.* 문이 추가
* 따라서, import문을 따로 작성하지 않아도 java.lang 패키지의 클래스들을 사용 가능

> ## Object 클래스
* 모든 클래스에 공통으로 상속되는 상위 클래스
* 모든 클래스에 공통으로 상속하는 멤버(메소드)를 가짐

### hashcode()
* 각 객체의 주소값을 해시코드로 만들어 반환하는 메소드
```java
Test test1 = new Test();
int hashcode1 = test1.hashCode(); 

Test test2 = test1;
int hashcode2 = test2.hashCode(); // test1과 같은 hashcode
```

### toString()
* 객체의 정보를 문자열로 반환하는 메소드
* 반환 형식 : 패키지명.클래스명@16진수 해시코드
```java
Test test = new Test();
System.out.println(test.toString());
System.out.println(test); // test.toString() 같은 결과
```

### equals()
* 같은 객체인지(참조변수를 비교) 확인하여 boolean값을 반환하는 메소드
* 오버라이딩을 하지 않으면, 기본적으로 참조변수를 비교 (== 연산자와 같은 결과)
```java
Test test1 = new Test(10);
Test test2 = new Test(10);

System.out.println(test1.equals(test2)); //false

Test test2 = test1;

System.out.println(test1.equals(test2)); //true
```
* 값을 비교하는 오버라이딩
```java
class Test {
    int value;
    Test (int value) {
        this.value = value;
    }
    
    @Override
    public boolean equals (Object obj) {
        if (obj instanceof Test) {
            return this.value == ((Test)obj).value;
        } //if
        return false;
    } //equals
}//Test
```

### clone()
* 메소드를 복제하여 새 인스턴스를 만드는 메소드
* 원본 인스턴스를 보존하는 목적으로도 사용
* 공변 반환 타입 : 오버라이딩 시, 상위 클래스의 리턴 타입을 하위 클래스로 변경 허용
* 클래스에 Clonable 인터페이스를 구현해야 clone() 호출 시 예외 발생하지 않음
* clone()은 예외처리 필수
```java
class Test implements Cloneable{
    //멤버
    @Override
    public Test clone() { // 공변 반환 타입
        Object obj = null;
        try {
			obj = super.clone(); //예외 처리 필수
		} catch (CloneNotSupportedException e) {
			e.printStackTrace();
		}
        return (Test)obj;
    }
}
```
* 얕은 복제 : 객체가 참조하고 있는 객체까지 복제하지 않음
* 깊은 복제 : 객체가 참조하고 있는 객체까지 복제

### getClass()
* 객체의 클래스 정보를 갖는 Class 클래스의 인스턴스를 반환하는 메소드 (클래스명이 Class)
```java
Test test = new Test();
Class cls = test.getClass();

String info = String.format("%s@%s",cls.getName(), Integer.toHexString(test.hashCode()));

System.out.println(info);
//toString()과 같은 결과 : 패키지명.클래스명@16진수 해시코드
```

### Class 객체 얻는 방법
1. getClass() : 리턴 타입 Class 객체
2. 클래스명.class : static 필드
```java
Class cls = Test.class;
```
3. Class.forName(String fullName) : static 메소드 
    * 예외 처리 필요 
```java
try {
    Class cls = Class.forName("패키지명.Test");
} catch (ClassNotFoundException e) {
	e.printStackTrace();
}
```

> ## String 클래스
```java
public final class String
    implements java.io.Serializable, Comparable<String>, CharSequence {

    private final char value[];
    ...
```
* 변경이 불가능한 클래스
```java
String name = "두부";
name = "쿠키";
```
* char value[]는 final 멤버로 값이 변경되는 되지 않음
* 새로운 인스턴스를 생성하여 name변수에 새로운 참조변수를 가짐
  
### 문자열 리터럴

### equals() / equalsIngnoreCase()
* == 연산자는 인스턴스의 주소를 비교
* equals() 메소드로 문자열의 내용을 비교

### "" / null
* 빈 문자열
* String name = null : 참조할 인스턴스 주소가 없음
* String name = "" : 인스턴스에서 참조하는 char[]의 길이가 0

### length()
```java
String msg = "HELLO";
System.out.println(msg.length()); //5

char[] msgs = new char[5];
System.out.println(msgs.length); // 5
```
* length() : 문자열 길이를 반환하는 메소드
* length : 배열 길이를 갖는 필드

### toUpperCase() / toLowerCase()
* 대/소문자 변환하는 메소드
```java
String msg1 = "hello";
System.out.println(msg1.toUpperCase()); // "HELLO"
String msg2 = "HELLO";
System.out.println(msg2..toLowerCase()); // "hello"
System.out.println(msg1); // "hello"
System.out.println(msg2); // "HELLO"
//변경 불가능한 클래스
```

### charAt() / substring()
* charAt() : 문자열에서 한 문자를 반환하는 메소드
* substring() : 문자열 중간의 문자열을 반환하는 메소드
```java
String msg = "0123456789";
System.out.println(msg.charAt(1)); // '1'
System.out.println(msg.charAt(msg.length()-1)); // '9'
System.out.println(msg.substring(0,6)); // "012345"
System.out.println(msg.substring(7,msg.length())); // "789"
```
### split(regex) / split(regex, int limit)
* 구분자(regex)를 기준으로 문자열을 나눠 문자열 배열로 반환하는 메소드
```java
String msg = "1234-5678-1234-5678";
String[] msgs = msg.split("-");
System.out.println(Arrays.toString(msgs));
// [1234, 5678, 1234, 5678]
String[] msgs = msg.split("-" ,3);
System.out.println(Arrays.toString(msgs));
// [1234, 5678, 1234-5678]
```

### toCharArray() 메소드
* 문자열을 문자 배열로 반환하는 메소드
```java
String msg = "1234";
String[] msgs = msg.toCharArray();
System.out.println(Arrays.toString(msgs));
// [1, 2, 3, 4]
```
### replace() / repalceAll()
* replace()
  * 문자열중 해당되는 문자를 새 문자로 대체하여 문자열을 반환하는 메소드
  * 매개변수 : char old, char new / CharSequence old, CharSequence new
* repalceAll()
  * 문자열(regex)과 일치하는 내용을 대체 하여 문자열로 반환하는 메소
  * 매개변수 : String regex, String new
```java
System.out.println(msg.replace('5', '0'));
// "0123406789"
System.out.println(msg.replace("456", "000"));
// "0123000789"
System.out.println(msg.replaceAll("[2-7]", "0"));
// "0100000089"
```

### trim()
* 공백 제거 메소드

### concat(String string)
* 문자열을 연결하는 메소드
```java
String a = "123";
String b = "456";
String c = "789";

System.out.println(a.concat(b).concat(c));
//"123456789"
```
### indexOf() / lastIndexOf()
* indexOf(String string, int pos)
  * 앞에서부터 string을 pos의 위치부터 찾아서 위치 값을 반환(없으면 -1)하는 메소드
  * 매개변수에 int값이 없으면 처음부터
* lastIndexOf(String string, int pos)
  * 뒤에서부터 string을 pos의 위치부터 찾아서 위치 값을 반환(없으면 -1)하는 메소드
  * 매개변수에 int값이 없으면 마지막부터

### compareTo()
* 두 문자열을 비교하여 정수값을 반환하는 메소드
* 반환값 
  * 두 문자열을 순서대로 문자 비교 : char - char
  * 같을 떄 0이 반환
  * 'b' - 'a' = 1 / 'a' - 'b' = -1
* equals()은 boolean값 반환

### startsWith(String prefix) / endsWith(String suffix)
* 문자열이 prefix로 시작하는지 / suffix로 끝나는지 boolean으로 반환하는 메소드

### join()
* 여러 문자열을 구분자로 결합하여 문자열을 반환하는 메소드
* 매개변수 : CharSequence delimiter, CharSequence... elements
* static 메소드
* 사용빈도 높음
```java
String[] names = {"경환", "두부", "쿠키"};
System.out.println(String.join("@@", names));
//"경환@@두부@@쿠키"
```

> ## StringBuffer / StringBuilder 클래스

* String 클래스는 변경이 불가한 클래스지만, StringBuffer는 변경이 가능하여 String을 수정, 변경할 떄 많이 사용
* StringBuffer는 멀티쓰레드에 안전하도록 동기화
* StringBuilder는 쓰레드 동기화만 뺀 클래스
* String 클래스는 초기화 할 때 마다 새로운 인스턴스를 생성하기 때문에 성능이 좋지 않음

### 생성자
* StringBuffer() : 16개의 문자를 담을 수 있는 버퍼를 가진 인스턴스 생성
* StringBuffer(int i) : i개의 문자를 담을 수 있는 버퍼를 가진 인스턴스 생성
* StringBuffer(String str) : str의 길이 + 16개의 문자를 담을 수 있는 버퍼를 가진 인스턴스 생성

### append()
* 입력된 값을 StringBuffer 인스턴스의 저장하여 뒤에 붙이는 메소드 
* 매개변수 : boolean/ char/ int/ long/ float/ double/ Object/ String
* 리턴타입 : StringBuffer
```java
StringBuffer sb = new StringBuffer("두부");
sb.append('&').append("쿠키");
System.out.println(sb);
```

### indexOf()
* 입력된 문자열을 버퍼에 담긴 문자열의 위치를 찾아 정수를 반환하는 메소드
* 매개변수 : String
* 리턴타입 : int

### replace()
* 범위 내의 문자들을 입력된 문자열로 대체하는 메소드
* 매개변수 : int start, int end, String str
* 리턴타입 : StringBuffer

### delete
* 범위 내의 문자들을 제거하는 메소드
* 매개변수 : int start, int end
* 리턴타입 : StringBuffer

### capacity()
* 인스턴스의 버퍼크기를 정수로 반환하는 메소드

### toString()
* StringBuffer인스턴스를 문자열로 반환하는 메소드
* 리턴타입 : String

### reverse()
* 저장되어있는 문자들의 순서를 뒤집는 메소드
* 리턴타입 : StringBuffer

> ## Math 클래스
* 수학에 관련된 멤버를 갖고 있는 클래스
* 멤버
  * PI(3.141592...), E(2.71...) 와 같은 상수
  * 메소드는 자주 사용하므로, static 메소드로 선언  

### 메소드
* double round(double a) : 소수점 첫째자리에서 반올림하는 메소드
* double ceil(double a) : 소수점 첫째자리에서 올림하는 메소드
  * 페이징 처리 시 유용
* double floor(double a) : 소수점 첫째자리에서 내림하는 메소드
* double random() : 0 ~ 1 사이 난수 반환하는 메소드
* int abs(int a) : 절대 값을 반환하는 메소드
* double pow(double a, double b) : 제곱을 계산하는 메소드
* double sqrt(double a) : 1/2승을 계산하는 메소드
* int max(int a, int b) : 더 큰 값을 구하는 메소드
* int min(int a, int b) : 더 작은 값을 구하는 메소드


> ## 래퍼 클래스
* 8가지 기본형 변수를 객체로 다루기 위한 클래스
  * boolean > Boolean
  * byte    > Byte
  * short   > Short
  * int     > Integer
  * long    > Long
  * fload   > Float
  * double  > Double
  * char    > Character
* Number 클래스
  * 숫자 래퍼 클래스의 상위 클래스
    * Byte
    * Short
    * Integer
    * Long
    * Float
    * Double
* 추상 클래스, 추상 메소드
```java
public abstract class Number implements java.io.Serializable {
  
  public abstract int intValue();
  public abstract long longValue();
  public abstract float floatValue();
  public abstract double doubleValue();

  public byte byteValue() {
    return (byte)intValue();
  }// byteValue()

  public byte shortValue() {
    return (short)intValue();
  }// shortValue()

}// Number
```

### 문자열 변환
* xxx n = XXX.parsexxx();
  * 문자열을 해당 기본형 타입으로 반환하는 static 메소드
  * 매개변수 : String str / String str, int radix
    * 진법(radix)과 문자열(str)을 일치 안시키면, NumberFormatException 발생
  * 리턴타입 : 해당 기본형 숫자 타입

### 오토박싱(autoboxing) / 오토언박싱(autounboxing)

* 래퍼 클래스 참조 타입과 기본형 타입과의 연산을 할 때 컴파일러가 자동으로 변환
* 오토박싱 : 기본형 타입을 자동으로 래퍼 클래스 참조형 타입으로 형 변환
* 오토언박싱 : 래퍼 클래스 참조형 타입을 자동으로 기본형 타입으로 형 변환




















