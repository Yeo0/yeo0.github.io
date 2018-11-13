---
layout: post
title:  "정리 _ BeautifulSoup Find_All"
subtitle:   "6"
categories: data
tags: crawling
comments: true





---



### Find() 정리



<br/>

##### 1. find함수 종류

`find()` `find_next()` `find_all()` 

<br/>

##### 2. find 함수 쓰기 전 확인할 것 

```python
#존재할 때만 가져오기
if soup.find("div". title=True) is not None:
    i=soup.find("div",title=True)
    
```

<br/>

##### 3. 모든 a 태그 검색

```python
soup.find_all("a")
soup("a")
```

<br/>

##### 4. string 검색

```python
soup.find_all(string="Elsie") # string 이 Elsie 인 것 찾기
soup.find_all(string=["Tillie", "Elsie", "Lacie"]) # or 검색
soup.find_all(string=re.compile("Dormouse")) # 정규식 이용
```

<br/>

##### 5. string 이 있는 title 태그 모두 검색

```python
soup.title.find_all(string=True)
soup.title(string=True)
```

<br/>

##### 6. p 태그와 속성 값이 title 이 있는 것 찾기

```python
soup.find_all("p","title") #ex) <p class="title"></p>
```

<br/>

##### 7. a 태그를 두개만 가져옴

```python
soup.find_all("a",limit=2)
```

<br/>

##### 8. p 태그와 속성 값이 title 이 있는 것 찾기

```python
soup.find_all("p","title") #ex) <p class="title"></p>
```

<br/>

##### 9. a태그와 b태그 찾기

```python
soup.find_all(["a","b"])

```

<br/>

##### 10. 태그명 가져오기

```python
soup.find("div").name
```

<br/>

##### 11. 태그 삭제

```python
a_tag.img.wrap()
```

<br/>

##### 12. 태그 추가

```python
soup.p.string.wrap(soup.new_tag("b"))
soup.p.wrap(soup.new_tag("div")
```

<br/>

##### 13. string을 다른 string으로 교체하기

```python
tag.string.replace_with("새로운 값")
```

<br/>

##### 14. 보기 좋게 출력하기

```python
soup.b.prettify()
```

<br/>

##### 15. 속성 값 가져오기

```python
soup.p['class']
soup.p['id']
```

<br/>

##### 16. 간단한 검색하기

```python
soup.body.b # body태그 아래의 첫번째 b태그
soup.a # 첫번째 a태그
```

<br/>

##### 17. 속성 값 모두 출력

```python
tag.attrs
```

<br/>

##### 18. 속성이 있는지 확인하기

```python
tag.has_attr('class')
tag.has_
```

<br/>

##### 19. 속성 가져오기

```python
soup.find("div")['class'] #속성 값이 없으면 error
soup.find("div").get('class') #속성 값이 없으면 None 반환
```

<br/>

##### 20.  data-로 시작하는 속성을 찾을 때

```python
soup.find("div", attrs={"data-value":True})
```

<br/>

##### 21. class를 검색할 땐 class_로 쓴다

```python
soup.find_all("a", class_="sister")
```

