---
layout: post
title:  "Scraping with BeautifulSoup"
subtitle:   "3"
categories: study
tags: crawling
comments: true



---



## 파이썬을 이용한 머신러닝, 딥러닝 실전개발 입문

### 1. 크롤링과 스크레이핑

<br/>

#### 1-2. BeautifulSoup으로 스크레이핑하기

##### - BeautifulSoup : HTML과 XML을 분석해주는 라이브러리

<br/>

  - BeautifulSoup 기본 사용법	

    ```python
    from bs4 import BeautifulSoup
    
    #분석하고 싶은 HTML
    html="""
    <html><body>
    	<h1>스크레이핑이란?</h1>
    	<p>웹페이지를 분석하는것</p>
    	<p>원하는 부분을 추출하는 것</p>
    </body></html>
    """
    
    #HTML 분석하기
    soup=BeautifulSoup(html,'html.parser') #BeautifulSoup(html, parser종류)
    
    #원하는 부분 추출하기
    h1=soup.html.body.h1 #html.body.h1에 있는 요소에 접근
    p1=soup.html.body.p
    p2=p1.next_sibling.next_sibling #두번째 p태그 접근/ next_sibling 1번할 경우 줄바꿈 뒤에있는 공백이 추출됨
    
    #요소의 글자 출력하기
    print("h1=",h1.string) #글자부분 추출
    print("p=",p1.string)
    print("p=",p2.string)
    
    ```

<br/>

  - id로 요소를 찾는 법

    - find() 메소드

    ```python
    from bs4 import BeautifulSoup
    
    html="""
    <html><body>
    	<h1 id="title">스크레이핑이란?</h1>
    	<p id="body">웹페이지를 분석하는것</p>
    	<p>원하는 부분을 추출하는 것</p>
    </body></html>
    """
    
    #html 분석하기
    soup=BeautifulSoup(html, 'html.parser')
    
    #find()메소드로 원하는 부분 추출
    title=soup.find(id='title')
    body=soup.find(id="body")
    
    #텍스트 부분 출력
    print("#title=",title.string)
    print("#body=", body.string)
    ```

<br/>

    - find_all() 메소드
    
      ```python
      #여러개의 요소 추출하기
      from bs4 import BeautifulSoup
      
      html="""
      <html><body>
        <ul>
          <li><a href="http://www.naver.com">naver</a></li>
          <li><a href="http://www.daum.net"daum</a></li>
        </ul>
      </body></html>
      """
      #html 분석하기
      soup=BeautifulSoup(html, 'html.parser')
      
      #find_all 메소드로 추출
      links=soup.find_all("a")
      
      #링크 목록 출력하기
      for a in links:
          href=a.attrs['href'] #attrs속성에서 추출
          text=a.string
          print(text,'=',href)
      ```

<br/>

  - DOM ( Document Object Model) : XML or HTML의 요소에 접근하는 구조 

    - ex) <a>태그 - href 속성 등 

    - *.string* : 내부의 글자 추출 / .attrs["title"] : 내부 속성 추출

      ```python
      #DOM요소 속성
      from bs4 import BeautifulSoup
      soup=BeautifulSoup(
          "<p><a href='a.html'>test</a></p>", "html.parser")
      
      #결과 확인
      soup.prettify() #'<p>\n <a href="a.html">\n  test\n </a>\n</p>'
      
      #<a>태그를 a 변수에 할당
      a=soup.p.a
      
      #attrs 속성의 자료형 확인
      type(a.attrs) #dict
      
      #href 속성이 있는지 확인
      'href' in a.attrs # true
      
      #href 속성값 확인
      a['href'] #a.html
      ```

    <br/>

  - urlopen() + BeautifulSoup

    - urlopen()을 이용해 `html` 파일을 불러오고 `BeautifulSoup`를 이용해 분석

    ```python
    from bs4 import BeautifulSoup
    import urllib.request as req
    
    url="http://www.kma.go.kr/weather/forecast/mid-term-rss3.jsp"
    
    #urlopen()으로 데이터 가져오기
    res=req.urlopen(url)
    
    #BeautifulSoup으로 분석하기
    soup=BeautifulSoup(res,'html.parser')
    
    #원하는 데이터 추출
    title=soup.find("title").string
    wf=soup.find("wf").string
    print(title)
    print(wf)
    ```

    <br/>

  - CSS 선택자 사용하기 

    - soup.select_one(<선택자>)  -> 요소 -> 그냥 사용 가능

    - soup.select(<선택자>) -> 요소의 배열 -> **반복문**으로 사용

      ```python
      #<h1> , <li> 태그 추출
      from bs4 import BeautifulSoup
      
      #분석대상 HTML
      html="""
      <html><body>
      <div id="meigen">
        <h1>위키북스 도서</h1>
        <ul class="items">
          <li>유니티 게임 이펙트 입문</li>
          <li>스위프트로 시작하는 아이폰 앱 개발 교과서</li>
          <li>모던 웹사이트 디자인의 정석</li>
        </ul>
      </div>
      </body></html>
      """
      
      #HTML 분석하기
      soup=BeautifulSoup(html,'html.parser')
      
      #필요한 부분을 CSS 쿼리로 추출하기
      #타이틀 부분 추출하기
      h1=soup.select_one("div#meigen > h1").string #하위로 갈때 > 사용
      print("h1=",h1)
      
      #목록부분 추출하기
      li_list=soup.select("div#meigen > ul.items > li")
      for li in li_list:
          print("li=",li.string)
      ```

      <br/>

      <br/>

    - CSS 선택자 자세히 알아보기

      1. <u>태그선택자 ( 요소선택자 )</u> : 특정이름, 태그 선택

         ex) "ul", "div", "li" 등

         <br/>

      2. <u>id 선택자</u> : id 선택 <id = "">
    
         ex) "#meigen", "#content" 등
    
         - html에서 id는 구분하는 식별자 역할. (유일함)

<br/>

      3. <u>클래스 선택자</u> : 클래스 이름 선택
    
         ex) ".items"
    
         - 만약 class="items books shoes" 라면 
    
           - ".items", ".books",".shoes" 다 사용할 수 있다.
    
           - 이들을 한번에 다 사용하고 싶다면 .을 이용해 공백없이 연결함
    
             ".items.books.shoes"

<br/>

      4. <u>구조 선택자</u>
    
         - 후손 선택자 : 어떤 태그 아래있는 모든 속성들. 띄어쓰기로 구분한다.
    
           - ex) 위의 예시에서 html태그의 후손 선택자는 html 하위에 있는 모든 것 - body div h1 ul li
           - ex) "#meigen li" : meigen 의 후손들 중 li태그만
    
         - 자식 선택자 : 어떤 태그 바로 아래에 있는 속성. > 로 나타낸다.
    
           - ex) 위의 예시에서 html태그의 자식 선택자는 html 바로 밑의 body
           - ex) "ul.items > li" : ul의 items 태그의 자식 중 li태그

<br/>

<br/>

    - ==따라서 선택할 때==
    
      ==1) 내가 가져올 태그의 갯수가 몇 개인지 판단하기==
    
      ==2) select one 인지 select 인지 구분하기==
    
      ==3) 어떤 선택자를 사용해야할지 판단하기==
    
      ​	ex) *soup.select("li")* 도 되지만 *soup.select("ul.items > li")* 가 더 명확
    
      ​	ex) *soup.select_one("hi")* 도 되지만 *soup.select("body > div> h1")* 가 더 명확
    
      ==4) 추출 후 원하는대로 사용한다.==

<br/>

<br/>

- 종합하여 제일 기본적인 크롤링을 해보기

  ex) 네이버 환율 페이지에서 미국 환율 가져오기

  ```python
  #네이버 금융에서 환율정보 추출
  from bs4 import BeautifulSoup
  import urllib.request as req
  
  #HTML 가져오기
  url="http://info.finance.naver.com/marketindex/"
  res=req.urlopen(url)
  
  #HTML 분석하기
  soup=BeautifulSoup(res, 'html.parser')
  
  #원하는 데이터 추출하기
  price=soup.select_one('div.head_info > span.value').string
  print("usd/krw=",price)
  
  ```
