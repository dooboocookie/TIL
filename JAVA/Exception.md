> ## 프로그램 오류
* 프로그램 오작동 또는 비정상적 종료
* 종류
    1. 컴파일 오류(compile-time error) 
    2. 런타임 오류(runtime error)
       1. 에러(Error) : 코드로 수습할 수 없는 심각한 오류 (ex.메모리 부족, 스택 오버 플로우,...)
       2. 예외(Exception) : 코드로 수습할 수 있는 덜 심각한 실행 오류   
    3. 논리적 에러(logical error) 

> ## 예외 클래스 상속
#### Object - Trowable (상위 클래스)
  * Exception
    * RuntimeException
      * ArithmeticException
      * NullPointerException
      * IndexOutOfBoundsException
      * ...
    * IOException
    * ClassNotFoundException
    * ...
  * Error
    * OutOfMemoryError
    * ...

1. unchecked 에외 : RuntimeException클래스와 그 하위 클래스들
    * 컴파일러가 예외처리를 확인하지 않는 클래스들
2. checked 예외 : 위를 제외한 Exception클래스와 그 하위 클래스들
    * 컴파일러가 예외처리를 확인하는 클래스들

> ## 예외처리(exception handling)
> ## try-catch 문
* 정의 : 예외가 발생할 수 있는 곳을 예측하여 코드를 작성하는 것
* 목적 : 예외가 발생하더라도 비정상적 종료를 막고 정상적으로 프로그램이 실행되도록 하기 위함
```java
try{
    //예외가 날 수 있는 코드
} catch (ArrayIndexOutOfBoundsException | ArithmeticException e) {
    System.out.println(e.getMessage());
} catch (Exception e) {
    e.printStackTrace();
}
```
* 상속 관계로 인해서 업캐스팅이 가능 (ex.Exception 타입에 ArithmeticException을 업캐스팅 가능)
* catch블럭을 다중으로 작성 시 상위 클래스의 예외를 밑에 작성
* 상위 클래스의 예외가 먼저 있으면 catch블럭이 모두 실행됨
* catch블럭에 상속관계가 없는 예외를 '|'기호를 통해 같이 사용 가능 (멀티 catch 블럭)

### finally 블럭
* try-catch문 끝에 위치
* 예외 발생 시 : try > catch > finally
* 예외 발생 안될 시 : try > finally
* try, catch 블럭에서 return값을 줘도 finally블럭은 반드시 실행
> ## throw, 예외 발생시키기
1. 예외 객체를 생성
2. throw 키워드를 통하여 예외 발생
```java
Exception e = new Exception("강제 예외");
throw e;
//throw new Exception("강제 예외");
```
> ## throws 문, 메소드 예외 선언
* 메소드 선언 시 예외가 발생할 수 있으면 throws문을 통하여 메소드가 호출되는 곳으로 예외처리를 떠넘기는 것
* 직접 예외처리를 하는 것은 아님
```java
class Test { 

    public static void main(String[] args) throws Exception {
        method1();
    }//main

    static void method1() throws Exception {
		System.out.println("method1()");
		method2();
    }//method1

    static void method2() throws Exception {
		System.out.println("method2()");
		throw new Exception(); 
	}//method2

}//Test
```
>  ## try-with-resources문, 자동 자원 반환
* I/O(입/출력)과 관련된 클래스 사용할 때 유용
* 예를 들어 Scanner 객체를 사용하고 명시적으로 닫지 않아도 자원이 자동으로 반환되는 것
```java
try (Scanner scanner = new Scanner(System.in)) {
    int i = scanner.nextInt();
} catch (InputMismatchException e) {
    e.printStackTrace();
} catch (IOException e) {
    e.printStackTrace();
}
```

> ## 새로운 예외클래스 정의
* 예외 클래스를 상속받아, 새로운 예외 클래스를 정의
* 목적 : 필요에 따라 메세지와 에러코드를 값을 멤버로 추가하여 예외 클래스를 새로 정의 / 팀 작업 시 도움
```java
public class MyException extends Exceptoin {
    private int ERROR_CODE;

    public int getERROR_CODE() { //getter
        return ERROR_CODE;
    }

    public MyException (int error_code) {
        this.ERROR_CODE = error_code;
    }

    public MyException (int error_code, String message) {
        super(message);
        this.ERROR_CODE = error_code;
    }
}
```
