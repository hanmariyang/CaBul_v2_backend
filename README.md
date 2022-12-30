# CaBul_v2 (유화제작 서비스)

## 프로젝트

<img width="443" alt="logo" src="https://user-images.githubusercontent.com/111295065/210082342-b748b547-6540-4f0f-9653-23f2e3ba91cf.png">


### CaBul_v2

시연 영상 :

[https://youtu.be/yDjeBdIAzjU/](https://youtu.be/yDjeBdIAzjU/)

프로젝트 일정 : 2022.11.22 ~ 2022.11.28

프론트엔드 Repository : [https://github.com/devjunseok/CaBul_v2_frontend](https://github.com/devjunseok/CaBul_v2_frontend)

백엔드  Repository :[https://github.com/devjunseok/CaBul_v2_backend](https://github.com/devjunseok/CaBul_v2_backend)

S.A 링크 : [B1팀 최종 프로젝트](https://iodized-justice-c7c.notion.site/B1-ed15c9156d7949faa389b0835662ab0a)

## 1. 프로젝트 주제

### 사물인식을 활용한 이미지 자동 분류 및 유화제작 서비스

자신의 사진을 유화로 제작해보고, 다른 사용자들과 소통하는 커뮤니티 사이트

## 2. 기술 스택

- 백엔드
    - Python 3.10
    - Django 4.1.4
    - Django Rest Framework 3.14
    - Django Rest Framework simple-jwt 5.2.2
    - PyTorch 1.13.0
- 프론트엔드
    - HTML5
    - Javascript
    - JQuery
    - CSS

## 3. 싸지방 팀 팀원 및 역할

### 박준석 - [devjunseok - Overview](https://github.com/devjunseok)

팀장 / 프로젝트 기획 / 테스트 코드 작성 / user 기능/ DB 모델링 / 머신러닝, 딥러닝 코드 작성

### 노우석 - [WooSeok-Nho - Overview](https://github.com/WooSeok-Nho/)

팀원 / 프로젝트 기획 / user기능 / 날씨추천기능 / 포인트적립기능 / FrontEnd 제작,API연결

### 성창남 - [SungChangNam - Overview](https://github.com/SungChangNam)

팀원 / 프로젝트 기획 / communities 기능/ DB 모델링 / FrontEnd 제작,API연결

### 양기철 - [hanmariyang - Overview](https://github.com/hanmariyang)

팀원 / 프로젝트 기획 / products, recommend 기능 / 상품정보 크롤링 / DB모델링 / 추천 서비스 기능 / FrontEnd 템플릿 제작 및 API연결

### 이태겸 - [poro625 - Overview](https://github.com/poro625)

팀원 / 프로젝트 기획 / communites 기능, products 기능, weather 기능/크롤링/ DB 모델링 /태그 기능/ 검색 기능/상세보기 수정 및 삭제

## 4. 프로젝트 기능

### User 기능(회원가입/로그인 - simple jwt 사용)

- dj-rest-auth 이용 회원가입, 로그인 기능 구현 (이메일 인증 포함)
- extra_kwargs 처리로 에러 메세지 세분화 처리
- 마지막 로그인 365일 경과된 아이디 삭제 기능
- 팔로우, 팔로워

### articles 기능 (게시글, 댓글, 사물인식, 유화제작)

- 게시글 CRUD 기능
- 게시글, 유저 검색 기능
- 업로드 이미지 사물인식 및 카테고리 자동 분류 기능(Pytorch 사용)
- 업로드 이미지 유화풍 이미지로 제작(딥러닝 모델 사용)

 
## 4-1. 트러블 슈팅

### 박준석

**문제 : 업로드한 사진을 유화처리한 후 저장될 때, 원본 이미지와 파일 이름이 겹쳐서 저장이 안되는 현상 발생**

**원인 : 처음에 모델링을 할 때, 유화처리된 이미지를 저장할 필드를 따로 선언해두지 않아 발생한 문제**

**해결 : models.py에 rename_imagefile_to_uuid 함수를 작성, uuid 사용하여 파일 이름을 난수처리 하여 파일 이름이 같은 사진이어도 겹치지 않게 처리** 

**참조: [https://hangjastar.tistory.com/202](https://hangjastar.tistory.com/202)**

### 양기철

**문제 : Serializer를 사용하지않고 ManyToMany 필드를 사용하는 대량 DB 저장시 각 필드끼리 연결되지 않는 문제 발생**

**원인 : 크롤링한 외부 데이터를 가져와서 DB에 저장시키려다보니 각각 알맞는 필드를 연결시키지 못함**

**해결 : ManyToMany 필드에 맞는 로직으로 저장하여 해결**
### 노우석

**문제 : 출석버튼을 눌렀을 때 db에 저장되어 있는 point가 증가하게 설계해놓았다.**

**다만 코드 로직 자체를 하루에 한번 포인트가 증가하게 할 수 있게 datetime.today()와 버튼을 클릭했을 때의 현재 날짜를 저장하는 click_time의 값을 비교해서 값이 같으면 기능이 작동하지 않게 작성해놓았는데 제대로 작동하지 않는 상황 발생**

**해결 : 두개의 값이 완전히 같게 보여도 타입이 달랐기 때문에 타입을 모델에서 변경해주어 같게 만들어주었더니 해결.**

### 이태겸

**문제 : 태그 기능을 게시글에 작성 시 여러개를 저장하더라도 각각 DB에 저장이 되도록 해야 하는데 각각 저장이 되지 않는 상황 발생**

**원인 : 원인은 Serializer 사용 시 ManyToMany 관계를 의식하지 않고 태그 기능을 구현하였기 때문에 생긴 현상.**

**해결 :ManyToMany 관계 Serializer를 사용하여 기존 Serializer를 수정 보완하여서 해결**

### 성창남

**문제 : 연동 하여 관리자가 신고 게시글 삭제 기능 구현 할 때 백엔드 정보가 프로트엔드에 구현되지 않은 오류가 발생 하는 문제가 발생. 처음에는 await fetch 만 사용 하여 원치않는 정보도 같이 들어와서 오류 발생.**

**해결 : 이중 반복문 을 활용하여 해결.**


## 5. 와이어프레임

[https://www.figma.com/file/hgtTToRaWbfP87GfNvHaMa/Off_the_Outfit?node-id=0%3A1&t=xw7FNe87Jr8IecaC-1](https://www.figma.com/file/hgtTToRaWbfP87GfNvHaMa/Off_the_Outfit?node-id=0%3A1&t=xw7FNe87Jr8IecaC-1)

![https://user-images.githubusercontent.com/111295065/207312359-91bb78a9-c108-4897-8cc3-e0cbb1f00cd0.png](https://user-images.githubusercontent.com/111295065/207312359-91bb78a9-c108-4897-8cc3-e0cbb1f00cd0.png)

## 6. API 명세서

[off_the_outfit (getpostman.com)](https://documenter.getpostman.com/view/24913558/2s8YzWRfo4)

## 7. DB 설계 ERD

![https://user-images.githubusercontent.com/111295065/207309475-759e6e8d-8265-4c49-8c8f-9f83478c329d.png](https://user-images.githubusercontent.com/111295065/207309475-759e6e8d-8265-4c49-8c8f-9f83478c329d.png)
