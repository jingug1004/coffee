GaintCoffeeApplication
# 1. Giantcoffee Project 김진국
## 2. from  @home
### 3. Author: Emiya Mulzomdao
#### 4. since 180331
##### 5. Fighting
###### 6. Hidden?
####### 7. Hidden Fighting!
######## 8. Hidden Fighting 2nd!

- 원
    - 투
        - 쓰리
            - 포
                - 파이브
                    - 식스

#### 180331 (토)
- 설치, 개발환경 세팅
    - [SpringBoot] #1 IntelliJ 에서 spring boot 시작하기 
        - 출처: http://jaystevency.tistory.com/19 [JayDevLife]
    - Failed to auto-configure a DataSource: 'spring.datasource.url' is not specified and no embedded datasource could be auto-configured.
        - https://stackoverflow.com/questions/32074631/spring-boot-application-without-a-datasource?utm_medium=organic&utm_source=google_rich_qa&utm_campaign=google_rich_qa    
    - java.lang.IllegalArgumentException: Invalid character found in method name. HTTP method names must be tokens
        - https://stackoverflow.com/questions/42218237/java-lang-illegalargumentexception-invalid-character-found-in-method-name-http?utm_medium=organic&utm_source=google_rich_qa&utm_campaign=google_rich_qa


#### 171203 (일)
- loginUserController.java부터 끝
- pom.xml 디펜던시 추가
  - org.apache.commons.dbcp.basicdatasource 가 없다고 할 경우 
    출처: http://yangyag.tistory.com/165 [Hello Brother!]
  - [JSONObject] Maven Dependency 설정
    출처: http://jjeong.tistory.com/836 [jjeong]    
  - java: incompatible types: java.util.List<java.lang.Object> cannot be converted to java.util.List
    DaoImpl 전부 캐스트 데이터 타입 제외 (List<WhatVO>) 제거
- 웹 컨텐트 내용 전부 옮김
- properties 파일의 config_local.properties와 database_local.properties 수정함

# 

### AWS Deploy시 예상 되는 오류

### 디버깅 예상 되는 오류
- 끝 작업
    - 트랜잭션 필요 유무 체크
    - AES 암호화
        - ㅇㄴㄹㄴㅇㄹㄴㅇㄹ
            
- 글 제목, 글 내용, 댓글 내용 없으면 오류 알림창 떠야 함!            

@ 2017년 09월
- 170913 (수) header.jsp 안에 function keywordSearchAny() 의 window.location.hostname, window.location.port 한번 점검해봐야 함.
- CKEditor GET 성공!
- CKEditor CRUD 성공. size(rows, height)까지 디버깅 완료.
- 카테고리별 조건 검색 가능. 패턴 = yyyy-MM-dd HH:mm 디버깅. 전체 조회시 url 파라미터 분리시키기
- 카테고리별 조건 검색 완료.
- 전체 검색 한글만 입력 가능하게!
- Good, Bad, Want, Out tr td 웹단 구현
- 전체 검색에도 페이징 검색 가능하게 만듦(SPA로!)!
- 전체검색은 한 페이지당(perPageNum = 100) 100개씩 출력
- Input TYPE=“File” 을 히든으로 하고 외부 버튼을 눌러서 파일을 선택
- 게시판 글(리스트, readPage 등) width 1170으로 맞춤.
- BoardVO 에 updatedate VO 추가. GB를 위한 BoardGBVO VO 클래스 추가 

@ 2017년 10월
- 굿 씨앤티 누르면 ajax 로 처리되며 굿 씨앤티 테이블에 userid 추가, 삭제.
- 글 작성시 포인트 증가 디버깅 완료 / 댓글 작성시 포인트 증가 구현 해야함
- 글 작성시 50 추가 완료 / boardVO.getBno 말고 제목으로 가져오기
- 회원가입하면 자동으로 칼라별 넘버 카운트 됨.
- 글 쓰면 자동으로 tbl_color_result에 맞게 카운트 됨.
- 로그인, 회원가입 사진 변경(캐시 때문에 안 됨)
- 댓글도 삭제시 delete가 아니라 update로 블라인드 처리
- 칼라별 회원가입 수 tbl_user_color에 회원가입시(칼라별 번호에 따라) 자동 업데이트됨

### *포인트 기능
저는 포인트 테이블을 따로두시는게 좋을 것 같아요. 이력관리위해서
##1. 포인트 이력테이블
고객seq/일자/시퀀스/적립구분(적립or사용)/포인트
##2.포인트 마스터 테이블 추가 or 회원테이블에 잔여포인트 컬럼추가

## 포인트 적립,사용시
### 테이블
- 1.포인트 이력테이블에 인서트
- 2.포인트이력테이블의 합계로 2. 업데이트
- point 테이블(A): 잔액
- 고객키      + balance point(B point - C point)
- ex) jingug1004 + 100
- point 적립 테이블(B): insert
- 고객키      + 적립일 + 적립순번 + 적립 point + 소멸 예정일 + 적립 내용
- ex) jingug1004 + 171022 + 13      + 500        + 180121     + jingug1004님 회원가입으로 100포인트 적립(+)(jingug1004님 1567번 글 작성으로 50포인트 적립(+))
- point 사용 테이블(C): update
- 고객키      + 사용일 + 사용순번 + 사용 point + 사용 내용
- ex) jingug1004 + 171023 + 48      + 100        + jingug1004님 157번 상품 투자로 50포인트 사용(-)
- point 소멸 테이블(D): delete
- 고객키     + 소멸일     + 소멸순번 + 소멸 point + 소멸 내용
- ex) jingug1004 + 180121 + 27     + 300        + jingug1004님 1567번 글 삭제로 45포인트 소멸(-)
- B테이블과 C테이블에 insert/update/delete 발생시
- A 테이블의 금액을 조정(트리거 등 사용)
- 일배치로 B 테이블의 데이터를 읽어서(당일이 소멸일인 rows)
- D 테이블에 insert하고(추후 감사/증빙 등 사용)
- B 테이블에서 delete
- B 테이블에서 delete되었으므로 A 테이블의 balance point 조정
- 회원가입시 + 100 [완료]
- 글 작성시 + 50 [완료]
- 댓글 작성시 + 10 [완료]
- 굿, 배드, 스팸 누를 시 + 5 (다시 굿 배드 누르면 어떻게 처리해야 할까? 포인트 차감시켜야 하는데.)
- 매일 로그인 시 + 10
- vs
- 글 삭제시 - 50 [완료]
- 댓글 삭제시 - 10 [완료]

## *그래프
- 총 회원가입수 -> 디비에서 그냥 가져와서 뿌려주면 됨. [완료]

### 색깔별(정치가입별) 
- 회원가입수 [완]
- 회원활동량 : 글 작성 [완]
- 회원활동량 : 댓글 작성 [완]
- 회원활동량 : 버튼(굿) 누른 수
- 회원활동량 : 버튼(배드) 누른 수
- 회원활동량 : 버튼(스팸) 누른 수
- 회원활동량 : 색깔별 포인트

### 게시글 하나당
- 굿 누른 통계(원형 테이블)
- 배드 누른 통계(원형 테이블)
- 스팸 누른 통계(원형 테이블)
- 댓글 쓴 통계(원형 테이블)
- 글 쓴 통계(원형 테이블)

### 개인 회원 (등록)보여지는 정보(ajax, 게시글에)
- 잔여 포인트
- 활동수 : 글 작성수 [완]
- 활동수 : 댓글 작성수 [완]
- 회원활동량 : 버튼(굿, 배드, 스팸) 누른 수
- 존경하는 정치인

### 그래프 증감 꺽은선 그래프
- 월별, 주별, 일별
- 빨간색(+), 파란색(-)

### 전체 순위, 중간 순위

### 게시판 카테고리별 분석 그래프
- 원형
- 꺾은선
- 막대 그래프

### 상품 리스트 메뉴

### 해야할 것
- 날짜 AWS 기준이 아니라 현재 자바 DATE 기준으로 변경
- 세션에 담아 게시글 카운트 안 올라가게!
- 글쓴이의 아이피랑 댓글 단 사람의 아이피 보이게!

### 칼라별, 전체별 레벨 수
- 통계 메뉴로 들어가면 전체 업데이트 실행
- 각 게시판 글 리스트 들어가면 자신과 글쓴이 Lv.? 을 볼 수 있게 함

#### 추후 추가 기능
- 유저 요청에 따라 카테고리 만들어줌


쌍용강북교육센터

git_hub 기반의 스프링을 활용한 실전 프레임워크 설계와 구축 개발자.

스프링 실습 프로젝트 3조 독수리5형제 팀

쇼핑몰 서비스 개발 프로젝트.

## Team

독수리5형제 

- 김영재: Project Manager

- 김태영

- 마성익

- 전창건

- 황인배

## 프로젝트 진행 동기 및 목적

1. 기본적으로 상품소개, 판매서비스를 제공하고  심플하고 직관적인 UI를 통해 상품에 대한 고객의 편의성뿐만 아니라
1.  쇼핑몰 CEO가 상품등록 등의 기능을 통해 직접 관리할 수 있는 차별  화된 서비스를 제공
1. Java, Oracle, Web(HTML, CSS, JavaScript), Web Programming(Servlet, JSP), Spring Framework 등 Spring Web MVC 개발 전반에 걸쳐 주요 기술을 숙달할 수 있다.

## 아이템 선정 동기
- 개발자로서 가장 사회에서 많이 접하게 될 아이템을 주제로 선정.
> 2015년 성인 20-40대 기준 인터넷 쇼핑 이용률은 72% 2016년 11월 온라인 쇼핑몰 600만개 돌파 최대 한달 50만개의 쇼핑몰 오픈

## 참고
- [ziozia](https://www.ziozia.co.kr/main.asp)
- [zara](http://www.zara.com/kr/)

## 기능

### 회원

- 로그인
  - 비밀번호 찾기
  - SNS 계정연동
- 회원가입
  - 이메일인증
- 회원관리
  - 수정
  - 탈퇴
- 장바구니
  - 구매
  - 담기
   - 삭제
- 공지 게시판
   - 조회
- 이벤트 게시판
   - 조회
   - 쿠폰받기
- 내가쓴게시물
   - 조회
   - 삭제
- 적립금&쿠폰
   - 조회
- 구매내역 확인
   - 기간별 조회
- 리뷰
  - 등록(사진첨부O)
   - 조회
   - 삭제
- Q&A
   - 등록
   - 조회
   - 삭제
- 상품상세조회
   - 품목별 분류
- 오늘본상품

### 관리자
- 로그인
- 제품관리
   - 등록
   - 수정
   - 삭제
   - 조회
- 게시판 관리
   - 등록
   - 수정
   - 삭제
   - 답글
- 쿠폰&적립금
   - 등록
   - 지급
   - 수정
   - 삭제
- 판매관리
   - 기간별 조회
   - 배송상태 변경
   - 엑셀파일 변환
- 배너
   - 수정
   - 등록

### 기타
- 팀 소개

|일|월|화|수|목|금|토|
|:---:|:---:|:---:|:---:|:---:|:---:|:---:|
|03/12|[03/13][01]|[03/14][02]|[03/15][03]|[03/16][04]|[03/17][05]|03/18|
|-|기획|분석|분석|설계<br>(화면구성)|설계<br>(화면구성)|-|
|03/19|[03/20][06]|[03/21][07]|[03/22][08]|[03/23][09]|[03/24][10]|03/25|
|-|설계<br>(문서화)|설계<br>(DB모델링)|설계<br>(쿼리작성)|코딩 컨벤션|기능 구현|-|
|03/26|[03/27][11]|[03/28][12]|[03/29][13]|[03/30][14]|[03/31][15]|04/01|
|-|기능 구현|기능 구현|기능 구현|기능 구현|기능 구현|-|
|04/02|[04/03][16]|[04/04][17]|[04/05][18]|[04/06][19]|[04/07][20]|04/08|
|-|기능 구현|기능 구현|기능 구현|기능 구현|테스트|-|
|04/09|[04/10][21]|[04/11][22]|[04/12][23]|[04/13][24]|[04/14][25]|04/15|
|-|유효성검사|테스트|테스트|발표 준비|발표|-|

![Plan](http://sistfers.github.io/ingsta/docs/plan.png)

[01]: http://sistfers.github.io/ingsta/2017/03/13/planning.html "2017-03-13 기획"
[02]: http://sistfers.github.io/ingsta/2017/03/14/analysis.html "2017-03-14 분석"
[03]: http://sistfers.github.io/ingsta/2017/03/15/analysis.html "2017-03-15 분석"
[04]: http://sistfers.github.io/ingsta/2017/03/16/design.html "2017-03-16 설계"
[05]: http://sistfers.github.io/ingsta/2017/03/17/design.html "2017-03-17 설계"
[06]: http://sistfers.github.io/ingsta/2017/03/20/design.html "2017-03-20 설계"
[07]: http://sistfers.github.io/ingsta/2017/03/21/design.html "2017-03-21 설계"
[08]: http://sistfers.github.io/ingsta/2017/03/22/design.html "2017-03-22 설계"
[09]: http://sistfers.github.io/ingsta/2017/03/23/design.html "2017-03-23 설계"
[10]: http://sistfers.github.io/ingsta/2017/03/24/design.html "2017-03-24 설계"
[11]: http://sistfers.github.io/ingsta/2017/03/27/design.html "2017-03-27 설계"
[12]: http://sistfers.github.io/ingsta/2017/03/28/implementation.html "2017-03-28 구현"
[13]: http://sistfers.github.io/ingsta/2017/03/29/implementation.html "2017-03-29 구현"
[14]: http://sistfers.github.io/ingsta/2017/03/30/implementation.html "2017-03-30 구현"
[15]: http://sistfers.github.io/ingsta/2017/03/31/implementation.html "2017-03-31 구현"
[16]: http://sistfers.github.io/ingsta/2017/04/03/implementation.html "2017-04-03 구현"
[17]: http://sistfers.github.io/ingsta/2017/04/04/implementation.html "2017-04-04 구현"
[18]: http://sistfers.github.io/ingsta/2017/04/05/implementation.html "2017-04-05 구현"
[19]: http://sistfers.github.io/ingsta/2017/04/06/implementation.html "2017-04-06 구현"
[20]: http://sistfers.github.io/ingsta/2017/04/07/implementation.html "2017-04-07 구현"
[21]: http://sistfers.github.io/ingsta/2017/04/10/test.html "2017-04-10 시험"
[22]: http://sistfers.github.io/ingsta/2017/04/11/test.html "2017-04-11 시험"
[23]: http://sistfers.github.io/ingsta/2017/04/12/test.html "2017-04-12 시험"
[24]: http://sistfers.github.io/ingsta/2017/04/13/test.html "2017-04-13 시험"
[25]: http://sistfers.github.io/ingsta/2017/04/14/presentation.html "2017-04-14 발표"



## Repository

[GitHub](http://github.com/sistfers/ingsta)

## Modeling

[Modeling](https://github.com/sistfers/Man-In-Black/tree/master/modeling)

### Entity-Relationship Diagram

![ERD](https://github.com/sistfers/Man-In-Black/blob/master/modeling/Man_In_Black_ERD.png?raw=true)

### Flowchart

![Flowchart](https://github.com/sistfers/Man-In-Black/blob/master/modeling/Flowchart.jpg)

## 개발 환경 및 개발 툴
- [Java SE 8 (Oracle JDK 1.8.x)](http://www.oracle.com/technetwork/java/javase/downloads)
- [Oracle Database 12c Release 1 (12.1.x Enterprise Edition)](http://www.oracle.com/technetwork/database/enterprise-edition/downloads)
- [Spring Tool Suite (3.8.x)](http://spring.io/tools/sts/all)
- [Apache Tomcat (8.5.x)](http://tomcat.apache.org)
- [Apache Maven (3.3.x)](http://maven.apache.org)
- [eXERD](http://exerd.com)
- [Gliffy Diagrams](http://www.gliffy.com)
- [Git](http://git-scm.com)
- [GitHub](http://github.com)
- [Maven Central Repository](http://maven.org)

## 적용 기술 및 라이브러리 의존성
- [Spring Framework 4.3.x](http://projects.spring.io/spring-framework)
- [JUnit 4.12](http://junit.org/junit4)
- [MyBatis 3.4.x](http://www.mybatis.org/mybatis-3)
- [MyBatis-Spring 1.3.x](http://www.mybatis.org/spring)
- [Servlet 3.1.x](http://jcp.org/en/jsr/detail?id=340)
- [JSP 2.3.x](http://jcp.org/en/jsr/detail?id=245)
- [EL 3.0.x](http://jcp.org/en/jsr/detail?id=341)
- [JSTL 1.2.x](http://jcp.org/en/jsr/detail?id=52)
- [JSON Processing](http://jcp.org/en/jsr/detail?id=374)
- [Oracle JDBC Thin Driver 12.2.0.1](http://www.oracle.com/technetwork/database/features/jdbc/jdbc-ucp-122-3110062.html)
- [Oracle 11g Release 2 (11.2) Standard SQL](http://docs.oracle.com/cd/E11882_01/server.112/e41084/ap_standard_sql.htm)
- [Oracle 12c Release 1 (12.1) Standard SQL](http://docs.oracle.com/database/121/SQLRF/ap_standard_sql.htm)
- [HTML5](http://w3.org/TR/html5)
- [CSS3](http://w3.org/TR/CSS)
- [JavaScript (ECMA-262 ECMAScript)](http://ecma-international.org/publications/standards/Ecma-262.htm)
- [jQuery 3.1.x](http://jquery.com)
- [jQuery UI 1.12.x](http://jqueryui.com)
- [Bootstrap 3.3.x](http://bootstrapk.com)
- [Log4j 2.8.x](http://logging.apache.org/log4j)
- [SLF4J 1.7.x](http://slf4j.org)
- [Semantic Versioning](http://semver.org)
- [NAVER Maps](http://github.com/navermaps/maps.js)
- [NAVER SmartEditor](http://github.com/naver/smarteditor2)
- [Daum Maps](http://apis.map.daum.net)
- [Daum Postcode](http://github.com/daumPostcode)
- [Google Maps](http://enterprise.google.com/intl/ko/maps)

## 배포 타겟 서버 런타임 환경 및 브라우저 호환성
- Microsoft Windows 10 Insider Preview
- Oracle Java SE HotSpot Virtual Machine JRE 8u121
- Oracle Database 12c Release 1 Enterprise Edition 12.1.0.2.0
- Apache Tomcat 8.5.12
- Chrome Stable Version

## Site
[GitHub Pages](http://sistfers.github.io/Man-In-Black)

## Repository
[GitHub](http://github.com/sistfers/Man-In-Black)


# 쌍용강북교육센터 팀 프로젝트 3차

## 프로젝트 소개

### 기간
**2016.08.29 ~ 2016.10.12**

### 참여인원
+ 5명

### 주제
**'Facebook'을 벤치마킹한 SNS 웹 사이트**

### 핵심 기능
+ 회원
+ 뉴스피드
+ 친구 관리
+ 일정(이벤트) 관리
+ 그룹 관리

### ----- 버전기록 -----

_2016.10.04 4차_

**권아영**
+ 친구 sns이동
+ 로그인한 회원으로 적용
+ 친구 그룹 설정 가능

**김명호**
+ 이벤트 상세보기
+ 이벤트 초대

**조성환**
+ 마이페이지 [수정 및 추가]
+ 프로필사진 [파일 업로드 및 수정]
+ 회원가입 [조건]

**조용호**


**한영선**
+ 뉴스피드 리스트 이미지 포함, 스크립트 수정
+ 좋아요, 댓글

_2016.09.26 3차_

**권아영**
+ 친구맺기, 끊기
+ 차단(기능) : 불완전함
+ 친구외검색 
+ 알수도 있는 친구
+ 친구요청 :수락 ,거절 , 요청취소

**김명호**
+ 일정 - 이벤트 만들기 기능
	+ 날짜/시간 - 외부 플러그인 사용
	+ 이미지 업로드

+ 보고서 - 각 기능별 진행률 차트

**조성환**
+ 로그인 (폰 번호 및 아이디로 로그인 가능)
+ 회원가입 (이메일 인증번호 발송 및 주소 API)
+ 마이페이지 (경력 및 학력, 자세한 내 소개, 가족 및 결혼/연애 상태 입력 및 수정)

**조용호**
+ 추천 그룹 리스트
+ 그룹 가입요청 
+ 그룹 사진 보기
+ 그룹 파일 다운로드

**한영선**
+ 뉴스피드 담벼락 작성 Form
+ 뉴스피드 담벼락 리스트 Form (수정 모달 포함)
+ 뉴스피드 작성/삭제
+ 뉴스피드 리스트(이미지 미포함, 스크립트 수정 전) 

_2016.09.09 2차_

**권아영**
+ 친구 리스트
+ 친구 예정자 리스트 Form(팔로우, 요청 미수락)
+ 차단 친구, 그룹 설정 Form

**김명호**
+ 현재 달 Form
+ 이전/다음 달 Form
+ 이벤트 만들기 Form

**조성환**
+ 로그인 Form
+ 회원가입 Form

**조용호**
+ 그룹 만들기
+ 그룹 리스트 보기
+ 멤버 리스트
+ 추천 그룹 리스트
+ 그룹 가입요청
+ 그룹 사진 
+ 그룹 파일 다운로드
+ 그룹 멤버 

**한영선**
+ 뉴스피드 담벼락 작성 Form

_2016.09.07 1차_
+ Spring 기본 환경설정
	+ 오류로 백업 기록 못 함