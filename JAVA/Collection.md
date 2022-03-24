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

> ## LinkedList 클래스

* 불연속적인 데이터들이 서로 연결한 자료구조
* 각 노드들이 다음 노드의 주소값을 참조하여 연결
* 배열과의 차이점
  * 배열은 간단한 데이터들을 물리적으로 묶여있어, 배열의 길이를 변경하거나, 비순차적인 데이터의 추가, 삭제에 시간이 많이 소요됨
  * LinkedList는 비순차적인 데이터 추가, 삭제가 배열에 비해 상당히 빠름
* List 인터페이스를 상속 : 순서 유지O, 중복 허용O 

### 종류
* 단방향 링크드 리스트
  * 노드에 다음 노드의 주소만 참조시켜 한방향으로만 연결시키는 링크드 리스트
* 양방향 링크드 리스트
  * 노드에 다음 노드와 이전 노드의 주소를 참조시켜 쌍방향으로 연결시키는 링크드 리스트
* 이중 환형 링크드 리스트
  * 쌍방향으로 연결시킥 마지막 노드에는 첫 노드를 참조, 첫 노드에는 마지막 노드를 연결시키는 링크드 리스트

### 간단한 구현
```java
public class ExLinkedList {
  public static void main(String[] args){
    Node node1 = new Node();
    node1.value = 10;
    Node node2 = new Node();
    node2.value = 20;
    Node node3 = new Node();
    node3.value = 30;
    Node node4 = new Node();
    node4.value = 40;

    node1.next = node2;
    node2.next = node3;
    node3.next = node4;
    node4.next = null;
  }//main
}//ExLinkedList

class Node{
  Object obj; // 해당 노드의 데이터 값
  Node next; // 다음 노드의 주소값 참조
  Node prev; // 이전 노드의 주소값 참조 (더블 링크드 리스트)
}
```

### LinkedList 생성자
* LinkedList() : 기본 용량이 없는 링크드 리스트 인스턴스를 생성
* LinkedList(Collection c) : 콜렉션 클래스를 포함하는 링크드 리스트 인스턴스를 생성

### 요소 추가
  * boolean add(Object obj) : 링크드 리스트 끝에 객체를 추가, boolean을 반환
  * void add(int idx, Object obj) : 인덱스 위치에 객체를 추가
  * boolean offer(Object obj) : 링크드 리스트 끝에 객체를 추가, boolean을 반환 / Queue 인터페이스에서 상속
  * addFist() / addLast() / ...

### 요소 반환
  * Object get(int idx) : 인덱스에 위치한 요소 객체를 반환
  * Object element() : 첫 인덱스의 위치한 객체를 반환 / Queue에서 상속
  * Object peek() : 첫 인덱스의 요소를 반환 / Queue에서 상속
  * Object poll() : 첫 인덱스의 요소를 반환하고 제거(꺼냄) / Queue에서 상속
  * ...

### 요소 검색
  * int indexOf(Object obj) : 일치하는 객체를 찾아 인덱스 정수를 반환
  * boolean contains(Object obj) : 일치하는 객체를 찾아 있으면 true를 반환
  * ...

### 요소 삭제
  * boolean remove(Object obj) : 일치하는 객체를 찾아 제거하고 boolean을 반환
  * ...

> ## Stack 클래스
* List 상속 : 순서 유지 O, 중복 허용 O
* LIFO(Last In First Out) - 마지막 순서(마지막으로 저장된)의 데이터를 처음으로 꺼내는 자료 구조
* 상속 
  * Collection <- List <- Vector <- Stack

### 생성자
* Stack() : 빈 용량의 인스턴스를 생성

### push()
* 마지막 위치에 요소 객체를 추가하는 메소드
* 매개변수 : Object obj
* 리턴타입 : Object(obj에 해당되는 자료형타입)
  
### pop()
* 스택의 맨위(마지막으로 저장된) 객체 요소를 꺼내어 반환(반환 후 삭제)
* 매개변수 : X
* 리턴타입 : Object / 비어 있으면 예외 발생

### peek()
* 스택의 맨위(마지막으로 저장된) 객체 요소를 반환(삭제X)
* 매개변수 : X
* 리턴타입 : Object / 비어 있으면 예외 발생


> ## Queue 인터페이스

* FIFO(First In First Out) - 처음 순서(먼저 저장된)의 데이터를 처음으로 꺼내는 자료 구조
* 상속
  * Queue <- Deque <- LinkedList

### 인스턴스 생성
* Queue 하위 인터페이스 Deque를 구현한 LinkedList로 업캐스팅하여 생성
```java
Queue q = new LinkedList();
```

### offer()
* 마지막 위치에 요소 객체를 추가하는 메소드
* 매개변수 : Object obj
* 리턴타입 : Object(obj에 해당되는 자료형타입)

### poll()
* 큐의 첫 순서(먼저 저장된) 객체 요소를 꺼내어 반환(반환 후 삭제)
* 매개변수 : X
* 리턴타입 : Object / 비어있으면 null 반환

### peek()
* 큐의 첫 순서(먼저 저장된) 객체 요소를 반환(삭제X)
* 매개변수 : X
* 리턴타입 : Object / 비어 있으면 null 반환

### PriorityQueue 클래스
* Queue의 하위 클래스
* Queue의 자료구조 개념에 객체들의 우선순위에 맞춰 꺼내는 특징
  * 숫자의 경우 오름차순 정렬(ex. 1 -> 2 -> 3 -> 4 -> 5)
  
### Deque
* Double-Ended Queue :  Queue의 맨 앞 / 맨 끝에서 데이터 저장 / 추출이 가능한 구조
* offerFirst() : 맨 앞에 저장
* offerLast() : 맨 뒤에 저장
* pollLast() : 맨 뒤에서 꺼냄(삭제)
* pollFirst() : 맨 앞에서 꺼냄(삭제)

> ## Iterator(반복자) 인터페이스

* 컬렉션 클래스에 저장한 객체 요소들을 읽어오는 방법을 표준화한 인터페이스
* fail-fast : 도중에 바로 예외를 발생 시킴
  
### 인스턴스 생성
* interator()
  * Iterator를 구현한 클래스의 인스턴스를 반환하는 메소드
```java
List list = new ArrayList();

Iterator ir = list.iterator();
```
### hashNext()
* 다음 요소가 있는지 확인하는 메소드
* 매개변수 : X 
* 리턴타입 : boolean

### next()
* 다음 요소 반환하는 메소드
* 매개변수 : X
* 리턴타입 : Object

### Enumeration(열거자)
* 컬렉션 프레임워크가 만들어지기 이전에 사용
* element() 메소드로 인스턴스 생성

### ListIterator
* Iterator는 이전 요소를 조회하려면 처음부터 다시 조회
* Iterator + 양방향 조회 / previous() 메소드
* listIterator() 메소드로 인스턴스 생성


> ## Arrays 클래스

* 배열을 다루는 기능이 구현된 클래스

### 메소드
1. Arrays.toString(null);
2. Arrays.fill(null, false);
3. Arrays.sort(null);
4. Arrays.binarySearch(null, 0);
5. Arrays.asList(null); ***
6. 배열복사 : Arrays.copyOf(), copyOfRange()


> ## Comparator 인터페이스 / Comparable 인터페이스
* 클래스 타입을 정렬하는 목적을 가진 인터페이스

### Comparable 인터페이스
* 클래스 타입을 정렬하는 기준을 구현할 때 사용
* compareTo() 메소드를 오버라이딩하여 비교하는 필드를 0 / 양수 / 음수 값을 반환하게 하여 오름차순, 내림차순같은 기준을 정함

### Comparator 인터페이스
* 클래스 타입을 다른 정렬 기준으로 정렬할 떄 사용
* compare() 메소드를 오버라이딩하여 비교하는 필드를 0 / 양수 / 음수 값을 반환하게 하여 오름차순, 내림차순같은 기준을 정함


> ## HashSet 컬렉션 클래스

* Set 인터페이스를 상속한 컬렉션 클래스, 그 중 대표적인 클래스
* Set 인터페이스의 특징 : 순서 유지 X / 중복 허용 X

### 생성자
* HashSet() : 디폴트 생성자,  초기용량이 16인 인스턴스 생성
* HashSet(int capacity) : 용량(정수)을 갖는 인스턴스 생성
* HashSet(Collection c) : 콜렉션의 객체들을 포함하는 인스턴스 생성

### add()
* 객체를 추가하는 메소드
* 데이터를 추가한 순서에 상관없이 데이터가 놓여짐
* 중복되는 객체는 추가하지 않음
* 매개변수 : Object obj
* 리턴타입 : boolean

### removd()
* 일치하는 객체를 제거하는 메소드
* 인덱스 값으로 자료를 수정하지 않음
* 매개변수 : Object obj
* 리턴타입 : boolean

```java
HashSet<Integer> hs = new HashSet<Integer>();

hs.add(9);
hs.add(1);
hs.add(15);
hs.add(20);
hs.add(15); // false

System.out.println(hs); // [1, 20, 9, 15]

hs.remove(20);
System.out.println(hs); // [1, 9, 15]
```

> ## TreeSet 컬렉션 클래스

* 이진 검색 트리(binary search tree) 자료구조
  * 루트 노드로 시작
  * 부모 - 자식 노드 관계 : 최대 2개의 자식 노드를 가짐
  * 형제 - 형제 노드 관계
  * 부모 노드 보다 작은 값은 왼쪽
  * 부모 노드 보다 큰 값은 오른쪽 
  * 정렬, 검색에서 높은 성능
* Set 특징 : 중복 허용 X / 순서 유지 X (정렬된 위치에 저장)

### 간단한 구현
```java
class TreeNode{
  TreeNode left; // 왼쪽 자식 노드의 주소 참조
  TreeNode ringt; // 오른쪽 자식 노드의 주소 참조
  Object obj; // 해당 노드의 저장할 객체
}
```
  



















