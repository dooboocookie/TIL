# 쓰레드(Thread)
> ## 프로세스(Process)
* OS(운영체제)로 프로그램을 실행하는데, 필요한 자원(데이터, 메모리, ...)을 할당 받음
* 자원을 이용하여 쓰레드들이 작업을 수행
* 필수적으로 1개의 'main 쓰레드'가 존재
* multi-threaded process : 2개 이상 쓰레드를 가진 프로세스
  * = 자원 + 쓰레드 + 쓰레드 + 쓰레드 + ...
  
> ## 쓰레드(Thread)
* 프로세스 내에서 독립적으로 실행되는 메소드(기능, 작업)
* 최소 1개 쓰레드 필요 : main 쓰레드

> ## 멀티 태스킹, 다중 작업

* 여러 개의 프로세스를 동시에 실행
* CPU 코어 1개가 1개의 작업을 수행
* 시분할을 통해 짧은 시간동안 여러 작업을 번갈아가며 수행
* OS가 관리하는 영역

>## 멀티 쓰레드
* 멀티 쓰레드로 프로그램을 작성하여, 동시에 여러 작업을 할 수 있게 함
* 장점
  * CPU의 '사용률'을 향상
  * 자원을 효율적으로 사용
  * 사용자에 대한 응답성으 향상
  * 작업이 분리되어 코드가 간결

> ## 쓰레드의 구현

### Thread 클래스 상속
```java
class WorkerThread extends Thread{
    @Override
    public void run(){
        // Worker 쓰레드가 작업할 내용
    }
}
```
### Runnable 인터페이스 구현
```java
class WorkerRunnable implements Runnable{
    @Override
    public void run(){
        // Worker 쓰레드가 작업할 내용
    }
}
```
* Thread 클래스를 상속 받으면 다른 클래스를 상속받지 못하니, Runnable 인터페이스를 구현하는 것이 일반적

> ## 인스턴스 생성
### Thread 클래스 상속
```java
Thread t1 = new WorkerThread();
```
### Runnable 인터페이스 구현
```java
Runnable r = new WorkerRunnable();
Thread t2 = new Thread(r);
```
### main 쓰레드 
```java
public static void main(String[] args){
    Thread t3 = Thread.currentThread(); //현재 실행중인 쓰레드를 반환
    System.out.println(t3.getName()); //main
}
```

> ## 쓰레드의 실행
### mian 쓰레드
* main 메소드의 작업을 수행
* main 메소드를 호출하고, main 메소드가 닫히는 지점에서 쓰레드의 작업이 종료

### run()
* Thread 클래스, Runnable 인터페이스의 run() 메소드를 오버라이딩
* run() 메소드는 해당 쓰레드가 작업할 내용을 갖음

### start()
* 쓰레드를 실행시킬 때 사용하는 메소드
* 호출 스택(Call Stack) : 모든 쓰레드는 독립적인 작업을 수행 > 각자의 호출 스택이 필요

  1. main메소드에서 새로운 쓰레드의 start()메소드 호출 > main메소드의 호출 스택 최상위에 start()메소드 호출
  2. start()가 그 쓰레드가 작업할 호출 스택을 생성
  3. 그 호출 스택에 run() 메소드가 호출되어  독립된 공간에서 run()안에 작업을 수행(혹은 할 예정)
  4. 두 호출 스택을 '정해진 순서에 의해' 번갈아 가며 쓰레드들이 실행 (실행 순서는 OS관할)

* 실행 중인 사용자 쓰레드가 없으면 프로그램은 종료된다

> ## 우선순위
* priority(우선순위)
  * 쓰레드의 멤버 변수
  * 우선순위를 통해 우선순위가 더 높은 쓰레드가 많은 작업시간을 갖을 수 있도록 함 
### setPriority()
* 해당 쓰레드의 우선순위를 지정한 정수값으로 변환하는 메소드
* 매개변수 : int newPriority (1~10)
* 리턴타입 : void
* mian 쓰레드의 우선순위 값 == 5 > main 메소드 안에서 생성되는 쓰레드는 기본 값이 5
```java
Thread t1 = new WorkerThread();
Thread t2 = new WorkerThread();

t1.setPriority(3)
t2.setPriority(7)

t1.start();
t2.start();
// t1보다 t2의 우선순위가 높아지게 됨
```

> ## 쓰레드의 상태 (실행 상태)
* NEW : 생성
  * 쓰레드가 생성만 된 상태
* RUNNABLE : 실행대기 + 실행
  * start() 메소드가 호출되어, 실행 중 or 실행 가능한 상태 (호출 스택이 생성된 상태?)
* TERMINATED : 소멸
  * 쓰레드가 작업을 종료한 상태 
* TIMED_WAITING : 일시정지
  * sleep()메소드에 의해서 지정된 시간동안 일시정지된 상태
  * 시간이 지나면 자동으로 실행대기 상태로 넘어감
* WAITING : 일시정지
  * Object.wait()메소드로 일시정지한 상태
  * Object.notify()메소드로 실행대기 상태로 바꿈
* BLOCKED : 일시정지
  * 동기화 블럭에 의해서 wkala(lock) 상태


> ## 실행제어

### sleep()
* 쓰레드를 지정된 시간동안 일시정지 상태가 되는 메소드
* 지정된 시간이 지나면 자동으로 실행대기 상태가 됨
* 매개변수 : long millis / long millis, int nanos
* 리턴타입 : void

### interrupt()
* 쓰레드의 interrupted 멤버 변수를 false에서 true로 변경
* sleep()으로 일시정지된 쓰레드에 interrupt()를 호출 시
  * InterruptedException 발생
  * 쓰레드가 실행대기 상태로 됨
  * Interruped 멤버 변수는 false로 자동 초기화
* 매개변수 : X
* 리턴타입 : void

### isInterrupted()
* 쓰레드의 interrupted 멤버 변수를 반환
* 매개변수 : X
* 리턴타입 : boolean(interrupted)















































