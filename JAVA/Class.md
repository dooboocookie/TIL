 > ## 클래스 vs 인스턴스 vs 객체
* 클래스 : 객체를 만들기 위한 설계도
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
        public void task(){
        }
    }
    </code>
    </pre>
* 객체 : 인스턴스의 주소를 참조하는 변수 / 실제로 존재하는 사물이나 개념
    <pre>
    <code>
    클래스명 객체명;
    Computer computer;
    </code>
    </pre>
* 인스턴스 : 클래스를 인스턴스화하여 힙영역에 만든 저장공간
    <pre>
    <code>
    객체명 = new 클래스명();
    computer = new Computer();
    </code>
    </pre>

> ## 객체의 구성요소
* 속성(property) : 필드(field), 상태(state), 멤버변수(member), 상태
    <pre>
    <code>
    computer.size = 13;
    computer.name = "MacBook Air"
    </code>
    </pre>
* 기능(function) : 메소드(method), 행위
    <pre>
    <code>
    computer.task();
    </code>
    </pre>

> ## 생성자(Constructor)
1. 정의 : 인스턴스 초기화 메소드
2. 호출 시기 : 인스턴스 생성 (생성자는 강제로 호출 X)
3. 리턴 값 X > 생성자 이름 앞에 void 키워드도 적지 않는다.
4. 생성자 이름 == 클래스 이름
5. 접근 지정자
     * public
     * default
     * protected
     * protected
6. 매개개변수가 없는 생성자를 디폴트 생성자(default constructor)
    (생성자를 추가하지 않는 경우, 컴파일러가 자동으로 디폴트 생성자를 추가한다.)
7. 매개변수를 달리하여 오버로딩 가능
8. 생성자는 상속되지 않는다.

> ## this(), this
1. 정의 : 클래스 자기 자신의 주소 값을 갖는 참조변수
2. 용도
    * 클래스 자기 자신의 멤버를 가리킬 때
    * 생성자에서 또 다른 생성자를 호출할 때
    * 단독으로 사용 - 리턴 값, 매개변수

> ## static
1. 제어자(modifier)
2. 용도
   * 클래스 : public static class Test{}
   * 정적 변수(클래스 변수) : public static int x;
     * 공유 변수라고도 불리며 인스턴스 선언 시 각각 부여 X
     * 인스턴스 선언 전에도 클래스명.필드명으로 사용
     * 프로그램 시작 시 메모리에 잡힘, 종료 시 제거
   * 정적 메소드 : public static void disp() {}
     * static 제어자를 설정하지 않으면, 인스턴스 선언 후 메소드 호출
   * 클래스 초기화 블럭 : static {}
  

> ## 초기화 블럭(Initialization Block)
   * 클래스 초기화 블럭 : 클래스 변수 초기화
   * 인스턴스 초기화 블럭 : 인스턴스 변수 초기화

> ## 멤버 변수의 초기화
   1. 명시적 초기화
   2. 클래스 초기화 블럭
   3. 인스턴스 초기화 블럭
   4. 생성자

> ## 클래스간 관계 : has-a (포함관계)
* 클래스 안에 멤버 변수로서 다른 클래스 타입의 참조변수를 선언
    <pre>
    <code>
    class Car {
        Engine engine; // 멤버 변수 선언, 기본 값은 null
    }
    </code>
    </pre>
* 참조변수 초기화 방법
  * 명시적 초기화 : 결합력이 높다는 단점이 있다.
    <pre>
    <code>
    class Car {
        Engine engine = new Engine();
    }
    </code>
    </pre>
  * 생성자를 통한 의존성 주입(DI,Dependency Injection)
    <pre>
    <code>
    class Car {
        Engine engine;
        // 디폴트 생성자
        Car() {
            this.engine = new Engine();
        }
        // 생성자
        Car(Engine engine) {
            this.engine = engine;
        }
    }
    </code>
    </pre>
  * setter를 통한 의존성 주입
    <pre>
    <code>
    class Car {
        private Engine engine; //null;
        public void setEngine(Engine engine) {
        this.engine = engine;
    }
    }
    </code>
    </pre>
  
> ## 클래스간 관계 : is-a (상속관계)
> ## 상속 (Inheritance)
1. 정의 : 기존 클래스를 재사용하여 새로운 클래스를 작성
2. 장점 : 코드의 재사용, 중복된 코드 제거 > 생산성과 유지보수 향상
3. 선언 : extends 키워드
        <pre>
        <code>
        class 클래스명 extends Super클래스 {}
        </code>
        </pre>
4. 상위(super)클래스 : 부모(parent)클래스, 기반(base)클래스<br>
   하위(sub)클래스 : 자식(child)클래스, 파생된(derived)클래스
5. 생성자, 초기화 블럭은 상속되지 않음
6. JAVA에서 단일 상속만 가능 / 다중 상속은 불가<br>
   다른 클래스로 상속받은 멤버의 이름이 같은 경우 구분이 어렵다는 단점
7. Object 클래스 : 모든 클래스의 조상<br>
    * 모든 클래스는 컴파일 시 자동으로 extends java.lang.Object로 Object클래스를 상속

> ## 오버라이딩 (Overriding)
1. 정의 : 부모 클래스에서 상속 받은 메소드를 재정의 하는 것
2. 선언 : @ 어노테이션(Annotation)
    <pre>
    <code>
    @Override
    public void test() {
        super.test();
        System.out.println("오버라이딩");
    }
    </code>
    </pre>
3. 조건
   * 같은 이름의 메소드
   * 같은 타입의 매개변수
   * 같은 리턴타입 (공동 반환 타입 : 오버라이딩 시, 상위 클래스의 리턴 타입을 하위 클래스로 변경 허용)
4. 제한
    * 부모 클래스의 메소드보다 접근제어자를 더 좁은 범위로 할 수 없다.
    * 부모 클래스의 메소드보다 예외를 많이 선언할 수 없다.
    * 인스턴스 메소드 -> 정적 메소드로 변경 불가 / 반대도 불가
5. 오버로딩(Overloading)과의 차이
   * 오버로딩은 매개변수와 리턴자료형을 달리하여 이름만 같은 메소드를 정의
   * 오버라이딩은 상속받은 클래스의 메소드를 내용을 재정의(수정)

> ## super(), super
1. super : 상속받은 부모 클래스를 가리키는 참조 변수
2. super() : 부모 생성자를 호출할 때 사용
    * 부모 생성자 > 자식 생성자 순으로 호출
    * Object클래스를 제외한 모든 클래스의 생성자 첫 줄에는 this(), super()가 호출되며, 컴파일러가 자동으로 super();를 추가

> ## final
1. final 클래스 선언 : subclass를 가질 수 없는 최종 클래스
2. final 변수 선언 : 상수
3. final 메소드 선언 : subclass에서 오버라이딩할 수 없다.

> ## 패키지 (package)
1. 정의 : 서로 관련된 클래스, 인터페이스 묶음
2. 목적 : 클래스, 인터페이스를 효율적으로 유지 및 보수
3. 선언위치 : 공백, 주석을 제외한 제일 첫 줄
4. 패키지명 : 소문자 사용을 권장 / 대문자는 클래스에 사용
5. 참고
    * 풀네임이란? java.util.Date와 같이 패키지명.패키지명..클래스명
    * 패키지는 물리적으로 하나의 디렉토리(폴더)를 의미
    * 모든 클래스는 반드시 하나의 패키지에 포함됨

> ## import 문
1. 역할 : 컴파일 시 import문을 통해 클래스들 앞에 패키지명을 붙임
2. 목적 : 다른 패키지의 클래스를 접근할 때 풀네임을 사용하는 것을 생략하기 위해 사용
3. 선언위치 : 패키지 선언부와 클래스 선언부 사이
4. import java.lang.*; 은 컴파일 시 자동으로 추가
5. '*'는 해당 패키지의 모든 클래스 포함, 하위 패키지 포함 X
    * 사용하지 않는 메소드도 포함시키기 때문에, 사용 시 주의

### static import 문
* static 멤버를 호출할 때 클래스 이름을 생략한다.
<pre>
<code>
package pack;
import static java.lang.Math.random;
public class Test {
	public static void main(String[] args) {
        System.out.println(random());
    }
}
</code>
</pre>

> ## 업캐스팅 / 다운캐스팅
* 업캐스팅
    * 정의 : 자식 클래스의 인스턴스를 부모 클래스 타입으로 참조
    * 형식 : 자동 형변환
* 다운캐스팅 
    * 정의 : 부모 클래스의 인스턴스를 자식 클래스 타입으로 참조
    * 형식 : 캐스트 연산자
    * 업캐스팅이 된 후에 다운캐스팅이 가능
* 오버라이딩된 함수가 호출됨

> ## 다형성
* 한 타입의 참조변수로 여러 타입의 객체를 참조
* 조상 클래스 타입의 참조변수로 자손클래스의 인스턴스를 참조
<pre>
<code>
Car car = new Engine(); // 업캐스팅
Engine engine = new Engine();
</code>
</pre>
* 같은 타입의 인스턴스 / 다른 타입의 참조변수
  * 사용할 수 있는 멤버의 개수가 달라진다.
  * 인스턴스 타입의 클래스에서 오버라이딩된 메소드가 호출됨
* 관련 : 업캐스팅 / 다운캐스팅, 오버라이딩 / 오버로딩
### 매개변수의 다형성
<pre>
<code>
public static void main(String[] args) {
    dispInfo(new B()); // A obj = new B() (자동 업캐스팅)
    dispInfo(new C()); // A obj = new C() (자동 업캐스팅)
    dispInfo(new D()); // A obj = new D() (자동 업캐스팅)
}
private static void dispInfo(A obj) {
    if (obj instanceof D) {
        D d = (D)obj; //다운캐스팅
        //코딩처리
    } else if (obj instanceof C) {
        C c = (C)obj; // 다운캐스팅
        //코딩처리
    } else if (obj instanceof B) {
        B b = (B)obj; //다운캐스팅
        //코딩처리
    }
}
</code>
</pre>
* 매개변수에 공통 조상 클래스를 지정하면 자식 클래스들로 메소드 호출 가능하여 다형성 
* 주의. 자식 클래스 먼저 물어 else if 문 빠져나와야 함
* instanceof 연산자 : 객체 instanceof 클래스타입 == boolean형

> ## 추상화
### abstract 키워드
* 추상의, 미완성의
* 대상 : 클래스, 메소드
  
### 추상 메소드
* 정의 : 몸체({},기능)이 구현이 안된 불완전한 메소드
* abstract 키워드를 붙임
* 목적 : 상속 받을 자식 클래스에서 오버라이딩하도록 강요

### 추상 클래스
* 추상 메소드를 1개 이상 멤버로 하는 클래스는 추상 클래스가 됨
* abstract 키워드를 붙임
* 추상 클래스는 인스턴스 생성 불가
<pre>
<code>
public abstract class Abs{
    public abstract void test();
}
</code>
</pre>

### 추상화
  * 클래스의 멤버의 중복을 찾아 공통의 상위 클래스를 만드는 것
  * 구체화 : 기능을 구체화하여 상속하는 것

> ## Singleton(싱글톤)
* 의도 : 객체를 1개만 생성
1. 생성자의 접근지정자를 private으로 지정
2. 인스턴스를 생성 못하게 함
3. 클래스 내에서 자기 자신의 인스턴스를 참조하는 static 참조변수를 선언
4. getInstance() 정적 메소드 선언하여 해당 메소드를 통하여 단 하나의 객체만 선언할 수 있게 함
<pre>
<code>
public class Singleton {
	private static Singleton singleton;
	private Singleton() {		
	}
	public static Singleton getInstance() {
		if(singleton == null) {
			singleton = new Singleton();
		}
		return singleton;
	}
}
</code>
</pre>

> ## 제어자(Modifier)
### 멤버의 접근제어자 (필드, 메소드, 생성자)
1. public : 패키지 내/외부 어디서나 접근(참조) 가능	
2. protected : 패키지 내부 접근(참조) 가능 + 상속 관계 있는 자식 클래스 접근(참조) 가능
3. default : 패키지 내부 접근(참조) 가능
4. private : 클래스 내부 접근(참조) 가능
* 범위 순<br>
    public > protected > default > private

### 제어자의 조합
* 메소드 : abstract - static : 사용 불가
  * static은 {}이 있는 메소드만 사용 가능
* 클래스 : abstract - fianl : 사용 불가
  * 추상메소드는 상속을 통해 확장해야 되는데, final은 확장이 불가
* 메소드 : abstract - private : 사용 불가
  * 추상메소드는 상속을 통해 확장해야 되는데, private이면 자손 클래스에서 접근 불가
* 메소드 : private - final : 불필요
  * 둘 다 오버라이딩이 불가능하다는 의미

> ## 인터페이스
* 참조타입의 자료형
* 상수, 추상 메소드'만'을 멤버로 갖음 (일종의 추상 클래스)
* 목적 : 클래스를 선언할 떄 도움
* 선언 형식
<pre>
<code>
[접근제어자] interface 인터페이스명 {
    //상수 선언 (final) //public static final 생략 가능
    //추상메소드 선언 (abstract) //public abstract 생략 가능
}
</code>
</pre>
* JDK 1.8 부터
  * static 메소드 선언 가능
  * default 메소드 선언 가능
### 인터페이스의 상속
* 상속 가능
* 중복 상속 가능
  * 중복되는 추상 메소드가 있어도 하나만 오버라이딩
* extends IA, IB 의 형식
* 클래스의 Object같이 공통 조상은 없다.

### 인터페이스의 구현
<pre>
<code>
class 클래스명 implements 인터페이스명,... {
    //인터페이스 내의 추상 메소드를 구현하는 오버라이딩
}
</code>
</pre>

### 인터페이스의 다형성
* 인터페이스는 그 인터페이스를 구현한 클래스의 조상
* 인터페이스를 구현한 클래스의 인스턴스를 인터페이스 타입으로 참조 가능

### 사용 이유
1. 개발시간 단축
2. 표준화 가능
3. 관계가 없는 클래스들을 관계를 맺어 줌
4. 독립적인 프로그래밍
