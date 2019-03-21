---
layout: post
title: "DAY9 _ Explicit feedback과 Implicit feedback에 대해 이해, implicit feedback을 풀기 위한 implicit ALS 구현"
subtitle: "10"
categories: data
tags: rs
comments: true







---



# Recommendation System_Day9/10

- DAY9/10 _ Explicit feedback과 Implicit feedback에 대해 이해, implicit feedback을 풀기 위한 implicit ALS 직접 구현
- 각 본문의 **출처**는 제목 링크와 같습니다.
- 각 본문에서 필요하다고 생각되는 부분을 뽑아 정리한 자료입니다.

------

### [Recommendation System with Implicit Feedback](http://sanghyukchun.github.io/73/)

#### [Collaborative Filtering for Implicit Feedback Datasets](http://yifanhu.net/PUB/cf.pdf)



Implicit feedback을 처리하는 가장 기본적인 접근법을 소개해보자. 이 논문은 user u가 item i를 선호하는지 하지 않는지 여부를 가르키는 <u>preference vector p<sub>*ui*</sub> 를 정의</u>한다.  p<sub>*ui*</sub> 의 값은 sign( r<sub>*ui*</sub> )으로 정의할 수 있다. sign 함수는  input이 negative value면 -1, positive value면 1을 return한다. 따라서 perference의 값은 rating r이 0보다 크다면 1이고, r이 0이라면 p도 0이 되는 것이다.

앞서 설명한 것 처럼, preference vector의 값을 항상 신뢰할 수 있는 것은 아니다. 때문에, 이 논문에서는 <u>confience level  c<sub>*ui*</sub></u> 라는 것을 정의하게 된다. 우리가 한 가지 가정할 수 있는 것은 만약  r<sub>*ui*</sub> 의 값이 크다면, 예를 들어 한 사용자가 한 항목을 엄청 많이 재구매했다면, u는 i를 아주 높은 확률로 선호한다는 사실을 가정할 수 있다. 따라서 c<u>onfidence level은 r에 대한 increasing function으로 정의하는 것이 타당</u>하다고 할 수 있다. 이 논문에서는 confidence level  c<sub>*ui*</sub> 를 다양한 방식으로 정의할 수 있다고 언급하고 있으며, 실제 실험에서는 가장 직관적이고 단순한 increasing function인 linear function을 사용한다. 따라서 이 논문에서는 다음과 같은 confidence를 사용한다.

 c<sub>*ui*</sub> =1+αr<sub>*ui*</sub>  

혹은  c<sub>*ui*</sub> =1+αlog(1+r<sub>*ui*</sub>  /ε) 등의 confidence도 대안으로 제안하기는 하지만, 기본적으로 위에서 설명한 linear confidence를 사용하는 듯하다. 한 가지 짚고 넘어가야할 점은,  <u>c<sub>*ui*</sub></u> 는 실제 데이터 r<sub>*ui*</sub> 와 hyper-parameter α에 의해서만 정의되므로 optimize해야 할 parameter가 아니라 한 번 confidence를 정의하기만하면 고정되는 <u>constant</u>라는 점이다. 따라서 confidence의 값을 어떻게 정의하더라도 전체 알고리즘의 로직을 바꾸거나 하지는 않는다.

c를 정의하는 것에는 또 하나의 이점이 있다. Parameter <u>α</u>가 <u>positive observation과 negative observation의 중요도를 조절</u>하는 역할을 하게 되면서, negative feedback에 대한 중요도를 조절할 수 있는 것이다. 예를 들어 α의 크기가 작다면, positive와 negative observation의 confidence 차이가 큰 α를 가질 때 보다 상대적으로 작을 것이라는 것을 기대할 수 있게 된다.

이제 objective를 정의할 차례이다. Explicit feedback에서는 복원한 rating r̂<sub>ui</sub> 와 관측한 데이터  r<sub>*ui*</sub> 의 RMSE를 바로 계산하였으나, 앞서 말한대로 이 값을 그대로 계산하기에는 confidence의 문제가 있다. 이 논문에서는 앞서 정의한 confidence를 고려하여 objective function은 다음과 같이 정의한다.



![image-20190301235525441](/Users/yeoyoung/Library/Application Support/typora-user-images/image-20190301235525441.png)

맨 처음 objective와 달라진 점은, <u>rating vector r (0 이상의 real value) 이 preference vector p (0 또는 1) 로 바뀌었다는 점</u>과, 각각의 u,i pair에 대해 confidence   c<sub>*ui*</sub> 가 곱해진다는 점이다. 이때,  c<sub>*ui*</sub> 는 optimization parameter와는 상관없이 맨 처음 정해지고 변하지 않는 값이므로, 이렇게 바뀐 objective function을 풀기 위해서 이전 문제와 마찬가지로 살짝 변형된 SGD나 ALS 등을 사용할 수 있다. 논문에서는 조금 더 scalability를 고려한 방법론을 제안하는데, matrix product를 조금 더 효율적으로 하도록 matrix들을 decompose하여 조금 더 order가 낮은 연산을 하는 방법을 사용한다. 자세한 알고리즘은 논문을 참고하면 좋을 것 같다.

정리하자면 이 논문은 rating vector r을 preference vector p로 변환하고, confidence level c를 정의한 후, p와 c를 사용해 RMSE objective function을 optimize하는 work인 것이다. 그리고 앞서 설명했던 두 가지 문제는 confidence level c를 정의하는 방법에 의해 해결할 수 있다.

<br/>

> 출처 http://sanghyukchun.github.io/73/

---

### [A Gentle Introduction to Recommender Systems with Implicit Feedback](https://nbviewer.jupyter.org/github/jmsteinw/Notebooks/blob/master/RecEngine_NB.ipynb)

- [download the data link](http://archive.ics.uci.edu/ml/datasets/Online+Retail)
  - all purchases made for an online retail company based in the UK during an eight month period.
- [jupyter notebook link](https://github.com/Yeo0/Recommendation-system/blob/master/Day9%2C10_Recommendation%20system_A%20Gentle%20Introduction%20to%20Recommender%20Systems%20with%20Implicit%20Feedback.ipynb)

- Part 1 : introduction
- Part 2 : Processing the Data
- Part 3 : Creating a Training and Validation Set
- Part 4 : Implementing ALS for Implicit Feedback



