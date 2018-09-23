---
layout: post
title:  "Data download"
subtitle:   "2"
categories: study
tags: crawling
comments: true


---



## 파이썬을 이용한 머신러닝, 딥러닝 실전개발 입문

##### link : [*github*](https://github.com/Yeo0/Study/blob/master/Web%20Crawling/1-1.%20%EB%8D%B0%EC%9D%B4%ED%84%B0%20%EB%8B%A4%EC%9A%B4%EB%A1%9C%EB%93%9C.ipynb)

<br/>

### 1. 크롤링과 스크레이핑

<br/>

#### 1-1. 데이터 다운로드

- urllib 라이브러리 사용 - url을 다루는 모듈을 모아놓은 패키지

  - urllib.request  : 웹 사이트에 있는 데이터에 접근하는 기능

<br/>

    - urlretrieve(url, savename) : 파일 직접 다운로드
    
       ex)  웹 상의 png파일 저장
    
      ```python
      import urllib.request
      
      #URL과 저장경로 저장하기
      url="http://uta.pw/shodou/img/28/214.png"
      savename="test.png"
      
      #다운로드
      urllib.request.urlretrieve(url,savename)
      print("저장되었습니다")
      ```

<br/>

    - urlopen() :
    
      ex) 웹 상의 png 파일 저장
    
      ```python
      import urllib.request
      
      #URL과 저장경로 저장하기
      url="http://uta.pw/shodou/img/28/214.png"
      savename="test1.png"
      
      #다운로드
      mem=urllib.request.urlopen(url).read()
      
      #파일로 저장하기
      with open(savename, mode="wb") as f:
          f.write(mem)
          print("저장되었습니다")
      ```
    
    		
    
    - 클라이언트 접속 정보 출력 - IP확인
    
      - decode('utf-8') or ('euc-kr') : 바이너리 데이터를 문자열로 변환
    
        ex) IP확인 API로 접근해서 결과 추출
    
        ```python
        import urllib.request
        
        #데이터 읽어오기
        url="http://api.aoikujira.com/ip/ini"
        res=urllib.request.urlopen(url)
        data=res.read()
        
        #바이너리를 문자열로 변환하기
        text=data.decode('utf-8') #text를 열면 알 수 없는 문자들임
        print(text)
        ```
    
    - 매개변수를 추가해 요청을 전송하는 방법
    
      - 웹 요청의 기본 
    
        https://search.naver.com/search.naver?where=nexearch&query=%ED%99%A9%ED%9D%AC%EC%B0%AC+%EA%B3%A8&sm=top_lve&ie=utf8 라는 주소가 있을 때
    
        - 방식 : GET (urllib.request 쓸 때는 주로 get방식)
        - 대상 : search.naver.com = 호스트이름
        - 추가적인 정보 
          - 경로 : /search.naver
          - 데이터 :?키=값&키=값&... 로 쭉 이어져 있음 
            :?where=nexearch
            &query=%ED%99%A9%ED%9D%AC%EC%B0%AC+%EA%B3%A8 (decoding ->황희찬 + 골)
            &sm=top_lve
            &ie=utf8
    
    ```python 
    import urllib.request
    import urllib.parse
    
    API="https://search.naver.com/search.naver"
    
    #매개변수를 URL 인코딩
    values={
        "where":"nexearch",
        "sm":"top-hty",
        "fbm":"1",
        "ie":"utf8",
        "query":"초콜릿",
    }
        
    params=urllib.parse.urlencode(values)
    
    #요청전용 URL 생성
    url=API+"?"+params
    print("url=",url)
    
    #다운로드
    data=urllib.request.urlopen(url).read()
    text=data.decode('utf-8')
    print(text)
    ```

<br/>

    - 매개변수를 명령줄에서 지정하기
    
      ```python
      import sys
      import urllib.request as req
      import urllib.parse as parse
      
      #명령줄 매개변수 추출
      if len(sys.argv)<=1:
          print("USAGE: download-forecast-argv <Region Number>")
          sys.exit()
      regionNumber=sys.argv[1]
      
      #매개변수를 URL 인코딩
      API="http://www.kma.go.kr/weather/forecast/mid-term-rss3.jsp"
      values={
          'stnId':regionNumber
      }
      params=parse.urlencode(values)
      url=API+"?"+params
      print("url=",url)
      
      #다운로드
      data=req.urlopen(url).read()
      text=data.decode('utf-8')
      print(text)
      ```

