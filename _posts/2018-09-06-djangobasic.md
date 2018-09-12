---
layout: post
title:  "Django Basic"
subtitle:   "1"
categories: programming
tags: Web
comments: true
---



## 웹 프레임워크 Django 개념정리

### 목차

1. MVC, MFV
2. Django 개념
3. Project와 App
4. settings.py
5. manage.py



---



#### 1. MVC, MTV

- MVC (= MTV in Django) :

   = Model View Control (= Model Template View in Django)

- MVC 이전에는 다양한 코드가 한 곳에 들어가 있었기 때문에, 하나를 잘못 건드리면 시스템 전체가 문제가 됐었음. 

   -> 이후 코드를 `Model` `View` `Control` 로 분류. 



   ![출처: http://djangogo.tistory.com/](https://s3.ap-northeast-2.amazonaws.com/opentutorials-user-file/module/327/1262.png)


#### 2. Django 개념

![출처:http://www.stechstar.com/user/zbxe/index.php?mid=AlgorithmPython&document_srl=51162](http://www.stechstar.com/user/zbxe/files/attach/images/3263/162/051/3b71346c7532be7fe7630bdc36b29f30.png)



- User's Browser 의 다양한 액션 (ex. url 클릭, 데이터 입력 등 )들을 Url Dispatcher을 거쳐서 적합한 View로 연결이 됨.
- 초록색 부분이 우리가 실제로 다루게 되는 python 파일들이다.
  - wigs.py : 웹 서버와 장고를 적절히 결합시켜 줌
  -  views.py : DB에서 받아온 데이터를 적절히 가공시키는 것. 대부분의 코드를 여기서 작성하게 됨
  - models.py : 변수를 다루게 되면 manager가 DB sql 과 연결시켜줌.
  - example.html : script 파일
  - forms.py : 게시물 작성 폼 등

<br / >



#### 3. Project와 App

- 하나의 프로젝트 내에 다양한 앱이 존재.

- 프로젝트는 장고 Admin을 통해 쉽게 생성 가능함 (Admin : 장고 관리자 페이지)

  ~~~ django-admin startproject 프로젝트이름 ~~~
  django-admin startproject 프로젝트이름
  ~~~

- App 생성

  ~~~ ./managy.py startup 앱이름 ~~~
  ./managy.py startup 앱이름 ~~~
  ~~~

  <br />



#### 4. Setting.py

- 전체적인 프로젝트와 관련된 다양한 설정

  `debug` : 에러들을 확인 가능. default=True. (실제 배포시엔 False)

  `installed_apps` : pip로 설치한 app들. 다양하게 설치 가능.

  `midedleware_classes `: request와 reponse 사이에서 다양한 기능들을 레이어함.

  `templates` : 템플릿 관련 설정과 실제뷰 (html과 다양한 변수들)

  `databases` : DB에 관한 설정

  `static_url` : html과 관련된 정적 파일들을 다루는 파일

<br />



#### 5. Manage.py

- 프로젝트를 관리하기 위한 다양한 명령어 제공

  `startapp`: 앱 생성

  `runserver` : 서버실행

  `createsuperuser` : 관리자 생성

  `makemigrations app` : app의 모델 변경 사항 체크 

  `migrate` : 변경사항 DB에 반영

  `shell` : 쉘을 통해 데이터 확인 

  `collect static - static` : 파일을 한 곳에 모음.



<br / >

** 참고

8000포트 연결 - 외부 접근 불가능한 서버 연결

8080포트 연결 - 외부 접근 가능한 서버 연결



<br />

** 이미지출처

>  http://djangogo.tistory.com/entry/Djangogo-8-Django-%EB%A6%AC%EC%8A%A4%ED%8A%B8%EC%99%80-%EB%B7%B0-%EA%B5%AC%EC%B6%95%ED%95%98%EA%B8%B0
>
> http://www.stechstar.com/user/zbxe/index.php?mid=AlgorithmPython&document_srl=51162



