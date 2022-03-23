# Collections Framework (컬렉션 프레임워크, JCF)
* 데이터의 집합을 관리하는 클래스들을 표준화 설계

> ## 인터페이스 

### List
* Collection 인터페이스의 하위 인터페이스
* 순서 유지 / 중복 허용 (ex. 대기자 명단)
* 구현 클래스
   * ArrayList
   * Vector
   * LinkedList
   * Stack
   * ...

### Set
* Collection 인터페이스의 하위 인터페이스
* 순서 유지 X / 중복 허용 X (ex. 정수 집합)
* 구현 클래스
  * HashSet
  * SortedSet
  * TreeSet
  * ...

### Map
* key + value (=entry)의 쌍으로 있는 데이터
* key 중복 허용 X / value 중복 허용 O
* 구현 클래스
  * HashTable
  * HashMap
  * SortedMap
  * TreeMap
  * TreeMap
  * LinkedHashMap
  * Properties
  * ...

> ## ArrayList 컬렉션 클래스

* Object 배열로 데이터를 관리하는 클래스
* List 인터페이스를 구현한 클래스
* 순서유지, 중복허용
* 공간이 없으면 클래스가 용량을 늘림

### 생성자
* ArrayList() : 디폴트 생성자,  용량(capacity)이 10개, 객체를 10개 담을 수 있는 인스턴스 생성
* ArrayList(int i) : 초기 용량을 설정하여 인스턴스 생성
* ArrayList(Collection c) : 콜렉션 객체를 갖는 인스턴스를 생성
```java
ArrayList list1 = new ArrayList(); // 용량 10

ArrayList list2 = new ArrayList(3); // 용량 3

int[] nums = {1,2,3,4,5};
List numlist = Arrays.asList(numlist);
ArrayList list3 = new ArrayList(numlist);
//[1,2,3,4,5]
```

### get()
* 인덱스에 해당되는 요소 객체를 반환하는 메소드
* 매개변수 : int index
* 리턴타입 : Object

### add()
* 지정된 인덱스 위치나 마지막 위치에 요소 객체를 추가하는 메소드
* 매개변수 : Object obj / int index, Object obj
* 리턴타입 : boolean / void

### set()
* 지정된 인덱스 위치에 요소에 해당 객체를 할당하는 메소드
* 매개변수 : int index, Object obj
* 리턴타입 : E

### 검색
* indexOf()
  * 요소들 중에 일치하는 객체를 찾아 위치를 반환하는 메소드
  * 매개변수 : Object obj
  * 리턴타입 : int (index or -1)
* contains()
  * 요소들 중에 일치하는 객체를 찾아 true/false를 반환하는 메소드
  * 매개변수 : Object obj
  * 리턴타입 : boolean

### 제거
* remove()
  * 일치하는 객체나 해당되는 인덱스의 객체를 제거하는 메소드
  * 매개변수 : Object obj / int index
  * 리턴타입 : booelean
* removeAll()
  * 일치하는 객체를 모두 제거하는 메소드
  * 매개변수 : Object obj
  * 리턴타입 : void
* removeIf()
  * 조건에 해당되는 객체들을 찾아 제거하는 메소드
  * 매개변수 : Predicate (익명클래스를 생성)
  * 리턴타입 : boolean

### iterator()
* 리스트 안에 요소들을 반복자로 반환하는 메소드
* 매개변수 : X
* 리턴타입 : Iterator
```
반복자 (Iterator)
* fail-fast : 도중에 바로 예외를 발생 시킴
* hasNext() 
  * 다음 요소가 있는지 불리언으로 반환하는 메소드
* next()
  * 다음 요소를 반환하는 메소드
```

### clone()
* 객체를 복제하는 메소드

### size()
* 객체가 담겨있는 요소의 개수를 반환하는 메소드

### trimToSize()
* 객체가 담겨있지 않은 null 요소들을 삭제하는 메소드

> ## Vector 컬렉션 클래스
* ArrayList와 유사한 역할을 하는 클래스
* 동기화 처리, 멀티 쓰레드에 안전
* 생성자도 ArrayList와 유사
* add() / indexOf() / get() / ... 메소드 유사

### elementAt()
* 인덱스에 있는 요소 객체를 반환하는 메소드
* 매개변수 : int index
* 리턴타입 : Object

### elements()
* Vector 객체 안에 있는 요소들을 열거자로 반환하는 메소드
* 매개변수 : X
* 리턴타입 : Enumeration
```
열거자 (Enumeration)
* hasMoreElemnts()
  * 다음 요소가 있는지 불리언으로 반환하는 메소드
* nextElement()
  * 다음 요소를 반환하는 메소드
  ```




















