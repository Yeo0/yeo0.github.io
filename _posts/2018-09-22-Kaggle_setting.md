---
layout: post
title:  "Kaggle_setting"
subtitle:   "2"
categories: study
tags: kaggle
comments: true





---



### 캐글 개발환경 따라하기

---

<br/>

#### 개발환경 준비

 파이썬이 설치되어있다는 가정하에 다음과 같이 진행한다 (리눅스, 맥 기준)

<br/>

##### 1. pip 설치

```python
python3 -m pip install --user --upgrade pip 
```

<br/>**2. virtualenv 설치 (라이브러리 버전관리)**

```python
python3 -m pip install --user virtualenv
```

<br/>

**3. 프로젝트를 위한 "kaggle_venv"라는 가상환경 생성**

```python
python3 -m virtualenv kaggle_env
```

<br/>

**4. 가상환경 활성화**

```python
source kaggle_venv/bin/activate
```

<br/>

가상환경이 활성화되면, terminal 좌측에 (kaggle_venv)라는 괄호가 추가된다. 

가상환경을 활성화 한 후 라이브러리를 설치하면, **kaggle_venv내에서만 해당 버전의 라이브러리가 설치**되어 시스템 기존 라이브러리 및 다른 가상환경의 라이브러리 버전과 충돌이 나지 않는다.

