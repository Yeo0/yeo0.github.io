---
layout: post
title: "DAY11 _ CF의 limitation을 이해하고 text data에 익숙해지기"
subtitle: "11"
categories: data
tags: rs
comments: true
---

# Recommendation System_Day11

- DAY11 _ CF의 limitation을 이해하고 text data에 익숙해지기
- 각 본문의 **출처**는 제목 링크와 같습니다.
- 각 본문에서 필요하다고 생각되는 부분을 뽑아 정리한 자료입니다.

------

### Machine Learning Summer School @CMU 2014 중 Introduction to Recommendation System Lecture 중 일부

- [Video _Machine Learning Summer School 2014 in Pittsburgh (1h43m31s ~ 1h56m39s)](https://www.youtube.com/watch?v=bLhq63ygoU8&feature=youtu.be&t=1h43m31s)

- [Slides_Recommender Systems (Machine Learning Summer School 2014 @ CMU) (89 page ~ 108 page)](https://www.slideshare.net/xamat/recommender-systems-machine-learning-summer-school-2014-cmu)

<br/>

---

#### Limitation of collaborative filltering

![image-20190302184038744](/assets/img/rs11_1.png)



Cold Start problem : Business 시작 할 때 추천시스템을 사용할 것을 권장했지만 초기에 유저가 없는 상태에서 (= user-item interaction data가 없는 상태에서) 추천시스템을 사용하라는 건 사실 불가능하다는 것.

Popularity Bias problem : 유명한 것으로 추천이 치우치게 된다는 것. 음악을 추천한다고 할 때, 사실상 collaborative filtering을 사용하여 3명 밖에 듣지않은 음악을 추천하는 것은 매우 어려운 일이다. 같은 similarity점수라 하더라도 더 많은 사람들이 좋아한 것을 추천하게 된다.



![image-20190303035321025](/assets/img/rs11_2.png)





1) new user problem

처음 유저가 새로 들어왔다고 하자. 이 유저에 대해 아무것도 모르는데 어떻게 시작해야 할까 ? 이 때는 기본적으로 유명한 것을 추천한다. 그리고 여기에 대한 피드백을 바탕으로 본격적인 추천을 시작한다.

<br/>

#### Content-Based Recommendations

![image-20190303040033178](/assets/img/rs11_3.png)

![image-20190303040357136](/assets/img/rs11_4.png) 

- IDEA : 우리는 아이템을 위한 similarity function 찾아야 한다. 이 때 이것은 아이템의 contents (장르, 개봉년도, 배우 등등) 를 분석하는 것을 기반으로 한다. 
- Content based recommendation은 <u>유저의 과거 아이템 데이터 (=과거 interaction)를 기반</u>으로 한다.



![image-20190303040809130](/assets/img/rs11_6.png)



기본 진행과정은 위와 같다. 먼저 Item에 대한 정보를 바탕으로 feature을 추출한다. 우리는 이 feature들을 가지고 모델을 만들수 있고, 유저의 기존 데이터를 모델에 적용하여 만든 training data를 통해 새로운 rating matrix를 만드는 것이 CB이다.

<br/>

#### Advantages / Disadvantages of CB Approach



![image-20190303041616362](/assets/img/rs11_7.png)



user가 없을 때 시작하는 초기 단계에서 좋은 방법이 된다는 장점이 있다.

<br/>

![image-20190303042701404](/assets/img/rs11_8.png)



아이템의 성격을 잘 파악해야 하고, 쉽게 오버피팅 될 수 있다는 단점이 있다. (Ex) 유저가 호러/스릴러에 좋다는 표시를 했다면 그 다음 모든 추천이 다 호러/스릴러 가 될 수 있다)

<br/>

#### Content-based Methods

![image-20190303042746042](/assets/img/rs11_9.png)



TF: uniqueness를 측정한다. 만약에 collection안에서 매우 common하다면 적은 정보를 주는 것이고, uncommon하다면 더 많은 정보를 주는 것이라 본다. 

IDF : 빈도를 나타낸다. (얼만큼 나타나는지)

<br/>

#### Content-based User Profile

![image-20190303043720276](/assets/img/rs11_10.png)

Content-based user profile을 활용하는 과정이다. Feature space를 정의하고 아이템을 Feature space에 나타낸다. 여기서 이미 나타나져 있는 유저와의 similarity function을 찾는다.

<br/>

#### A word of caution

![image-20190303044101025](/assets/img/rs11_11.png)



넷플릭스 prize가 끝나고 쓰여진 논문이다. 요약하면 흥미로운 점은 모든 meta데이터를 사용하는 것 보다 일부를 사용한 것이 ( rating 몇 개를 추가한 것이)  훨씬 더 powerful 했다고 한다. 또한 <u>일반적으로 CF가 CB보다 뛰어났</u>다고 한다.

<br/>

---

### [딥러닝을 이용한 자연어 처리](https://www.edwith.org/deepnlp/home) _ [Overview](https://www.edwith.org/deepnlp/lecture/29206/)

- 텍스트 분류(Text Classification):

  - Supervised learning으로 문장, 문단 또는 글을 어떤 카테고리에 분류하는 작업

  - Input: 하나의 문장, 문단 혹은 문서
  - Output: 유한한 C 개의 카테고리 (input 이 어떤 카테고리에 속하는지)


- 예시

  - 감성 분석

  - 카테고리 분류
    - 뉴스 
    - 영화리뷰
  - 의도 분류
    - 이메일 스팸분류


<br/>

---

### [딥러닝을 이용한 자연어 처리](https://www.edwith.org/deepnlp/home) _ [How to represent sentence & token?](https://www.edwith.org/deepnlp/lecture/29207/)

#### 토큰(tokens)

- 문장은 일련의 토큰(tokens)으로 구성되어 있다. 이미지와 비교했을 때 <u>텍스트 토큰은 다소 주관적, 임의적(arbitrary)</u>인 성격을 띄고 있다. 

  ![image-20190302202911441](/assets/img/rs11_12.png)

- 토큰을 나누는 기준은 다양합니다.

  - 공백(White space)

  - 형태소(Morphs)
  - 어절
  - 비트숫자


![image-20190302203055708](/assets/img/rs11_13.png)

- 단어를 숫자로 표현하기 위해 단어장(Vocabulary)을 만들고, 중복되지 않는 인덱스(index) 로 바꿔준다. 궁극적으로는 모든 문장이 정수로 바뀌게 되며 이를 **인코딩(Encoding)**이라 한다.
- 하지만 관계없는 숫자의 나열로 인코딩하는 것은 우리가 원하는 것이 아니므로 비슷한 의미의 단어를 가깝게, 그렇지 않으면 멀리 있도록 하는 과정이 필요하다.
  - <u>One hot Encoding</u>
    - 길이가 단어장의 총 길이(∣*V*∣)인 벡터에서, 단어의 index 위치에 있는 값은 1, 나머지는 0으로 구성한다.
    - *x*=[0,0,0,⋯,0,1,0,⋯,0,0]∈{0,1}∣*V*∣ 
    - 단점: 모든 토큰 간에 거리가 같다. 모든 단어의 뜻이 같지 않기 때문에 <u>거리가 달라져야 우리가 원하는 단어간의 관계를 파악할 수 있다.</u> 




![image-20190302203746072](/assets/img/rs11_14.png)



- 각 토큰을 <u>**연속 벡터 공간(Continuous vector space)** 에 투영</u>한다. 이를 **임베딩(Embedding)** 이라고 한다. 이렇게 되면 비슷한 특징을 가진 것 끼리 가까이에 위치하게 된다.
  - **Table Look Up**: 각 <u>one hot encoding 된 토큰에게 벡터를 부여하는 과정</u>. 즉 토큰이 실제 의미하는게 무엇인지 찾는 과정이다. 실질적으로 one hot encoding 벡터( *x* )와 연속 벡터 공간( *W* )을 내적 한 것 (=weight matrix를 곱한 것) 이다. 

<br/>

#### 문장표현(Sentence representation)

- ##### CBoW ( Continues bag-of-words)

![image-20190302204312541](/assets/img/rs11_15.png)



- Table Look Up 과정을 거친후 모든 문장 토큰은 연속적이고 높은 차원의 벡터로 변하게 된다. Vocablory에 해당하는 integer index들이있고, 거기에 일치하는 토큰들이 있고, 그 옆에 그에 일치하는 벡터가 있는 것이다. 즉 Neural Net이 토큰을 받았을 때 integer index를 찾아서 거기에 맞는 벡터를 가져오게 되는 것이다.
- *X*=(*e*1,*e*2,⋯,*e<sup>T</sup>*)*where* *e<sub>t</sub> ∈ R<sup>d</sup>
- 계산 후 나온 벡터의 사이즈는 카테고리의 개수와 같다. 
- Softmax함수를 거치게 되면  Input sentence가 어떤 카테고리에 속할지에 대한 probability들이 Output이 된다.

<br/>

---

### [University of Washington CSE573 렉쳐 중 일부](https://courses.cs.washington.edu/courses/cse573/12sp/lectures/17-ir.pdf )

- 참고자료 

