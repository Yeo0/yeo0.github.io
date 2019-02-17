---
layout: post
title: "추천시스템의 시작 Netflix prize에 대한 이해"
subtitle: "2"
categories: data
tags: rs
comments: true



---



# Recommendation System_Day1

- DAY1 _ 추천시스템의 시작 Netflix prize에 대한 이해
- 각 본문의 **출처**는 제목 링크와 같습니다.
- 각 본문에서 필요하다고 생각되는 부분을 뽑아 정리한 자료입니다.

<br/>

---

### [**From the Labs: Winning the Netflix Prize**](https://www.youtube.com/watch?v=ImpV70uLxyw)

#### Netflix Prize 승자 인터뷰. 

1) analysis data set

2) SVD (singular value decomposition) _ helps organize vast datasets

- dimensional reduction method in Linear algebra

- characterizes each movie and each user by a vector
- hard to handle 'Napolean dynamite', which has big gaps between ratings. (Only 5 points or 1 points) 
- Combine 3 teams to one and combine each team's models to one model. -> increase by 6%

<br/>

----

### [**How Does Netflix Recommend Movies?**](http://sanghyukchun.github.io/30/)

- #### [RMSE](https://ko.wikipedia.org/wiki/%ED%8F%89%EA%B7%A0_%EC%A0%9C%EA%B3%B1%EA%B7%BC_%ED%8E%B8%EC%B0%A8) (Root Mean Square Error ; 평균 제곱근 오차)

  ![img](https://lh4.googleusercontent.com/GD-CcmSDeb1ficAt41u0ZDtFd7syTpJGc_NJ3NGTlQtY-rikX7Tqn9DMaG4b5JtWlKOI6RBayJZNxr4h5SHL2SeKX9ceQCLj9uGTuqeAfgS0EDjh20oZnImahJ2oUa3up9E7KjI)

  

- #### [Matrix Factorization](https://en.wikipedia.org/wiki/Matrix_factorization_(recommender_systems))

사람들의 type, 영화 class가 많지 않다는 것을 가정. 즉, drama를 얼마나 좋아하느냐, action을 얼마나 좋아하느냐 등등의 요소들이 각 유저들의 rating을 결정한다는 의미이다. 만약 전체 점수를 S, factor를 f<sub>i</sub>, 각각의 factor마다 개인이 가지는 가중치(rating)를 a<sub>i</sub>, 전체 n개의 factor가 있다고 가정. 한 사람이 rating하게 될 점수의 예상치를 아래와 같이 나타낼 수 있다.

![image-20190216193301460](/assets/img/rs1_1.jpg)

이런 몇 개의 basic classes의 combination으로 user의 rating이 표현이 될 수 있다면, basic한 몇 개의 요소로 rating이 결정된다 라고 설명할 수 있으며 약간 수학적으로 설명을 하자면 Netflix Matrix가 몇 안되는 factor들을 통해 표현할 수 있다는 의미가 되므로 Netflix Matrix가 low rank를 가지고 있다라고 표현할 수 있다.



![img](http://sanghyukchun.github.io/images/post/30-1.png)

이 알고리즘의 목표는 각각의 ‘ratings of class i’ 를 알아내는 것이다. 이 알고리듬이 실제 의미가 있기 위해서는 Netflix Matrix에서 알고 있는 데이터가 어느 정도 많아야 한다. 실제로 해당 decomposed 된 matrix에 들어있는 entry보다는 많은 데이터를 알고 있어야 하는데, 위의 그림에서 우리는 18,000개의 영화와 480,000명의 유저의 정보를 2개의 class로 표현했으므로 우리가 이미 알고 있는 1%의 정보를 사용하면, 총 48000 * 18000 * 0.01개, 약 8백만개 정도의 데이터를 사용해서 2 * 48000 + 18000 * 2 개, 즉 13만 2천개의 entry를 알아내야 한다. 8백만개의 정보에서 13만 2천개의 정보를 뽑아내는 것은 데이터의 양이 충분하다고 할 수 있을 것이다. 물론 지금은 rank가 2이라고 가정했으므로 2를 곱했고 13만 2천이라는 숫자를 얻게 되었고 실제로는 실제로는 이보다는 더 많은 rank를 가질 것 이지만 그래도 8백만개에 비하면 충분히 작은 숫자라고 할 수 있을 것.

<br/>

---

### [NETFLIX PRIZE – 다이나믹 했던 알고리즘 대회 1](http://www.shalomeir.com/2014/11/netflix-prize-1/)

### [NETFLIX PRIZE – 다이나믹 했던 알고리즘 대회 2](http://www.shalomeir.com/2014/11/netflix-prize-2/)

### [NETFLIX PRIZE – 다이나믹 했던 알고리즘 대회 3 ](http://www.shalomeir.com/2014/12/netflix-prize-3/)

- Netflix Prize에 대한 상세한 설명. 

- Netflix Prize에서 사용했던 RMSE를 이용한 성능 평가는 영화 추천 서비스를 제공하는데 있어 최적화된 방법은 아니라고 할 수 있다. 왜냐하면 영화 예측 시스템이 유저가 안 본 모든 영화에 대하여 별점을 잘 예측하는 것보다는 **어떤 영화를 가장 재미있게 볼지를 예측하는 것이 중요하기 때문**이다. 그러므로 별표 1개를 줄 영화를 잘 예측하는 것은 영화를 서비스하는 입장에선 별로 의미가 없다고 할 수 있으며, 추천 시스템이 유저에게 재미있게 볼 것이라고 예상한 Top N 영화목록이 실제 유저가 좋아할만한 영화인지가 더 중요하다. 그래서 Netflix Prize 우승팀의 Yahuda Koren 연구원의 논문에서도 이를 지적하며 다른 평가방법을 제안하였다. 현재는 **Top N의 Precision** 을 보거나 **nDCG** 등의 다른 평가 방법을 통해 추천할 순서로 상위 예측 영화에 더 가중치를 주어 추천 시스템의 성능을 평가하고 있다.

<br/>

































































