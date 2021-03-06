# 자바에서 사용되는 연산자 정리

> ### 산술 연산자
+ \+ : 덧셈 연산자, 이항 연산자   
+ \- : 뺄셈 연산자, 이항 연산자   
+ \* : 곱하기 연산자, 이항 연산자    
+ \/ : 나눗셈 연산자, 이항 연산자   
+ \% : 나머지 연산자, 이항 연산자   
<pre>
<code>
  System.out.println(5/0);  // 정수/0은 >> 산술적 예외 에러
  System.out.println(5%0);  // 정수%0은 >> 산술적 예외 에러
  System.out.println(3.14/0);  // 실수/0은 >> Infinity 리터럴
  System.out.println(3.14%0);  // 실수%0은 >> NaN
</code>
</pre>
> ### 비교 연산자
+ \== : 같다   
+ \!= : 다르다  //=와 =!는 완전히 다른 의미   
+ \>, <, >=, <=   

> ### 일반 논리 연산자
+ \&& : 일반 논리 AND 연산자 (논리 곱)   
T && T == T    
T && F == F    
F && T == F    
F && F == F   

+ \|| : 일반 논리 OR 연산자 (논리 합)   
T || T == T    
T || F == T    
F || T == T    
F || F == F   
+ \! 부정 연산자 (NOt 연산자)   
> ### 기타
+ ; 명령 종결 연산자   
+ . 멤버 연산자   
+ = 할당(대입) 연산자   
