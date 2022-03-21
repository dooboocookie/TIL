# 날짜, 시간과 관련된 패키지, 클래스
> ## Date 클래스
* 날짜와 시간에 관련된 클래스
* JDK1.0부터 오랫동안 사용된 클래스
* Calendar 클래스가 추가되면서 Date의 많은 메소드가 'deprecated' 됨

### 생성자 : Date()
* Date() : 현재 시스템의 날짜 정보를 가져와서 인스턴스를 생성하는 생성자
* Date(long date) : 1970.1.1 00:00:00 부터 밀리세컨드(date) 후의 날짜와 시간에 대해서 객체를 생성하는 생성자
* Date(int year, int month, int date) : 년(year) 월(month, 1월 == 0) 일(date)의 날짜에 대해서 객체를 생성하는 생성자

### toString(),  toGMTString()
* 인스턴스가 가진 날짜 시간 정보를 문자열로 반환
* 매개변수 : X
* 리턴타입 : String ("Mon Mar 21 11:44:00 KST 2022")

### getYear(), getMonth(), ...
* 인스턴스가 가진 정보에 년, 월, 일, 시간, 분, 초, ... 의 정보를 가져오는 getter 메소드
* 매개변수 : X
* 리턴타입 : int(1월 == 0 / 일요일 == 0)

### setYear(), setMonth(), ...
* 인스턴스에 년, 월, 일, 시간, 분, 초, ...정보를 입력하는 setter 메소드
* 매개변수 : int
* 리턴타입 : void

### after() / befor() / equals()
* 각 인스턴스의 날짜, 시간 정보를 비교하여 true/false 값을 반환하는 메소드
* 매개변수 : Date date
* 리턴타입 : boolean

### compareTo()
* 각 인스턴스의 값을 비교하여 -1, 0, 1을 반환하는 메소드
* 매개변수 : Date date
* 리턴타입 : int (0 : 같음, -1 : 작음, 1 : 큼)

> ## Calendar 클래스
* 날짜와 시간에 관련된 추상클래스
* JDK1.1부터 사용된 오래된 클래스

### 인스턴스 생성
* Calendar를 상속한 클래스인 GregorianCalendar의 인스턴스를 생성
* getInstance() static 메소드를 통해 시스템의 지역을 확인하여 GregorianCalendar 혹은 BuddhistCalendar의 인스턴스를 생성
```java
Calendar date1 = new GregorianCalendar(); 
// 시스템의 날짜 정보를 가지는 인스턴스 생성

Calendar date2 = new GregorianCalendar(1994, 11, 6);
// 1994년 12월 6일의 정보를 가진 인스턴스 생성

Calendar date3 = Calendar.getInstance();
// 시스템의 지역에 맞는 하위 클래스, 시스템의 날짜 정보를 가지는 인스턴스 생성
```

### Calendar.YEAR, Calendar.MONTH, ...
* 각 필드 값을 지칭하는 상수
* Calendar.YEAR == 1
* Calendar.MONTH == 2
* ...
* getter, setter 메소드에서 활용

### get()
* 인스턴스가 가지고있는 날짜, 시간 정보 중 해당되는 필드 값을 반환
* 매개변수 : int field
* 리턴타입 : int

### set ()
* 해당되는 필드 값을 인스턴스에 지정하는 메소드
* 매개변수 : int field, int value / int year, int mon, int date, int hour, int min, int sec
* 리턴타입 : void

```java
Calendar date = new GregorianCalendar(1994, 11, 6);
// 1994년 12월 6일

date.set(Calendar.YEAR, 2022);
// 2022년 12월 6일

date.set(2022, 2, 21);
// 2022년 3월 21일

System.out.println(date.get(Calendar.YEAR));
// 2022

System.out.println(date.get(Calendar.MONTH));
// 2
```

### add()
* 해당되는 필드의 값을 더하는 메소드 / 다른 필드에 영향
* 매개변수 : int field, int amount
* 리턴타입 : void

### roll()
* 해당되는 필드의 값을 더하는 메소드 / 다른 필드에 영향X
* 매개변수 : int field, int amount
* 리턴타입 : void

```java
Calendar date = new GregorianCalendar(1999, 11, 31);
// 1999년 12월 31일

date.add(Calendar.DATE, 1);
// 2000년 01월 01일

date.roll(Calendar.MONTH, -1);
// 2000년 12월 01일
```
