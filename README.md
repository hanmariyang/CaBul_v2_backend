# CaBul_v2 (유화제작 서비스)

## 프로젝트

<img width="443" alt="logo" src="https://user-images.githubusercontent.com/111295065/210082342-b748b547-6540-4f0f-9653-23f2e3ba91cf.png">


### CaBul_v2

시연 영상 :

[https://youtu.be/yDjeBdIAzjU/](https://youtu.be/yDjeBdIAzjU/)

프로젝트 일정 : 2022.11.22 ~ 2022.11.28

프론트엔드 Repository : [https://github.com/devjunseok/CaBul_v2_frontend](https://github.com/devjunseok/CaBul_v2_frontend)

백엔드  Repository :[https://github.com/devjunseok/CaBul_v2_backend](https://github.com/devjunseok/CaBul_v2_backend)

S.A 링크 : [B-1팀 유화제작서비스](https://iodized-justice-c7c.notion.site/B1-ed15c9156d7949faa389b0835662ab0a)

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

팀원 / 프로젝트 기획 / user기능 / API연결을 위한 각종 조회 로직 작성 / 이메일 인증 기능 / 팔로우 기능 작성 / user기능 관련 프론트 api 연결 /좋아요 기능 추가

### 성창남 - [SungChangNam - Overview](https://github.com/SungChangNam)

팀원 / 댓글 CRUD

### 양기철 - [hanmariyang - Overview](https://github.com/hanmariyang)

팀원 / 프로젝트 기획 / articles 기능 / DB 모델링 / 머신러닝, 딥러닝 코드 작성 / 프론트엔드 템플릿 제작 및 API 연결

### 이태겸 - [poro625 - Overview](https://github.com/poro625)

팀원 / 게시글 좋아요 기능 구축 / 검색 기능 구축
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

**문제 : 게시글 작성시 이미지를 유화 처리하면서 이미지 저장시 변환된 이미지를 저장 위치를 지정해주는 방식에서 에러가 발생 하였다.**

**해결 : 변환된 이미지를 저장할시 .save(“저장위치“, “파일포맷“) 으로 설정하여 변환된 이미지를 저장하여 해결 하였다.**
### 노우석

**문제 : 프로필을 조회하는 serializer 안에 나를 팔로우 하는 사람에 대한 필드 정보를 담아야 했는데 안됨**

**해결 : StringRelatedField로 지정해놨던 필드값이 제대로 출력되지 않아서 필드값을 SlugRelatedField로 바꿔주어서 제대로 팔로우 한 사람의 정보가 나오게 만들어서 해결**

### 이태겸

**문제 : 게시글 관련된 댓글을 보기 위해 serializer안에 serializer 역참조를 이용 작업시  인스턴스 키가 어떤 속성과도 일치하지 않은 오류가 발생**

**해결 :source = "comment_set을 넣어주면서 인스턴스 값과 속성값을 일치시켜 해결**

### 성창남

**댓글기능을 구현 할 때 게시글 정보를 받을 때 필요없는 부분도 같이 받아져 Serializer 기능을 활용하여 해결**


## 5. 와이어프레임

[https://www.figma.com/file/hgtTToRaWbfP87GfNvHaMa/Off_the_Outfit?node-id=0%3A1&t=xw7FNe87Jr8IecaC-1](https://www.figma.com/file/hgtTToRaWbfP87GfNvHaMa/Off_the_Outfit?node-id=0%3A1&t=xw7FNe87Jr8IecaC-1)

![https://user-images.githubusercontent.com/111295065/207312359-91bb78a9-c108-4897-8cc3-e0cbb1f00cd0.png](https://user-images.githubusercontent.com/111295065/207312359-91bb78a9-c108-4897-8cc3-e0cbb1f00cd0.png)

## 6. API 명세서

[off_the_outfit (getpostman.com)](https://documenter.getpostman.com/view/24913558/2s8YzWRfo4)

## 7. DB 설계 ERD

![https://user-images.githubusercontent.com/111295065/207309475-759e6e8d-8265-4c49-8c8f-9f83478c329d.png](https://user-images.githubusercontent.com/111295065/207309475-759e6e8d-8265-4c49-8c8f-9f83478c329d.png)
