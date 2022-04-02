# I/O (입출력, Input/Output)
## Stream (스트림)
* 입력 : 키보드나 파일 같은 대상에서 데이터를 받는 것, 읽기
* 출력 : 모니터나 프린터 따위에 데이터를 출력하는 것, 쓰기
* 스트림
  * 자바에서 데이터 입출력은 스트림을 통해서 이루어짐
  * 데이터를 운반하는데 사용되는 연결통로
  * 단방향 
  * 연속적, FIFO(Fist In First Out)
---
## InputStream / OutputStream (바이트 스트림)
* 1byte(8bits)를 단위로 데이터를 전송하는 입출력 스트림
* 입력 스트림 : InputStream의 자식 클래스
  * int read() : 0~255, -1(없을 때) 입력된 바이트를 정수로 반환
  * int read(byte[] b, int off, int len) : len개의 바이트를 배열b에 off부터 저장하는 메소드

* 출력 스트림 : OutputStream의 자식 클래스
  * void write(int b) : 정수를 입력받아 바이트로 전송
  * void write(byte[] b, int off, int len) : 배열 b의 off부터 len만큼의 데이터를 읽어서 출력하는 메소드
  * void flush() : 스트림 버퍼의 내용을 출력하는 메소드
  * void close() : 스트림 버퍼의 내용을 출력 후 입력소스를 닫음
  

> ## ByteArrayInputStream / ByteArrayOutputStream
* byte 배열에 데이터를 입출력하는 스트림

### 생성자
* ByteArrayInputStream(byte[] buf, int pos, int len) : 바이트 배열을 입력받는 스트림 생성
* ByteArrayOutputStream(int size) : size만큼의 버퍼 용량을 가진 바이트 배열 출력 스트림 / 입력 안하면 32바이트

> ## FileInputStream / FileOutputStream
* 파일을 바이트 단위로 입출력하는 스트림
* 실행파일, 이미지파일,텍스트파일,... 입출력 하는데 사용

### 생성자
* FileInputStream(String name) : 입력된 파일 경로에 해당되는 파일에서 입력받는 스트림 생성
* FileInputStream(File file) : 파일 객체에 해당되는 파일에서 입력받는 스트림 생성
* FileOutputStream(String name, boolean append) : 파일 경로에 해당되는 파일에 출력하는 스트림 생성, 불리언 값을 tre로 주면 기존 파일에 데이터를 이어 붙임

> ## BufferedInputStream / BufferedOutputStream
* 바이트 배열인 버퍼를 사용
* 한 번에 여러 바이트를 입출력하여 효율 높이는 보조스트림


> ## DataInputStream / DatataOutputStream
* 기본형 자료형에 맞는 바이트 단위로 입출력할 수 있게하는 보조스트림

> ## SequenceInputStream
* 여러개의 스트림을 한개의 스트림으로 합쳐주는 보조스트림
* SequnceInputStream(Enumreation e) : 열거형 e에 저장된 값들을 이은 하나의 스트림을 저장하는 인스턴스 생성
* SequnceInputStream(InputSteream s1, InputStream s2) : s1, s2의 입력스트림을 하나의 스트림으로 저장하는 인스턴스 생성


> ## PrintStream
* print() / println() / printf()같은 메소드를 오버로딩하여 제공
* System.out은 PrintStream

---
## Reader / Writer (문자 스트림)
* 바이트가 아닌 문자를 기반으로 데이터를 입출력하는 스트림
* 입력 스트림 : Reader의 자식 클래스
  * int read() : char 유니코드 0~65535정수를 반환, 없을 떄 -1
  * int read(char[] c) : c의 크기만큼 읽어서 c의 문자를 저장하는 메소드, 반환 값은 데이터의 개수(없으면 -1)
* 출력 스트림 : Writer의 자식 클래스
  * void write(int b) : 정수를 입력받아 전송
  * void write(String) : 문자열을 입력받아 전송
  * void flush() : 스트림 버퍼의 내용을 출력하는 메소드
  * void close() : 스트림 버퍼의 내용을 출력 후 입력소스를 닫음

* 대부분 문자 스트림과 바이트 스트림이 유사
 
> ## InputStreamReader / OutputStreamWriter
* 바이트 스트림을 문자 스트림으로 변환하는 문자기반 보조 스트림
* InputStreamReader(InputStream in) : 바이트 입력 스트림을 문자로 변환하여 문자 입력 스트림 생성
* OuputStreamWriter(OutputStream out) : 바이트 출력 스트림을 문자로 변환하여 문자 출력 스트림 생성


---
> ## 표준 입출력

### System.in
* InputStream
* 콘솔로부터 데이터를 입력받음
* 표준 입력 장치 : 키보드, ...

### System.out / System.err
* PrintStream
* 콘솔로 데이터를 출력
* 표준 출력 장치 : 모니터, 프린터, ...


> ## File 클래스

* 파일이나 디렉토리를 다룰 수 있게하는 클래스

### 생성자
* File(String fileName)
  * 경로를 포함한 파일이름(디렉토리)을 통하여 해당 파일에 대한 인스턴스 생성 / 경로를 적지 않고 파일이름만 적을 시, 파일 경로는 프로그램이 실행되는 위치로 간주

> ## 직렬화 (Serialization)
* 직렬화 : 객체 -> 스트림
  * 객체 단위로 입출력을 하기 위함
* 역직렬화 : 스트림 -> 객체
  * 스트림을 다시 객체로 변환하여 객체를 사용하기 위함
  
### ObjectInputStream
* 역직렬화
* 스트림을 객체로 변환하기 위함 클래스
* Object readObject() : 스트림에 저장된 내용을 객체로 반환하는 메소드

### ObjectOutputStream
* 직력화
* 객체를 스트림으로 변환하기 위한 클래스 
* void writeObject(Object obj) : 객체정보를 스트림에 저장하는 메소드

### Serializable 인터페이스
* 빈 인터페이스
* 직렬화가 가능하게 설계된 클래스인지를 판다하는 목적
* 직렬화 가능 클래스를 상속받은 클래스도 직렬화 가능
