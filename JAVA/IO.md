# I/O (입출력, Input/Output)
> ## Stream (스트림)
* 입력 : 키보드나 파일 같은 대상에서 데이터를 받는 것, 읽기
* 출력 : 모니터나 프린터 따위에 데이터를 출력하는 것, 쓰기
* 스트림
  * 자바에서 데이터 입출력은 스트림을 통해서 이루어짐
  * 데이터를 운반하는데 사용되는 연결통로
  * 단방향 
  * 연속적, FIFO(Fist In First Out)
---
> ## InputStream / OutputStream (바이트 스트림)
* 1byte(8bits)를 단위로 데이터를 전송하는 입출력 스트림
* 입력 스트림 : InputStream의 자식 클래스
  * int read() : 0~255, -1(없을 때) 입력된 바이트를 정수로 반환
  * int read(byte[] b, int off, int len) : len개의 바이트를 배열b에 off부터 저장하는 메소드

* 출력 스트림 : OutputStream의 자식 클래스
  * void read(int b) : 정수를 입력받아 바이트로 전송
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

> ## PrintStream


---
> ## Reader / Writer (문자 스트림)

---
> ## File
