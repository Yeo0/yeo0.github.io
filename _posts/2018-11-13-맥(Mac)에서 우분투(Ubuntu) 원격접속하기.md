---
layout: post
title:  "맥(Mac)에서 우분투(Ubuntu) 원격접속하기"
subtitle:   "2"
categories: com
tags: os
comments: true


---



## 맥(Mac)에서 우분투(Ubuntu) 원격접속

- 환경은 우분투 18.04 lts 입니다. (정리된 정보가 많이 없어 애를 먹었습니다.)
- VNC viewer를 통해 접속하는 방법을 정리해보려 합니다.
- VNC는 로컬 시스템에 사용자가 로그인 되어있을 때 같은 화면을 보면서 PC를 제어하게 됩니다.
- Xrdp 원격접속은 다음에 따로 포스팅할 예정입니다:)

<br/>

### 1. Ubuntu 환경 설정

- `Setting` - `Sharing` 에 들어가 **ON** 상태로 만들어 줍니다. 
- Screen Sharing 도 **Active** 상태로 만들어 줍니다.
- 비밀번호를 설정하고 Wired connection1 상태도 **ON** 으로 만듭니다.

![img](/assets/img/ubuntu_vnc.png)



<br/>

### 2. 설치

- VNC viewer를 이용하기 위한 설치파일입니다.
- 다른 운영체제의 접속을 암호화하였기 때문에 이것을 풀어주는 과정이 필요합니다.

```
$ sudo apt install dconf-editor
$ dconf write /org/gnome/desktop/remote-access/require-encryption false
```

<br/>

### 3. VNC Viewer 이용

- 먼저 현재 PC의 IP주소를 확인한다.

```
$ hostname -I
```

<br/>

- VNC 뷰어는 PC용  [크롬 VNC 뷰어](https://chrome.google.com/webstore/detail/vnc%C2%AE-viewer-for-google-ch/iabmpiboiopbgfabjmgeedhcmjenhbla) , [RealVNC 뷰어](https://www.realvnc.com/download/viewer/) , 안드로이드용 [VNC Viewer](https://play.google.com/store/apps/details?id=com.realvnc.viewer.android&hl=ko) 등 다양하다. 

- 이 중 제일 간편한 크롬 VNC뷰어를 사용해보려한다.

- 위의 링크를 들어가 `앱 실행` 버튼을 누르면 아래와 같은 화면을 볼 수 있다.

  ![img](/assets/img/chrome_vnc.png)

- 위에서 확인한 IP주소를 입력하고 Connect 버튼을 누른 후 처음에 설정한 passward를 입력하면 접속이 완료된다.