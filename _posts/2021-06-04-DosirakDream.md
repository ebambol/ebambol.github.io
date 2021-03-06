---
layout: single
title:  "[Project] 도시락드림"
categories: Project
tags: 
  - [Project, DosirakDream]
toc: true
toc_sticky: true
last_modified_at: 2021-06-25
---

> 도시락드림ppt 를 정리한 페이지입니다.
> ppt는 [Github](https://github.com/ebambol/DosirakDream)에서 받으실 수 있습니다.

### 🌲 프로젝트 개요

시니어 세대를 위한 도시락 배달 및 도움 서비스

상품의 주문도 받고 고령자의 안부를 확인하여 가족이 안심할 수 있는 도시락 제품을 판매하기 위한 플랫폼 개발하였습니다.

- 소스코드  [Github](https://github.com/ebambol/DosirakDream)


#### 🍁 개발환경

Java 1.8.0_171
Tomcat 9.0
Bootstrap 5.0 beta
MySQL 8.0.17

#### 🍁 사이트맵 구성

![슬라이드6](https://user-images.githubusercontent.com/73654909/124751465-9f28b900-df61-11eb-8c6b-1cf19fea5ae0.PNG)

- 도시락드림 프로젝트는 상품관련한 전체종류, 반찬종류, 국/찌개종류, 밥 종류로 구성되어있고, 상품을 추가하였을때 장바구니 페이지와 상품주문 페이지로 구성되어 있습니다.

- 회원과 관련된 로그인, 로그아웃, 회원가입과 소통을 위한 공지사항, 게시판이 존재합니다. 아이디가 admin일 경우 관리자페이지와 공지사항,게시판,상품을 등록,수정,삭제가 가능합니다.

### 🌲 구성

#### 🍁 데이터베이스 구성

회원정보, 상품정보, 장바구니정보, 공지사항, 게시판으로 구성되어 있습니다.

##### 🍂 product 상품 정보 관리

| 순번 | 칼럼  명 | 칼럼  설명   | 타입         | Null? | Key  | Default |
| ---- | -------- | ------------ | ------------ | ----- | ---- | ------- |
| 1    | pno      | 상품  코드   | varchar(10)  | NO    | PRI  | Null    |
| 2    | pname    | 상품  이름   | varchar(20)  | NO    |      | Null    |
| 3    | price    | 상품  가격   | integer      | NO    |      | Null    |
| 4    | info     | 상품  설명   | text         | NO    |      | Null    |
| 5    | category | 상품  분류   | varchar(10)  | NO    |      | Null    |
| 6    | filename | 상품  이미지 | varchar(100) | YES   |      | Null    |

##### 🍂 jsp_member 회원정보

| 순번 | 칼럼  명 | 칼럼  설명     | 타입        | Null? | Key  | Default |
| ---- | -------- | -------------- | ----------- | ----- | ---- | ------- |
| 1    | id       | 회원  아이디   | varchar(50) | NO    | PRI  | Null    |
| 2    | password | 회원  비밀번호 | varchar(50) | NO    |      | Null    |
| 3    | username | 회원  이름     | varchar(20) | NO    |      | Null    |
| 4    | addr1    | 주소           | varchar(50) | NO    |      | Null    |
| 5    | addr2    | 상세주소       | varchar(30) | NO    |      | Null    |
| 6    | phone    | 휴대폰  번호   | varchar(20) | NO    |      | Null    |

##### 🍂 cart 장바구니 정보

| 순번 | 칼럼  명     | 칼럼  설명   | 타입        | Null? | Key  | Default |
| ---- | ------------ | ------------ | ----------- | ----- | ---- | ------- |
| 1    | product_num  | 상품 코드    | varchar(20) | NO    | PRI  | Null    |
| 2    | product_name | 상품  이름   | varchar(50) | NO    |      | Null    |
| 3    | userid       | 회원  아이디 | varchar(20) | NO    |      | Null    |
| 4    | price        | 가격         | integer     | NO    |      | Null    |

##### 🍂 notice 정보

| 순번 | 칼럼  명 | 칼럼  설명       | 타입        | Null? | Key  | Default | Extra          |
| ---- | -------- | ---------------- | ----------- | ----- | ---- | ------- | -------------- |
| 1    | Id       | 공지사항 ID      | Int(11)     | NO    | PRI  | Null    | Auto_increment |
| 2    | title    | 제목             | varchar(20) | YES   |      | Null    |                |
| 3    | content  | 내용             | text        | YES   |      | Null    |                |
| 4    | writeid  | 작성자           | varchar(20) | YES   |      | Null    |                |
| 5    | ntdate   | 작성일           | Datetime    | YES   |      | Null    |                |
| 6    | hit      | 조회수  (미구현) | Int(100)    | YES   |      | 0       |                |
| 7    | files    | 파일             | varchar(30) | YES   |      | Null    |                |
| 8    | pub      | 공개여부         | Int(1)      | NO    |      | 0       |                |

##### 🍂 board 구성

| 순번 | 칼럼  명 | 칼럼  설명      | 타입        | Null? | Key  | Default | Extra          |
| ---- | -------- | --------------- | ----------- | ----- | ---- | ------- | -------------- |
| 1    | Id       | 게시글 고유번호 | Int(11)     | NO    | PRI  | Null    | Auto_increment |
| 2    | title    | 제목            | varchar(20) | YES   |      | Null    |                |
| 3    | content  | 내용            | text        | YES   |      | Null    |                |
| 4    | writeid  | 작성자          | varchar(20) | YES   |      | Null    |                |
| 5    | bdate    | 작성일          | Datetime    | YES   |      | Null    |                |

#### 🍁 자바 코드 구성

```
📂src
├──📘controller				#📘컨트롤러
│	├──📘admin					#📘관리자 페이지
│	│	├──📘board					#📘게시판
│	│	│	├──📝DeleteController			#📝게시판 삭제
│	│	│	├──📝DetailController			#📝게시판 상세
│	│	│	├──📝ListController				#📝게시판 리스트
│	│	│	├──📝RegController				#📝게시판 게시글 등록
│	│	│	├──📝UpdateController			#📝게시글 수정
│	│	│	└──📝UpdateProcessContoller			#📝게시글 수정처리
│	│	├──📘notice					#📘공지사항
│	│	│	├──📝DeleteController			#📝공지사항 삭제
│	│	│	├──📝DetailController			#📝공지사항 상세
│	│	│	├──📝ListController				#📝공지사항 리스트
│	│	│	├──📝RegController				#📝공지사항 게시글 등록
│	│	│	├──📝UpdateController			#📝공지사항 게시글 수정
│	│	│	└──📝UpdateProcessContoller			#📝공지사항 게시글 수정처리
│	│	└──📘product					#📘상품
│	│		├──📝AddController				#📝상품 추가
│	│		├──📝DeleteController			#📝상품 삭제
│	│		├──📝DetailController			#📝상품 상세
│	│		├──📝PageController				#📝상품 리스트
│	│		├──📝UpdateController			#📝상품 수정
│	│		└──📝UpdateProcessController		#📝상품 수정처리
│	├──📘board					#📘게시판
│	│	├──📝DeleteController			#📝게시판 삭제
│	│	├──📝DetailController			#📝게시판 상세
│	│	├──📝ListController				#📝게시판 리스트
│	│	├──📝RegController				#📝게시판 게시글 등록
│	│	├──📝UpdateController			#📝게시글 수정
│	│	└──📝UpdateProcessContoller			#📝게시글 수정처리
│	├──📘cart					#📘카트
│	│	├──📝addCartController			#📝카트 추가
│	│	├──📝CartController				#📝카트 페이지
│	│	├──📝DeleteCart				#📝카트 전체 제거
│	│	└──📝RemoveCartController			#📝카트 선택 제거
│	├──📘member					#📘회원
│	│	├──📝SignInController			#📝로그인
│	│	└──📝SignUpController			#📝로그아웃
│	├──📘notice					#📘공지사항
│	│	├──📝DetailController			#📝상세
│	│	└──📝ListController				#📝리스트
│	├──📘order					#📘주문
│	│	├──📝OrderController			#📝주문페이지
│	│	└──📝OrderProcessController			#📝주문처리
│	├──📘product					#📘상품
│	│	└──📝ListController				#📝상품리스트
│	└──📝indexController			#📝홈페이지
├── 📘entity					#📘테이블
│	├──📝Board					#📝게시판 테이블
│	├──📝BoardView				#📝게시판 뷰 테이블
│	├──📝Cart					#📝카트 테이블
│	├──📝Member					#📝회원 테이블
│	├──📝Notice					#📝공지 테이블
│	├──📝NoticeView				#📝공지 뷰 테이블
│	└──📝Products				#📝상품 테이블
├── 📘service				#📘서비스
│	├──📝BoardService					#📝게시판 서비스
│	├──📝CartService					#📝카트 서비스
│	├──📝MemberService					#📝회원 서비스
│	├──📝NoticeService					#📝공지 서비스
│	├──📝OrderService					#📝주문 서비스
│	└──📝ProductsService				#📝상품 서비스
└──📘util					#📘유틸
	├──📝CharacterEncodingFilter  		#📝인코딩 필터
	└──📝Member					#📝회원 서비스
```

#### 🍁 view 구성

```
📂WebContent
├──📂parts
│	├──📝footer.jsp		#푸터페이지
│	└──📝header.jsp		#헤더페이지
├──📂resources		
│	├──📂css
│	│	└──📘style.css	#커스텀 css
│	└──📂js
│		└──📒script.js	#js
└──📂WEB-INF
	└──📂view
		├──📂admin				#관리자 페이지
		│	├──📂board				#게시판
		│	│	├──📝detail.jsp			#상세
		│	│	├──📝list.jsp			#목록
		│	│	├──📝reg.jsp			#글쓰기
		│	│	└──📝update.jsp			#수정
		│	└──📂notice				#공지사항
		│		├──📝detail.jsp			#상세
		│		├──📝list.jsp			#목록
		│		├──📝reg.jsp			#글쓰기
		│		└──📝update.jsp			#수정
		├──📂board				#게시판
		│	├──📝detail.jsp			#상세
		│	├──📝list.jsp			#목록
		│	├──📝reg.jsp			#글쓰기
		│	└──📝update.jsp			#수정
		├──📂member				#회원 페이지
		│	├──📄signIn.jsp			#로그인
		│	├──📄signOut.jsp			#로그아웃
		│	├──📄signUp_success.jsp		#회원가입 성공
		│	└──📄signUp.jsp			#회원가입
		├──📂notice				#공지사항
		│	├──📄detail.jsp			#상세
		│	└──📄list.jsp			#목록
		└──📂product			#상품
			├──📄addDosirak.jsp			#추가
			├──📄cart.jsp			#카트페이지
			├──📄detail.jsp			#상품 상세
			├──📄edit.jsp			#상품 관리
			├──📄index.jsp			#홈페이지
			├──📄list.jsp			#상품 목록
			├──📄order_process.jsp		#주문 처리
			├──📄order.jsp			#주문
			└──📄update.jsp			#상품 수정
```

### 🌲 화면구성

#### 🍁 메인 페이지

![슬라이드14](https://user-images.githubusercontent.com/73654909/124752932-6ab5fc80-df63-11eb-9b41-f570925eb8f5.PNG)

비로그인시 로그인과 회원가입 버튼이 나타나도록하고 홈페이지에서는 카테고리별로 3개의 상품을 출력해서 보여줍니다.

#### 🍁 비로그인

![슬라이드15](https://user-images.githubusercontent.com/73654909/124753046-7ef9f980-df63-11eb-91c9-eb451d3f4565.PNG)

로그인과 회원가입 버튼을 클릭했을때 나오는 페이지입니다.

![슬라이드16](https://user-images.githubusercontent.com/73654909/124753089-8c16e880-df63-11eb-90ed-a9c0d58ac48c.PNG)

`div`태그에 `onclick`을 이용하여 상세페이지로 이동하도록 하였습니다.

![슬라이드14](https://user-images.githubusercontent.com/73654909/120837514-bf034080-c5a1-11eb-98d2-0be90a178134.PNG)

장바구니 추가와 장바구니는 비로그인시 사용이 불가하며 클릭시 로그인 페이지로 이동합니다.

#### 🍁 회원 로그인

![슬라이드15](https://user-images.githubusercontent.com/73654909/120837515-bf9bd700-c5a1-11eb-96ea-1acfab7d9532.PNG)

장바구니 추가버튼을 눌렀을 때, 추가할지 물어보고 확인을 클릭하게 되면 상품이 추가되었다는 알림창이 나타납니다.
장바구니 버튼을 눌렀을 때, 장바구니 페이지로 이동합니다.

![슬라이드19](https://user-images.githubusercontent.com/73654909/124753201-a781f380-df63-11eb-98f9-d18af5cbcec7.PNG)

카트페이지에서는 장바구니 추가한 목록을 출력해주고, 장바구니의 총액과 선택적으로 삭제,전체삭제이 가능합니다.
주문하기 버튼을 누르면 주문페이지로 넘어가지만, 장바구니에 상품이 없을 시 주문페이지로 넘어가지 않습니다.

![슬라이드17](https://user-images.githubusercontent.com/73654909/120837520-c0346d80-c5a1-11eb-8aed-66575aff8065.PNG)

주문페이지에서는 현재 주문하고자 하는 상품의 목록을 출력해주고, 회원가입때 작성한 정보드를 배송주소의 `input` 값에 넣어주고 결제유형을 선택하고 동의에 체크후 결제하기 버튼을 누르면 결제완료페이지로 이동됩니다.

![슬라이드21](https://user-images.githubusercontent.com/73654909/124753291-c1bbd180-df63-11eb-9459-d616ab6c2c4f.PNG)

주문완료 페이지로 아이디와 주문상품이 간단하게 나오도록 만들었습니다.

#### 🍁 관리자 로그인

![슬라이드22](https://user-images.githubusercontent.com/73654909/124753354-d8622880-df63-11eb-9c9e-6ba30af6b7c3.PNG)

세션 아이디가 admin일때 들어올 수 있는 페이지입니다.
관리자 페이지에서는 상품,게시글,공지사항을 추가하거나 수정,삭제할 수 있습니다.

![슬라이드23](https://user-images.githubusercontent.com/73654909/124753456-f9c31480-df63-11eb-8c68-f118ab698c34.PNG)

상품 수정 페이지는 데이터베이스에서 상품정보를 불러와서 form에 채워줍니다.

![슬라이드24](https://user-images.githubusercontent.com/73654909/124753508-07789a00-df64-11eb-9d64-d8debce8cbfe.PNG)

공지사항 페이지입니다. 관리자페이지는 공지사항을 등록, 삭제, 공개를 할 수 있고 사용자 페이지는 열람만 가능합니다. 그리고 게시글을 제목,작성자를 기준으로 검색할 수 있습니다.

![슬라이드25](https://user-images.githubusercontent.com/73654909/124753622-2bd47680-df64-11eb-9c52-9960548ad657.PNG)

공지사항 등록 페이지입니다. 제목, 2개의 첨부파일과 내용을 입력할 수 있고 등록과 동시에 공지사항을 공개할 수 있도록 하는 체크박스가 있습니다.

![슬라이드26](https://user-images.githubusercontent.com/73654909/124753715-4c9ccc00-df64-11eb-9a48-da7576a63d6a.PNG)

공지사항 상세보기 페이지입니다. 이곳에서는 id가 admin일 경우 수정과 삭제가 가능하고, 삭제를 클릭시 한번더 확인하는 경고창이 뜹니다.

![슬라이드27](https://user-images.githubusercontent.com/73654909/124753815-6b02c780-df64-11eb-8fc8-5884ebf0aee7.PNG)

게시판 목록 페이지 입니다. 어드민일 경우 삭제할 게시글을 체크후 삭제와 글쓰기가 가능하고 일반 회원은 글쓰기와 검색이 가능합니다.

![슬라이드28](https://user-images.githubusercontent.com/73654909/124754005-a43b3780-df64-11eb-9808-e69c18f22de1.PNG)

게시글 등록페이지로 제목과 내용만을 입력받아 등록됩니다.

![슬라이드29](https://user-images.githubusercontent.com/73654909/124754067-bc12bb80-df64-11eb-8326-43ee408620aa.PNG)

게시글 상세보기 페이지로 접속한 아이디가 작성자이거나 admin일 경우 수정과 삭제 버튼이 나타나고 삭제시 한번더 확인하는 창을 표시합니다.

### 🌲 유효성 검사

![슬라이드20](https://user-images.githubusercontent.com/73654909/120837528-c1659a80-c5a1-11eb-8913-16c4f5cb64b3.PNG)

회원가입의 유효성검사입니다.

![슬라이드21](https://user-images.githubusercontent.com/73654909/120837531-c1659a80-c5a1-11eb-9547-df071127da91.PNG)

로그인의 유효성검사입니다.

![슬라이드22](https://user-images.githubusercontent.com/73654909/120837533-c1fe3100-c5a1-11eb-9514-caaa69d6dd44.PNG)

상품등록 페이지의 유효성검사 및 화면구성입니다.

끝까지 봐주셔서 감사합니다!