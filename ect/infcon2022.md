# 인프콘 2022

> ## 한정수님 발표


> ## 이동욱님 발표
> ## 인프런 아키텍처의 과거, 현재 그리고 미래
> ## 리스크 기반의 적정 소프트 웨어 아키텍처

### 적정?
* A라는 목표를 B라는 일정안에 달성하기위해 감사하는 제약조건
  * 물을 건너가는데 돈과 동료가 없다면 > 직점 헤엄친다 > 혼자서 모든것을 다 해야된다외부 자원을 최대한 활용하자 직접 개발은 최소화하고 > 워드 프레스 > 회원수 10만 > 서비스가 느려진다 > 저장하는 데이터가 설계한 테이블이 아니였다.
  * 서버와 데이터를 한대에 둠
#### 시즌 2
* 백엔드 프론트엔드 데브옵스 대포1
  * 한명이 빠져도 개발이 가능해야한다?
    * 기술 스택 통일
      * 풀 js 
        * CDK -JS
    * 낮은 러닝 커브
      * FxDom? > 정적 html을 내려주고 DOm을 이후에 핸들링하는 
      * FxSQL  
    * 최소 관리
      * 직접 서버관리 X
      * 
* 3.5명의 개발자로 5개월만에
* 신규 개발자들이 채용 되면서 점점 발생하는 문제들
  * 구현 코드 최소화 코드상으로 확인 불가  > 테스트 코드 없다?
  * 단일화 라이브러리 > 부족한 생태계, 커뮤니티, 문서
  * 바닐라 자바스크립트? 대부분의 라이브러리가 리액트기반
  * 익숙한패턴 > 신입 개발자들은 익숙치 않는 구조, 패턴 
  * 단일 프로젝트
  * 높은 진ㅇ비장벽
  * 낮아진 심리적 안정감
  * 느려진 번들링, 리로드
  * 불가능한 컴포넌트 개발

#### 시즌 3
* 백엔드3 프론트엔드3, 데브옵스1, CTO1
* 심리적 안정감 > 클래스와 타입을 쓰자, 테스트코드 정적분석 > 이에스린트 프리터
* 낮은 진입장벽 > 타입스크립트, 리액트, 타입오알엠, 레이어드 아키텍처, DI
* 독립성 > 꼐층 분리, 명세기반 아키텍처, 분리된 레파지토리
* 빅뱅
  * 서비스 개선을 멈출지 > 1년
* 점진적 개편 
  * 서비스 개석과 개편 병행 기능 그룹별 이관  > 2년?
* 스타트업에서 6개월이란 시간은 일반 기업의 2년에 준하는 시간
* 매년 2~300퍼센트 성장하는 서비스를 중단 없이 개편하는 경험 >> 노하우...
* 백엔드와 프론트엔드를 순차적으로 
* 한기능의 장애가 전체 서비스의 장애로 확장

#### 시즌 4
* 백엔드 8 프론트 11 데브옵스 4
* 단일 프로젝트에 모든 하위 서비스 운영
* &rarr; 전체장애로 번지지 않도록
* 독립적으로 운영하는 서비스들은 분리를 한다
* 애플리케이션 서버의 메모리 시피유를 많이 점유하는 작업으로 인한 장애는 격리됨
* 데이터베이스 장애 격리는? > 다음시즌에
* 분산된 데이터베이스로 높아지는 복잡도 트랜잭션 관리의 어려움 기존 쿼리들의 전체 개편
* 높아진 장애 민감도
* 다양한 기능 요구사항
* 몽고디비아틀라스  > 검색앤지
* 검색엔진 아킽

> ## 얄코님 발표

### 1. 머나먼 오지의 개발자 (혼자 성장해야 했던 이유)

* `포항`에 위치한 스타트업
  * 동종업계 사람들이 없는 곳
  * 컨퍼런스 오프라인 활동에도 참여가 불가능한 상황
  * 사수가 없는 곳 
  * 리뷰를 받을 수가 없느 상황
  * 구식 개발 스택과 업무방식
  * 개발자 문화 부재 
    * 스터디, 코드리뷰, 워크숍, 지식공유등이 없는 상황이였다
  * 셀프 성장 고군분투기...

#### 토이프로젝트 (물길 찾기)

* 회사일과 별개로 실사용이 을 목표로한 토이프로젝트
  * 개발부터 배포 자동화 운영까지 오에스나 네
  * 다양한 기술과 스택 접목해보기
  * 배운것을 실무에 활용하기
    * 회사에도 구식 스택을 리뉴얼하거나 기술적 결정을 내릴떄 토이 프로젝트에서 배운점을 활용할 수 있었음

#### 지식공유
1. 유튜브
   1. 얄팍한 코딩사전
   2. 채널을 시작하게 된 계기 
      1. 책이나 문서를 읽어서는 바로 이해하기 어려운 개념들이 있다
         1. 레스트에이피아이 
         2. 함수영 프로그래밍
      2. 고통스럽게 이해한 후에 이것을 남에게 전달하고 싶어서
      3. 정보를 나만의 것으로 재구성
         1. 파편화된 정보를 남에게 말해줄 수 이슨 ㄴ정보로 재구성한다
         2. 알고있는거랑 남에게 전달할 수 있는건 지식의 깊이가 다르다
         3. 컨텐츠에 대한 나만의 정의가 되는 것
   3. 지적댓글의 공포
      1. 검토를 많이 한다
      2. 큰 스트레스지만 더더욱 자세히 아렉 된다
   4. 단점
      1. 시간대비효율이 좋지가 않음
2. 강의제작
   1. 유튜브와 차이점은 따로 편집이 필요하지 않아 비용이 적음
   2. 강의 진행에만 집중하면됨
      1. 가성비
   3. 각 주제를 마스터하는 가장 좋은 방법
   4. 나만의 강의 커리큘럼 구성
   5. 큐엔에이
      1. 답변에 대답하면서 부담스러우나
      2. 다른환경 및 미리 경험한 내용을 질문으로 올려주어 답변을 하면서 배울 수 있음
   6. 금전적 수입?
3. 책집필
   1. 기획, 집필, 퇴고, 편집, 소통
   2. 개발자 : 책을 쓰기 위한 수월한 직업

#### 마무리
* 성장을 향한 갈망
* 인센티브로 동력 불어넣기 
* 나만의 성장 로드를 뚫어라!!!!!!!!!! 



> # 김민준님 발표(라프텔. 개발자의 셀프 브랜딩)

* 15분 강의 녹화본 꼭 들어보기
* 벨로그 개발하신 분
* 개발 컨텐츠를 만드는 이유
  * 동기부여

> # 강동한님 발표(언어와 함께 성장하기)

* 노드제이에스는 자바스크립트 언어의 런타임입니다

## 왜 Node.js
* 버전 0.8.6 ?
* 대한민국은 자바공확국인데 왜 javascript일까요?
  * 프론트와 백앤드를 같은 언어로 하면 장점이 있지 않을까요?

## 언어와 함께 성장하기
* 콜백 > 프로미스 > 어싱크어웨이크


> # 김영한님 발표

## 나의 개발자 커리어 이야기
1. 게임 폐인
2. 게임 프로그래머
3. 최고의 컴퓨터 > 게임
4. 피자배달, IT학원, 고졸
5. 서울에서 취업 준비
6. 파견직 임금체불
7. IT 학원 강사 > 커리큘럼 준비(자바, JSP) > 어려운 내용을 쉽게 설명하는게 강점일 수 있겠다
8. SI > 여의도 > 이렇게는 못살겠다 > 회사의 부도
9. 가장 힘든 시기
10. 남는 시간을 쪼개서 개발 공부 > 지하철이나 버스에서  > 환경을 벗어나고 싶어서
11. 다음 커뮤니케이션 합격 >  
12. 우아한 형제들 기술이사
13. 밑바닥 부터 올라온 케이스? 
14. 개발자부터 기술이사까지 수많은 개발자 채용, 성장
15. 성장 취업 이직 주니어개발자의 이직

## 이직 

1. 가고싶은 회사를 1,2,3티어로 정리
   1. 1티어 언제가는 가고싶은 회사
   2. 2티어 그래도 가고싶다
   3. 취업을위해
2.  기술맞추기
    1.  1티어 회사들 채용 사이트 사용 기술 조사
    2.  비슷한 기술을 사용하는 23티어 회사들 찾기
3. 채용 확률 높이기
   1. 실무에서는 당장 사용하는 기술을 잘 다루는 경력자를 선호
   2. 기술을 맞추어 두면, 3티어 회사에 입사해도 경력을 쌓아서 1티어에 갈 확률이 높아짐
4. 신입 취업 격력 이직
   1. 1티어 회사는 신입으로 취업이 10배는 더 어려움
   2. 일단 3티어 회사로 취업
   3. 그게 안되면 개발 회사로 우선 취업
5. 3티어 2티어 1티어로 순위로 더 이직하기 쉬움
6. 성장
   1. 개발, 운영 개선 사이클을 다 경험해볼 수 있는 회사
   2. 프로덕트도 성장하고 엔지니어도 회사
   3. 타인의 제품을 만들어주는 회사
   4. 본인 제품을 만드는회사
   5. 개발 운영 개선
   6. 트래픽이 많으면 더 좋음
   7. 서비스 회사가 만들어내는 초과 수익은 아주 큼
   8. 기여도가 크고 초과 연봉 가능
7. 채용
   1. 채용은 확률이다
      1. 네카라쿠배는 합격하고 2티어만 합격하는 경우도 있다
      2. 같은 사람을 여려명이 면접을 봐도 서로 합격 불합격이 갈림
      3. 면접관마다 선호하는 것이 다 다르다
      4. 기술과 성향이 맞다면 합격 확률이 높음
      5. 티어가 높은 회사가 평균 기대치가 높다
         1. 사용자 , 트래픽, 돈, 개발자의 기여가 크다
   2. (실력있는)개발자의 TO는 무제한이다
      1. 개발자 채용 전쟁
         1. 시력있는 개발자를 위한 자라는 언제나 있다
         2. 실력이 가장 중요하다
         3. 시장에 실력있는 개발자가 부족하다
8. 이력서
   1. 서류에서 계속 탈락
      1. 아직 실력과 경험이 해당 티어에 가기에는 부족
         1. 기대치를 낮추고 회사 티어를 낮추어야한다
         2. 학습과 경험을 더 쌓아야 한다
      2. 실력은 있지만 이력서 작성 방법 부족
         1. 나쁜케이스 : 프로젝트만 나열
   2. 필살기
      1. 기술 면접관을 낚는 마법의 단어
         1. Solving problems is the core of cs
      2. 프로그래머는 세상의 문제를 해결해야한다
         1. 문제를 보는 순간 풀어야한다
         2. 해결방법이 궁금하다
      3. "문제와 해결"
      4. 프로젝트를 하다가 어떤 문제가 발생했는지, 어떻게 해결했는지
      5. 문제를 기술적으로 어떻게 해결했는지 자세히 적는다
         1. 어떤 문제가 일어났는지 자세히 히스토리를 적어야한다
         2. 기술적으로 깊이 있는 개발자를 선호한다
      6. "깊이!!!!!"
      7. 스스로 깊이있게 파고 학습한 개발자들은 보통 문제를 잘 해결한다
      8. 이력서를 잘쓰는 방법도 공부해야함
         1. 겸손도 중요하지만 본인 마케팅도 중요한
         2. 
      9. 문제 해결포인트
         1.  어떤 문제가 있었다 기술적으로 어ㄸ허게 해결했다 중요함
         2.  이렂ㄴ것을 통해 나의 기술적 깊이를 보여주어야 한다
         3.  이게 바로 면접에서 물어보는 낚시가 된다. 내가 준비한필살기를 물어볼 확률이 높다
9.  면접
    1.  실제로 내공이 부족
    2.  내가 안다는 것이 진짜 아는 걸까?
        1.  모 개발자의 스프링 강의를 다 들었는데, 그렇다고 정말 스플이응ㄹ 잘 아는 걸까?
        2.  학습 > 체득 > 정리
    3.  면접 시간은 짧다. 내가 아는 것을 정리해서 전달할 수 있었야한다.

## 학습
1, 궁극적으로 가고 싶은 회사의 기술스택 참고
채용공고에 다나와있음
서비스 플랫폼 백엔드는 주로 자바스프링
2. 학습의 3단계
   1. 학습
      1. 강의
      2. 책
   2. 체득
      1. 실무 적용
      2. 토이 프로젝트
   3. 정리
      1. 노트
      2. 블로그
      3. 세미나 만들기
      4. 면접에서 짧은 시간에 대답을 다 해야되는데, 정리를 해놓지 않으면 논리 정연하게 설명하지 못한다.
3. 지속적인 학습과 성장
   1. 마라톤
4. 시스템
   1. 목표와 시스템의 차이
   2. 오늘의 주제임
   3. 이번달까지 영어 점수를 100점 받는다
   4. 이번달까지 모개발자의 스프링 인강을 다 듣는다
   5. 목표는 달성하면 성공 아니면 실패
   6. 목표는 열정과 같이온다
   7. 열정이 생간다 >목표를 잡는 다> 실패한다> 좌절한다 > 포기한다 > 반복
   8. 열정은 불쏘시게 같은거
   9. 열정을 앞세워 목표를 준비하다 포기
   10. 목표의 성공과 실패가 아닌 과정에 충실
   11. 이게 바로 시스템
   12. 하루의 3깨ㅣ밥먹는것
   13. 시스템 루틴
   14. 퇴근 후 30분 운동
   15. 7시 30분 10시30분 학습 강의 준비
   16. 그냥 이시간에 앉아서 하는 것
   17. 열정이나 열심히 하는게 아닌다, 그냥 시스템에 나를 맡기는 것
   18. 시스템을 돌린다
   19. 이렇게 반복한다
   20. 시스템도 본인에게 맞도록 개선이 필요하다
   21. 시스템을 통해서 지속적으로 성장 > 개발 역량 상승 > 이직 성공
   22. 피드백 사이클
   23. 피드백은 빠를수록 좋다
   24. 야구선소의 공던지기 연습
   25. 던진 공이 스ㅌ트라이크인지 몇달 뒤에 알수있다면
   26. 테스트 케이스 빠르게 성공 실패를 확인
   27. 면접과 피드백
   28. 개발자 에이와개발자비의 실력은 비슷합
   29. 개발자에이
       1.  면접을 자주 보는 개발자 피드백 확률
       2.  더빨리 좋은 회사에 취업 서비스 회사에서 더 큰성장
   30. 개발자비
   31. 완벽하게 준비되고 면접 보는 개발자 피드백 확률
   32. 준비 과정에서 본인이 어떤것이 부족한지 인지하기 어렵다
   33. 시스템과 피드백 사이클
   34. 시스템을 통한 성장 > 이직 시도 피드백 > 사이클
   35. 시스템을 통해서 계속 성장
   36. 피드백을 통해 나의 상태
   37. 실무에서 업수시간 이후에 학습하는개발자가 그렇게 많지는 않음
   38. 시스템으로 매일 3시간 학습 
   39. 이렇게 학습하는 개발자는 잘 될 수 밖에 없음
   40. 보통 머리를 가지고 있다면 언제가 1티어 회사에 충분히 갈 수 잇음
   41. 속도의 차이이다

## 시스템

## 성장
1. 두 종류 개발자
   1. 진짜 실력잇는 개발자로 성장하는 개발자
   2. 그렇지 못한 개발자
2. 보통 개발자
   1. 주니어 3년 정도 되면 대충 업무 굴러가는 것 보임
   2. 담당 업무는 공부하지 않고 처리할 수 있음
   3. 더이상 공부할 것이 없다 생각합
   4. 업무를 잘하니 본인이 ㅈ라한다고생각
   5. 성장이 멈춤
   6. 혁신이 어려움 우물안 개구리
   7. 3년차 경험을 10년동안 반복
3. tlffurdltsms tlsldjfh tjdwkdgksms roqkfwk
   1. 공부하면 할수록 더 배울것이 나옴
   2. 본인이 배워야할 것이 많다생각함
   3. 실력은 있지만 겸서ㅗㄴ함
   4. 지속적인 성장 엄청난 내공
   5. 기술적인 혁신, 더 큰 도전을 즐김
   6. 실력있는 시니어 개발자로 성장
4. 기술적 겸손함
5. 대나무 이야기
   1. 대나무에 마디가 있는 것은
   2. 더 크게 성장하기 위함
   3. 사람은 컨디션 사이클이 있다
   4. 계속 기게처럼 할 수 없음
   5. 마음을 다지고, 삶의 방향과 시스템을ㅇ 점검하는 시간이 필요 우리는 사람
   6. 저는 3개월에 한번정도 산에가거나 좋은카페를 가는 것을 즐김
6. 마지막으로

> 시스템을 통해서 더 좋은 개발자로 지속해서 성장ㅎ나ㅡㄴ 것
> 좋은 회사, 높은 연봉은 자연스럽게 따라온다

* 개발은 팀웍

* 성장을 통해
* 주변 동료들에게
* 좋은 기술과 리더십

주변 동료들에게 인정받고
함께 일하고 싶은 개발자로 남는 것

