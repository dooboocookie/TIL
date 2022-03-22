# 형식화 클래스

* java.text 패키지에 포함되어있는 클래스들
* 숫자, 날짜, 문자열 데이터를 정의한 형식에 맞춰 반환하거나, 형식화된 문자열에서 원하는 정보를 추출할 떄 사용
  
> ## DecimalFormat 클래스

* 숫자 데이터를 단위 구분자, 소수점, 통화, 퍼센트,...로 형식화 하는 클래스

### 생성자
* new DecimalFormat() : default format 사용
* new DecimalFormat(String pattern) : 입력된 패턴으로 인스턴스 생성

### 패턴 기호
* 0 : 10진수 (값이 없을 떄 0)
* \# : 10진수 (값이 없을 때 공백)
* . : 소수점
* , : 단위 구분자
* \- : 음수
* \u00A4 : 통화 기호 (시스템 지역에 맞는)
* ' : escape문자
* % : 퍼센트
* \u2030 : 퍼밀 (퍼센트 x 10)
* ; : 패턴 구분자
* E : 지수 기호

### format()
* 인스턴스에 지정된 형식에 맞춰 숫자 데이터를 문자열을 반환하는 메소드
* 매개변수 : long / double / Object
* 리턴타입 : String

```java
String pattern = "\u00A4 #.###.#";
DecimalFormat df = new DecimalFormat(pattern);

String str = df.format(1234567.89);
System.out.println(str);
//"₩1,234,567.9+"
```

### parse()
* 인스턴스에 지정된 형식에 맞는 문자열에서 숫자 데이터를 얻어 반환하는 메소드
* 문자열이 형식에 맞지 않으면 예외 발생
* 매개변수 : String
* 리턴타입 : Number

```java
DecimalFormat df = new DecimalFormat("₩#,###.#");
try {
    Number number = df.parse("₩1,234,567.89");
    System.out.println(num.doubleValue());
    //1234567.89
} catch (ParseException e) {
	e.printStackTrace();
}
```


> ## SimpleDateFormat 클래스

* DateFormat 클래스의 하위 클래스로 날짜, 시간 데이터를 원하는 형식화 하기 위한 클래스

### 생성자
* new SimpleDateFormat() : default format 사용
* new SimpleDateFormat(String pattern) : 입력된 패턴으로 인스턴스 생성

### 패턴 기호
* 년 : yy(22) / yyyy(2022)
* 월 : M(3) / MM(03) / MMM(Mar) / MMMM(Martch)
* 일 : d(1) / dd(01)
* 요일 : E(Tue) / EEEE(Tuesday)
* 시 : h(1~12) / H(0~23)
* 분 : m(0~59)
* 초 : s(0~59) / S(밀리세컨드)
  
### format()
* 인스턴스에 지정된 형식에 맞춰 날짜, 시간 데이터를 문자열을 반환하는 메소드
* 매개변수 : Date / Object
* 리턴타입 : String


```java
String pattern = "yyyy년 MM월 dd일 a hh:mm:ss:S(EEEE)";
SimpleDateFormat sdf = new SimpleDateFormat(pattern);

String str = sdf.format(new Date());
System.out.println(str);
//"2022년 03월 22일 PM 09:23:44:388(Tuesday)"
```

### parse()
* 인스턴스에 지정된 형식에 맞는 문자열에서 날짜, 시간 데이터를 얻어 반환하는 메소드
* 문자열이 형식에 맞지 않으면 예외 발생
* 매개변수 : String
* 리턴타입 : Date

```java
SimpleDateFormat sdf = new SimpleDateFormat("yyyy.MM.dd(E)");
try {
    Date d = sdf.parse("2022.03.22(Tue)");
    System.out.println(d);
    //Tue Mar 22 00:00:00 KST 2022
} catch (ParseException e) {
	e.printStackTrace();
}
```

> ## ChoiceFormat 클래스

* 범위를 나타내는 형식에 맞춰 반환하기 위한 클래스

### 생성자
* ChoiceFormat(String pattern)
  * 문자열에서 나타내는 <(경계 포함 X), # (경계 포함)로 표현된 값에 따른 범위를 갖는 인스턴스 생성
* ChoiceFormat(double[] limit, String[] pattern)
  * 경계값을 담고있는 실수 배열과 그 값에서 출력되는 패턴을 담고있는 문자열 배열 정보를 갖는 인스턴스 생성

### format()
* 입력된 값을 범위에 맞는 문자열을 반환하는 메소드
* 매개변수 : long(정수)
* 리턴타입 : String
  
```java
String[] grades = {"F","D","C","B","A"};
double[] limits = {0,60,70,80,90};
ChoiceFormat cf = new ChoiceFormat(limits, grades);

System.out.println(cf.format(65));
//"D"
```

> ## MassageFormat 클래스

* 여러 데이터들을 형식에 맞춰 출력하거나, 형식화된 문자열에서 특정 데이터를 얻기 위한 클래스

### format()
* static 메소드
* 데이터들을 형식에 맞춰 문자열로 반환하는 메소드
* 매개변수 : String pattern, Object... arguments
* 리턴타입 : String

```java
String name = "Hwan";
int age = 29;
boolean gender = true;

String message = MessageFormat.format("이름 : {0}, 나이 : {1}살, 성별 : {2}", name, age, gender? "남자" : "여자");
System.out.println(message);
//"이름 : Hwan, 나이 : 29살, 성별 : 남자"
```

### parse()
* 형식화된 문자열에서 원하는 정보를 얻는 메소드
* 매개변수 : String src
* 리턴타입 : Object

```java
String src = "이름 : Hwan, 나이 : 20살, 성별 : 남자";
String pattern = "이름 : {0}, 나이 : {1}살, 성별 : {2}";
MessageFormat mf = new MessageFormat(pattern);
try {
	Object[] objs = mf.parse(src);
	for (Object object : objs) {
		System.out.println(object);
        //"Hwan" "20" "남자"
	}
} catch (ParseException e) {
	e.printStackTrace();
}
```
