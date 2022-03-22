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

> ## Date - Calendar 변환

* Calendar -> Date
```java
Calendar c = Calendar.getInstance();

Date d1 = c.getTime();

Date d2 = new Date(c.getTimeMillis());
```
* Date -> Calendar
```java
Date d = new Date();

Calendar c = Calendar.getInstance();
c.setTime(d);
```
---
---
# java.time 패키지
* JDK1.8 추가
* Date와 Calendar의 단점을 극복하고자 추가된 패키지
* 불변(immutable)한 클래스들
* 하위 패키지
  * chrono : 표준(ISO)가 아닌 달력 시스템을 위한 클래스들
  * format : 날짜, 시간의 형식화를 위한 클래스들
  * temporal : 필드(field)와 단위(unit)을 위한 클래스들
  * zone : 시간대(time-zone)에 관련된 클래스들

> ## LocalDate 클래스 : 날짜
> ## LocalTime 클래스 : 시간
> ## LocalDateTime 클래스 : 날짜 + 시간
> ## ZonedDateTime 클래스 : 날짜 + 시간 + 시간대

### 구현된 상위 인터페이스
* Temporal
* TemporalAcessor
* TemporalAdjuster

### 인스턴스 생성
* now()
  * 시스템의 현재 날짜 및 시간 정보를 담아서 인스턴스를 생성하는 메소드
  * 매개변수 : X
  * 리턴타입 : LocalDate, LocalTime, ...
  
* of()
  * 입력된 정보들로 날짜 및 시간 정보를 담아서 인스턴스를 생성하는 메소드
  * 매개변수
    * int year, int month, int date
    * int hour, int minute, int second, ...
    * LocalDate, LocalTime
  * 리턴타입 : LocalDate, LocalTime, ...

### TemporalField 인터페이스
* 날짜 및 시간에 대한 필드를 정의한 인터페이스
* 구현 클래스 : ChronoField 클래스
* 필드
  * DAY_OF_WEEK : 요일
  * YEAR : 년
  * MONTH_OF_YEAR : 월
  * DAY_OF_MONTH : 일
  * HOUR_OF_DAY : 시(0~23)
  * CLOCK_HOUR_OF_AMPM : 시(1~12)
  * MINUT_OF_HOUR : 분(0~59)
  * SECOND_OF_MINUTE : 초(0~59)
  * ...

### TemporalUnit 인터페이스
* 날짜 및 시간의 단위를 정의한 인터페이스
* 구현 클래스 : ChronoUnit 클래스
* 필드
  * YEARS : 년
  * MONTHS : 월
  * DAYS : 일
  * HOURS : 시
  * MINUTES : 분
  * SECONDS : 초
  * ...

### get()
* 필드값에 해당되는 값을 정수로 반환하는 메소드
* 매개변수 : TemporalField field (ChronoField.XXX)
* 리턴타입 : int

### getXXX()
* 해당되는 날짜 정보를 출력하는 메소드
* 매개변수 : X
* 리턴타입 : 각 메소드에서 나타내는 날짜 정보에 맞는 타입
```java
LocalDate d = LocalDate.now();

int year = d.getYear();
System.out.println(year); //2022

year = d.get(ChronoField.YEAR);
System.out.println(year); //2022
```
### plus() / minus()
* 지정된 단위의 값을 더하거나 빼는 메소드
* 매개변수 : long amountToAdd, TemporalUnit unit
* 리턴타입 : LocalDate, LocalTime, ...

### with()
* 필드값에 해당되는 값을 변경하는 메소드
* 매개변수 : TemporalField field, long newValue
* 리턴타입 : LocalDate, LocalTime, ...
```java
LocalDate date = LocalDate.of(2022, 3, 22);
//2022-03-22
date = date.plus(30,ChronoUnit.DAYS);
//2022-04-21
date = date.plusDays(1);
//2022-04-22
date = date.with(ChronoField.MONTH_OF_YEAR, 3));
//2022-03-22
```
### truncatedTo()
* 입력된 단위 밑으로는 절삭하는 메소드
* 매개변수 : TemporalUnit unit
* 리턴타입 : LocalDate, LocalTime, ...

```java
LocalTime time = LocalTime.of(12, 34, 56);
//12:34:56
time = time.truncatedTo(ChronoUnit.HOURS);
//12:00
```
### isAfter() / isBefore() / isEquals()
* 두 인스턴스의 날짜, 시간 정보를 비교하여 true/false값을 반환하는 메소드
* 매개변수 : LocalDate, LocalTime, ...
* 리턴타입 : boolean

### 변환
* LocalDateTime atTime(LocalTime t)
* LocalDateTime atDate(LocalDate d)
* LocalDate toLocalDate()
* LocalTime toLocalTime()

```java
LocalDate d = LocalDate.now(); // 날짜
LocalTime t = LocalTime.now(); // 시간
LocalDateTime dt;

// LocalTime,LocalDate > LocalDateTime
dt = d.atTime(t);
dt = t.atDate(d);

// LocalDateTime > LocalTime,LocalDate
LocalDate a = dt.toLocalDate();
LocalTime b = dt.toLocalTime();
```

> ## Instant
* EPOCH TIME(에포크 타임, 1970-01-01 00:00:00)부터 경과된 시간을 나노초 단위로 표현
* Date의 대체를 위해 클래스
* Instant > Date 변환 : static Date from(Instant instant)
* Date > Instant 변환 : Instant toInstant()


> ## TemporalAdjusters 클래스
* 자주 쓰이는 날짜 계산을 메소드를 정의한 클래스

```java
LocalDate now = LocalDate.now();
System.out.println(now); // "2022-03-22"

// 다음 금요일
LocalDate result  = now.with(TemporalAdjusters.next(DayOfWeek.FRIDAY));
System.out.println(result); // "2022-03-25"

// 지난 금요일
result = now.with(TemporalAdjusters.previous(DayOfWeek.FRIDAY));
System.out.println(result); // "2022-03-18"
```
