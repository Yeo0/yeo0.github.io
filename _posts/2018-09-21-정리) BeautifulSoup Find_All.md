---
layout: post
title:  "정리 _ BeautifulSoup Find_All"
subtitle:   "6"
categories: study
tags: crawling
comments: true





---





##### 1. find함수 종류

`find()` `find_next()` `find_all()` 



##### 2. find 함수 쓰기 전 확인할 것 

```python
#존재할 때만 가져오기
if soup.find("div". title=True) is not None:
    i=soup.find("div",title=True)
    
```



##### 3. 모든 a 태그 검색

```python
soup.find_all("a")
soup("a")
```



##### 4. string 검색

```python
soup.find_all(string="Elsie") # string 이 Elsie 인 것 찾기
soup.find_all(string=["Tillie", "Elsie", "Lacie"]) # or 검색
soup.find_all(string=re.compile("Dormouse")) # 정규식 이용
```



##### 5. string 이 있는 title 태그 모두 검색

```python
soup.title.find_all(string=True)
soup.title(string=True)
```



##### 6. p 태그와 속성 값이 title 이 있는 것 찾기

```python
soup.find_all("p","title") #ex) <p class="title"></p>
```



##### 7. a 태그를 두개만 가져옴

```python
soup.find_all("a",limit=2)
```



##### 8. p 태그와 속성 값이 title 이 있는 것 찾기

```python
soup.find_all("p","title") #ex) <p class="title"></p>
```



##### 9. a태그와 b태그 찾기

```python
soup.find_all(["a","b"])

```



##### 10. 태그명 가져오기

```python
soup.find("div").name
```



##### 11. 태그 삭제

```python
a_tag.img.wrap()
```



##### 12. 태그 추가

```python
soup.p.string.wrap(soup.new_tag("b"))
soup.p.wrap(soup.new_tag("div")
```



##### 13. string을 다른 string으로 교체하기

```python
tag.string.replace_with("새로운 값")
```



##### 14. 보기 좋게 출력하기

```python
soup.b.prettify()
```



##### 15. 속성 값 가져오기

```python
soup.p['class']
soup.p['id']
```



##### 16. 간단한 검색하기

```python
soup.body.b # body태그 아래의 첫번째 b태그
soup.a # 첫번째 a태그
```



##### 17. 속성 값 모두 출력

```python
tag.attrs
```



##### 18. 속성이 있는지 확인하기

```python
tag.has_attr('class')
tag.has_
```



##### 19. 속성 가져오기

```python
soup.find("div")['class'] #속성 값이 없으면 error
soup.find("div").get('class') #속성 값이 없으면 None 반환
```



##### 20.  data-로 시작하는 속성을 찾을 때

```python
soup.find("div", attrs={"data-value":True})
```



##### 21. class를 검색할 땐 class_로 쓴다

```python
soup.find_all("a", class_="sister")
```

