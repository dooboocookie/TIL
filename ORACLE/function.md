# 오라클 함수 정리

> ### NVL(exp1, exp2)
* exp1의 값이 널일 때, exp2로 변환

> ### NVL2(exp1, exp2, exp3)
* exp1의 값이 널이 아닐 때 exp2, 널일 때 exp3로 변환

> ### SUBSTR(char, pos, [ length ])
* char문자열에 pos위치부터 length길이만큼 출력
* pos이 음수면 뒤에서 부터

> ### TO_CHAR(date, [ format, [ nlsparm ] ])
* 날짜를 포맷에 맞춰 출력

> ### EXTRACT(datetime)
* datetime이나 interval 값으로 특정 날짜/시간 정보를 추출

> ### REGEXP_LIKE(char, pattern, [ match_option ])
* 정규표현식으로 해당되는 문자열 평가

> ### UPPER(char)
* 대문자로 변환

> ### CONCAT(char1, char2)
* 두 문자열을 합쳐 하나의 문자열로 변환

> ### REPLACE(char1, char2, char)
* char1 문자열 중 char2를 char3로 대체하여 문자열로 변환

> ### SYSDATE
* 시스템의 날짜 정보를 가져오는 함수

> ### VSIZE()
* 입력된 자료의 크기를 출력하는 함수
  * 한글 1문자 == 3바이트
  * 영문 1문자 == 1바이트
  * 숫자 == 2바이트 

> ### FLOOR()
버림하는 함수

> ### ROUND()
반올림하는 함수

> ### MOD(num1, num2)
* num1을 num2로 나누었을 떄 나머지 값을 반환하는 함수
* num1 - (num2 * FLOOR(num1 / num2)) 계산으로 나머지를 구함
  * REMAINDER()의 경우 버림대신 반올림으로 계산하는 함수
