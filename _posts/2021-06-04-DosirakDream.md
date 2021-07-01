---
layout: single
title:  "도시락드림"
categories: Project
tags: 
  - [Project, DosirakDream]
toc: true
toc_sticky: true
---

> 도시락드림ppt 를 요약 정리한 페이지입니다.
> ppt는 [Github](https://github.com/ebambol/DosirakDream)에서 받으실 수 있습니다.

### 프로젝트 개요

#### 시니어 세대를 위한 도시락 배달 및 도움 서비스

상품의 주문도 받고 고령자의 안부를 확인하여 가족이 안심할 수 있는 도시락 제품을 판매하기 위한 플랫폼 개발하였습니다.

- 소스코드  [Github](https://github.com/ebambol/DosirakDream)


#### 개발환경

Java 1.8.0_171
Tomcat 9.0
Bootstrap 5.0 beta
MySQL 8.0.17

#### 사이트맵 구성

![siteMap](https://user-images.githubusercontent.com/73654909/120821478-742cfd00-c590-11eb-8550-d4cb5b4108e8.PNG)

#### 데이터베이스 구성

![DB](https://user-images.githubusercontent.com/73654909/120830516-88c1c300-c599-11eb-8b91-4627d8a79c3f.PNG)

#### product 상품 정보 관리

| 순번 | 칼럼  명 | 칼럼  설명   | 타입         | Null? | Key  | Default |
| ---- | -------- | ------------ | ------------ | ----- | ---- | ------- |
| 1    | pno      | 상품  코드   | varchar(10)  | NO    | PRI  | Null    |
| 2    | pname    | 상품  이름   | varchar(20)  | NO    |      | Null    |
| 3    | price    | 상품  가격   | integer      | NO    |      | Null    |
| 4    | info     | 상품  설명   | text         | NO    |      | Null    |
| 5    | category | 상품  분류   | varchar(10)  | NO    |      | Null    |
| 6    | filename | 상품  이미지 | varchar(100) | YES   |      | Null    |

#### jsp_member 회원정보

| 순번 | 칼럼  명 | 칼럼  설명     | 타입        | Null? | Key  | Default |
| ---- | -------- | -------------- | ----------- | ----- | ---- | ------- |
| 1    | id       | 회원  아이디   | varchar(50) | NO    | PRI  | Null    |
| 2    | password | 회원  비밀번호 | varchar(50) | NO    |      | Null    |
| 3    | username | 회원  이름     | varchar(20) | NO    |      | Null    |
| 4    | addr1    | 주소           | varchar(50) | NO    |      | Null    |
| 5    | addr2    | 상세주소       | varchar(30) | NO    |      | Null    |
| 6    | phone    | 휴대폰  번호   | varchar(20) | NO    |      | Null    |

#### cart 장바구니 정보

| 번   | 칼럼  명     | 칼럼  설명   | 타입        | Null? | Key  | Default |
| ---- | ------------ | ------------ | ----------- | ----- | ---- | ------- |
| 1    | product_num  | 상품 코드    | varchar(20) | NO    | PRI  | Null    |
| 2    | product_name | 상품  이름   | varchar(50) | NO    |      | Null    |
| 3    | userid       | 회원  아이디 | varchar(20) | NO    |      | Null    |
| 4    | price        | 가격         | integer     | NO    |      | Null    |

### 자바 코드 구성

```
📂src
├──📘controller				#컨트롤러
│	├──📘admin						#관리자 페이지
│	│	├──📘notice						#공지사항
│	│	│	├──📝DetailController			#공지사항 상세
│	│	│	├──📝ListController				#공지사항 리스트
│	│	│	└──📝RegController				#공지사항 글쓰기
│	│	└──📘product						#상품
│	│		├──📝AddController				#상품 추가
│	│		├──📝DeleteController			#상품 삭제
│	│		├──📝DetailController			#상품 상세
│	│		├──📝PageController				#상품 리스트
│	│		├──📝UpdateController			#상품 수정
│	│		└──📝UpdateProcessController			#상품 수정처리
│	├──📘cart						#카트
|	│	├──📝addCartController			#카트 추가
|	│	├──📝CartController				#카트 페이지
|	│	├──📝DeleteCart				#카트 전체 제거
|	│	└──📝RemoveCartController			#카트 선택 제거
│	├──📘member						#회원
|	│	├──📝SignInController			#로그인
|	│	└──📝SignUpController			#로그아웃
│	├──📘notice						#공지사항
|	│	├──📝DetailController			#상세
|	│	└──📝ListController				#리스트
│	├──📘order						#주문
|	│	├──📝OrderController			#주문페이지
|	│	└──📝OrderProcessController		#주문처리
│	└──📘product					#상품
|	|	└──📝ListController				#상품리스트
|	└──📝indexController			#홈페이지
├── 📘entity			#테이블
|	├──📝Cart				#카트 테이블
|	├──📝Member				#회원 테이블
|	├──📝Notice				#공지 테이블
|	├──📝NoticeView			#공지 뷰 테이블
|	└──📝Products			#상품 테이블
├── 📘service			#서비스
|	├──📝Cart				#카트 서비스
|	├──📝Member				#회원 서비스
|	├──📝Notice				#공지 서비스
|	├──📝NoticeView			#공지 뷰 서비스
|	└──📝Products			#상품 서비스
└──📘util				#유틸
	├──📝CharacterEncodingFilter  #인코딩 필터
	└──📝Member					#회원 서비스
```

#### view 구성

```
📂WebContent
├──📂parts
|	├──📝footer.jsp		#푸터페이지
|	└──📝header.jsp		#헤더페이지
├──📂resources		#커스텀 css,js
|	├──📂css
|	|	└──📄style.css
|	└──📂js
|		└──📄script.js
└──📂WEB-INF
	└──📂view
		├──📂admin			#관리자 페이지
		|	└──📂notice			#공지사항
		|		├──📄detail.jsp			#상세
		|		├──📄list.jsp			#목록
		|		└──📄reg.jsp			#글쓰기
		├──📂member				#회원 페이지
		|	├──📄signIn.jsp				#로그인
		|	├──📄signOut.jsp			#로그아웃
		|	├──📄signUp_success.jsp		#회원가입 성공
		|	└──📄signUp.jsp				#회원가입
		├──📂notice				#공지사항
		|	├──📄detail.jsp				#상세
		|	└──📄list.jsp				#목록
		└──📂product			#상품
			├──📄addDosirak.jsp			#추가
			├──📄cart.jsp				#카트페이지
			├──📄detail.jsp				#상품 상세
			├──📄edit.jsp				#상품 관리
			├──📄index.jsp				#홈페이지
			├──📄list.jsp				#상품 목록
			├──📄order_process.jsp		#주문 처리
			├──📄order.jsp				#주문
			└──📄update.jsp				#상품 수정
```

### 화면구성

#### 메인 페이지

![슬라이드11](https://user-images.githubusercontent.com/73654909/120837455-ae52ca80-c5a1-11eb-9b69-bf2ca498684c.PNG)

비로그인시 로그인과 회원가입 버튼이 나타나도록하고 홈페이지에서는 카테고리별로 3개의 상품을 출력해서 보여줍니다.

#### 비로그인

![슬라이드12](https://user-images.githubusercontent.com/73654909/120837505-bd397d00-c5a1-11eb-9fa5-86da62372ed5.PNG)

로그인과 회원가입 버튼을 클릭했을때 나오는 페이지입니다.

![슬라이드13](https://user-images.githubusercontent.com/73654909/120837512-be6aaa00-c5a1-11eb-9c18-0b1e2dd20232.PNG)

`div`태그에 `onclick`을 이용하여 상세페이지로 이동하도록 하였습니다.

![슬라이드14](https://user-images.githubusercontent.com/73654909/120837514-bf034080-c5a1-11eb-98d2-0be90a178134.PNG)

장바구니 추가와 장바구니는 비로그인시 사용이 불가하며 클릭시 로그인 페이지로 이동합니다.

#### 회원 로그인

![슬라이드15](https://user-images.githubusercontent.com/73654909/120837515-bf9bd700-c5a1-11eb-96ea-1acfab7d9532.PNG)

장바구니 추가버튼을 눌렀을 때, 추가할지 물어보고 확인을 클릭하게 되면 상품이 추가되었다는 알림창이 나타납니다.
장바구니 버튼을 눌렀을 때, 장바구니 페이지로 이동합니다.

![슬라이드16](https://user-images.githubusercontent.com/73654909/120837517-bf9bd700-c5a1-11eb-85c3-cc3b09936bb3.PNG)

카트페이지에서는 장바구니 추가한 목록을 출력해주고, 장바구니의 총액과 선택적으로 삭제,전체삭제이 가능합니다.
주문하기 버튼을 누르면 주문페이지로 넘어가지만, 장바구니에 상품이 없을 시 주문페이지로 넘어가지 않습니다.

![슬라이드17](https://user-images.githubusercontent.com/73654909/120837520-c0346d80-c5a1-11eb-8aed-66575aff8065.PNG)

주문페이지에서는 현재 주문하고자 하는 상품의 목록을 출력해주고, 회원가입때 작성한 정보드를 배송주소의 `input` 값에 넣어주고 결제유형을 선택하고 동의에 체크후 결제하기 버튼을 누르면 결제완료페이지로 이동됩니다.

#### 관리자 로그인

![슬라이드18](https://user-images.githubusercontent.com/73654909/120837522-c0346d80-c5a1-11eb-97cf-a8eecaeb57f5.PNG)

세션 아이디가 admin일때 들어올 수 있는 페이지입니다.
관리자 페이지에서는 상품 정보를 추가하거나 수정,삭제할 수 있습니다.

![슬라이드19](https://user-images.githubusercontent.com/73654909/120837525-c0cd0400-c5a1-11eb-8210-ed32655ab0a6.PNG)

상품 수정 페이지는 데이터베이스에서 상품정보를 불러와서 form에 채워줍니다.

### 유효성 검사

![슬라이드20](https://user-images.githubusercontent.com/73654909/120837528-c1659a80-c5a1-11eb-8913-16c4f5cb64b3.PNG)

회원가입의 유효성검사입니다.

![슬라이드21](https://user-images.githubusercontent.com/73654909/120837531-c1659a80-c5a1-11eb-9547-df071127da91.PNG)

로그인의 유효성검사입니다.

![슬라이드22](https://user-images.githubusercontent.com/73654909/120837533-c1fe3100-c5a1-11eb-9514-caaa69d6dd44.PNG)

상품등록 페이지의 유효성검사 및 화면구성입니다.