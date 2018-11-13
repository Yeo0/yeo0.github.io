---
layout: post
title:  "맥(Mac)에서 우분투(Ubuntu) 부팅usb 만들기"
subtitle:   "1"
categories: com
tags: os
comments: true

---

<br/>

- 처음 실행 시 usb를 꽂지 않고 진행합니다.

<br/>

### 1. Ubuntu Download

**http://mirror.kakao.com/ubuntu-releases/bionic/**

- 위의 링크는 우분투 18.04 lts 를 다운받는 링크입니다.
- 원하는 버전, desktop 나 server 의 .iso 파일을 다운 받아야 합니다.

<br/>

### 2. Iso -> Img

- 부팅디스크 작업시 img파일로 진행되기 때문에 확장자 변환이 필요합니다.
- *hdiutil convert -format UDRW -o [변환할 img 경로, 파일명] \[다운받은 iso 파일 경로, 파일명]*
- 저의 경우 download 폴더에 파일이 있어 다음과 같이 사용했습니다.

```
$ hdiutil convert -format UDRW -o ~/Downloads/ubuntu-18.04.1-desktop-amd64.img ~/Downloads/ubuntu-18.04.1-desktop-amd64.iso
```

- 실행 후 .img.dmg파일로 저장이 되는데, .dmg를 삭제해 .img파일로 만들어 줍니다.

  ![img](/assets/img/dmg to img.png)

<br/>

### 3. Disk number 확인

- diskutil list 명령어로 현재 연결된 디바이스 장치들을 확인합니다.

  ```
  $ diskutil list
  ```

- 이후 부팅디스크를 만들 usb를 삽입 후 다시한번 dksiutil list를 통해 추가된 디스크를 확인합니다.

  ```
  $ diskutil list
  ```

- 이전과 비교해 추가된 디스크의 디스크 넘버를 확인합니다. (그게 usb의 disk number)

<br/>

### 4. 부팅USB 제작

- USB의 마운트를 해제합니다. (해제하지 않으면 사용중이라고 떠 설치할 수 없습니다.)
- diskutil unmountDisk /dev/disk숫자
- 저의 경우 disk5라 다음과 같이 사용했습니다.

```
$ diskutil unmountDisk /dev/disk5
```

- unmount를 완료한 후 아래의 명령어를 사용해 설치합니다.
- *sudo dd if=[4번 작업으로 변환된 img파일의 경로] of=[7번 작업을 통해 알게된 USB disk ] bs=1m*
- 저의 경우 다음과 같이 사용했습니다.

```
$ sudo dd if=~/Downloads/ubuntu-16.04.1-desktop-amd64.img of=/dev/disk5 bs=1m
```

<br/>

- 저의 경우 계속 'No such file or directory'라는 에러가 떴는데, 이거는 맥 상의 오류로 판단되므로 다시 껐다 키고 진행하여 해결할 수 있습니다.
- 위의 USB를 설치하려는 컴퓨터에 꽂아 진행하면 됩니다. (제 컴퓨터의 경우 F2를 눌러 메인보드 관리 페이지에서 부팅 USB를 1순위로 옮겨 설치를 진행할 수 있었습니다.)

<br/>

---

## 부팅 USB 다시 사용하기

- USB포맷을 진행해야 원래 USB로 사용할 수 있습니다.

<br/>

### 1. Disk number 확인

- 디스크 설치할 때의 방식과 동일합니다. 
- 현재 USB의 disk number를 아래의 명령어로 확인합니다.

```
$ disktutil list
```

<br/>

### 2. USB 포맷

- *diskutil eraseDisk [파일 포맷] \[포맷 후 disk 이름] \[/dev/disk숫자]*
- 파일 포맷에는 아래와 같은 형식을 사용할 수 있습니다.
  - **JHFS+** : Mac OS Extended Journaled (JHFS+)
  - **HFS+** : Mac OS Extended (HFS+)
  - **FAT32** : MS-DOS FAT32
  - **ExFAT** : ExFAT
- ExFAT의 경우 ubuntu에서 사용이 안되길래 (따로 소프트웨어 설치가 필요하다고 알고 있습니다.) 속도는 느리지만 FAT32로 진행하였습니다.

```
$ diskutil eraseDisk FAT32 SANDISK /dev/disk5
```



