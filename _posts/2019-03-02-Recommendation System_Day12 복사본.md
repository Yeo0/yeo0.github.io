---
layout: post
title: "Model based text similarity 공부하기 (Word2Vec, Glove, FastText)"
subtitle: "12"
categories: data
tags: rs
comments: true


---



# Recommendation System_Day12

- DAY12 _ Model based text similarity 공부하기 (Word2Vec, Glove, FastText)
- 각 본문의 **출처**는 제목 링크와 같습니다.
- 각 본문에서 필요하다고 생각되는 부분을 뽑아 정리한 자료입니다.

------

### [딥러닝을 이용한 자연어 처리](https://www.edwith.org/deepnlp/home) _ [CBoW & RN & CNN](https://www.edwith.org/deepnlp/lecture/29208/)

- 문장표현(Sentence representation)
- Continuous bag-of-words
- Relation Network
- Convolution Neural Network

#### 문장표현(Sentence representation)

문장표현(Sentence representation)의 의미: 어떤 과제를 풀기에 적합하고 숫자로 나타낸 문장의 표현입니다

- ##### CBoW ( Continues bag-of-words)

![image-20190302212209898](/Users/yeoyoung/Library/Application%20Support/typora-user-images/image-20190302212209898.png)

![image-20190302213530179](/Users/yeoyoung/Library/Application%20Support/typora-user-images/image-20190302213530179.png)

*[DAG](https://en.wikipedia.org/wiki/Directed_acyclic_graph) : Directed acyclic graph

- **CBoW(Continuous bag-of-words):**

- - 단어장을 단어 주머니로 보게되고, 이에 따라 단어의 순서는 무시합니다. 
  - 문장에 대한 표현은 <u>단어 벡터들을 평균시킨 벡터</u>로 구합니다.
  - 효과가 좋기 때문에 제일 먼저 시도해봐야합니다. (<u>Baseline 모델</u>)
  - 공간상에서 가까우면 비슷한 의미, 아니면 멀리 떨어져 있을 것입니다.
  - 장점 : 결과가 좋음 ([Fasttext](https://fasttext.cc/) 활용)

![image-20190302213633173](/Users/yeoyoung/Library/Application%20Support/typora-user-images/image-20190302213633173.png)

내가 푸는 문제에서 가장 적합한 sentence가 무엇인지에 따라서, 즉, 모델을 어떻게 만드느냐에 다라서 representation이 달라집니다. (ex. category classification을 한다고 한다면 내가 원하는 카테고리에 필요한 representaiton)

<br/>

- ##### Relation Network

![image-20190302214314371](/Users/yeoyoung/Library/Application%20Support/typora-user-images/image-20190302214314371.png)

![image-20190302214605770](/Users/yeoyoung/Library/Application%20Support/typora-user-images/image-20190302214605770.png)

![image-20190302214823080](/Users/yeoyoung/Library/Application%20Support/typora-user-images/image-20190302214823080.png)



*색칠된 부분만 CBoW와 다르다

<br/>

- **Relation Network(Skip-Bigram):**

- - <u>문장안에 있는 모든 토큰 쌍(pairs)</u>을 보고, 각 쌍에 대해서 신경망을 만들어서 문장표현을 찾습니다.
  - 장점: 여러 단어로 된 표현을 탐지 할 수 있습니다. (CBoW보단 쉽게)
  - 단점: 모든 단어간의 관계를 보기 때문에, 전혀 연관이 없는 단어도 보게 됩니다.  (영어 같은 S V O 구조 언어에서 굳이 첫 단어와 끝 단어의 연관관계를 봐야하는가)

<br/>

- ##### CNN (Convolution Neural Network)

![image-20190302215100970](/Users/yeoyoung/Library/Application%20Support/typora-user-images/image-20190302215100970.png)

![image-20190302215412248](/Users/yeoyoung/Library/Application%20Support/typora-user-images/image-20190302215412248.png)

- **Convolution Neural Network(CNN) :**
  - 특징:
    - k-gram (나란히 붙어있는 k개의 단어들) 을 계층적으로(hierachically) 보게 됩니다.
    - <u>Layer 를 쌓을 때 마다, 점진 적으로 넓은 범위</u>를 보기 때문에, <u>"단어(token) > 다중 단어 표현(multi-word expression) > 구절(phrases) > 문장(sentence)"</u>순으로 보는 인간의 인식과도 알맞습니다. 
    - 1차원의 Convolutional Network 입니다. (텍스트)
    - 구현이 잘 되어있습니다. (효율성등에서 사용하기 좋음)
  - 장점: 좁은 지역간 단어의 관계를 볼수 있습니다.

<br/>

---

### [딥러닝을 이용한 자연어 처리](https://www.edwith.org/deepnlp/home) _ [Self Attention & RNN](https://www.edwith.org/deepnlp/lecture/29209/)

- 지난 시간이 이야기한 CNN 과 RN 의 관계를 살펴보면 아래와 같습니다.
- RN:
  - 모든 다른 토큰의 관계를 봅니다. <u>모든 단어간의 관계를 봐서 효율적이지 못합니다.</u>
  -  h<sub>t</sub> = *f(x<sub>t</sub>,x<sub>1</sub>)* +⋯+*f(x<sub>t</sub>,x<sub>t-1</sub>)*+*f(x<sub>t</sub>,x<sub>t+1</sub>)*)+⋯+*f(x<sub>t</sub>,x<sub>T</sub>)*
- CNN:
  - 작은 범위의 토큰의 관계를 봅니다. 따라서 <u>더 먼 거리의 단어간의 관계가 있을 경우 탐지할 수 없거나 더 많은 convolution 층을 쌓아야합니다.</u>
  -  h<sub>t</sub> = *f(x<sub>t</sub>,x<sub>t-k</sub>)* +⋯+*f(x<sub>t</sub>,x<sub>t</sub>)*+⋯+*f(x<sub>t</sub>,x<sub>t+k</sub>)*

- <u>어떻게 하면 두개를 조합해 조금 더 generalize할 수 있을까?</u>

- CNN 방식을 가중치가 부여된 RN의 일종으로 볼 수도 있습니다. 

![image-20190302223759764](/Users/yeoyoung/Library/Application%20Support/typora-user-images/image-20190302223759764.png)

(가까이에 있는 애들은 weight = 1 , 그 밖은 0 )

<br/>

- ##### Self Attention

  IDEA : CNN에서 가중치가 0 과 1 이 아닌 그 사이의 값으로 계산 할 수 있다면 어떨까? (by Neural Net)

![image-20190302224844100](/Users/yeoyoung/Library/Application%20Support/typora-user-images/image-20190302224844100.png)

![image-20190302223815204](/Users/yeoyoung/Library/Application%20Support/typora-user-images/image-20190302223815204.png)

이 때, weight constraint 필요하다. (0~1사이 or 합이 1이 되도록)

- 장점:

  - Long range & short range dependency 극복할 수 있습니다.

  - 관계가 낮은 토큰은 억제하고 관계가 높은 토큰은 강조할 수 있습니다.

- 단점
  - 계산 복잡도( 매번 pairwise interaction을 계산해야 하기 때문) 가 높고 counting 같은 특정 연산이 쉽지 않습니다. 

<br/>

- ##### Recurrent Neural Network 

![image-20190302225352586](/Users/yeoyoung/Library/Application%20Support/typora-user-images/image-20190302225352586.png)

![image-20190302225636643](/Users/yeoyoung/Library/Application%20Support/typora-user-images/image-20190302225636643.png)

- **Recurrent Neural Network(RNN):** 

  - 메모리를 가지고 있어서 현재까지 읽는 정보를 저장할 수 있습니다. (한 토큰 읽을 때 마다 메모리에 정보를 업데이트)

- - 문장의 정보를 시간의 순서에 따라 압축 할 수 있습니다.
  - 단점:
    - 문장이 많이 길어질 수록 고정된 메모리에 압축된 정보를 담아야 하기 때문에, 앞에서 학습한 정보를 잊습니다. 이는 곧 정보의 손실을 뜻합니다. 
    - 토큰을 순차적으로 하나씩 읽어야 하기 때문에, 훈련 할때 속도가 기타 네트워크 보다 느립니다. (independent 하지 않다.)
  - Long Term Dependency 해결방법:
    - bidirectional network를 쓰게됩니다. (왼쪽 -> 오른쪽 + 오른쪽 -> 왼쪽)
    - <u>LSTM, GRU</u> 등 RNN의 변형을 사용합니다.

<br/>

----

### [딥러닝을 이용한 자연어 처리](https://www.edwith.org/deepnlp/home) _ [Summary](https://www.edwith.org/deepnlp/lecture/29210/)

![image-20190302230455364](/Users/yeoyoung/Library/Application%20Support/typora-user-images/image-20190302230455364.png)

![image-20190302231134344](/Users/yeoyoung/Library/Application%20Support/typora-user-images/image-20190302231134344.png)Sentence representation의 5가지 방법들.

- CBoW 
- RN
- CNN
- Self-Attention
- RNN

<br/>

- CBoW를 제외하고 나머지는 문장이 주어졌을 때 각 토큰 위치 별로 벡터를 추출합니다.

- 5개 모두 다 combine해서 쓸 수 있는 알고리즘 입니다. (ex) Self-Attention + RNN)

- Classification이 목적인 경우 최종적으로 Average를 많이 합니다.

<br/>

---

### [딥러닝을 이용한 자연어 처리](https://www.edwith.org/deepnlp/home) _ [Questions](https://www.edwith.org/deepnlp/lecture/29219/)

**1. 단어 임베딩에서 다의어(polysemy) 문제는 어떻게 해결하나요?**

벡터들은 High dimensional space에 놓여있다. 따라서 neighbor들이 많이 있기 때문에 서로 다른 의미에 대해서도 neighborhood를 다 임베딩 할 수 있다. 

<br/>

**2. 훈련 데이터에 없는 새로운 단어는 어떻게 표현이 되나요?**

어떤 token level에서 진행되는가를 보아야 한다. 새로운 단어를 쓰는 example들을 training set에 추가해서 튜닝을 하거나 새로운 단어를 기존에 존재하는 임베딩들을 이용해서 새로 만들어 줄 수 도 있다.  

<br/>

**3. 분류 모델 훈련 완료후, 새로운 클래스가 등장했을 때 어떻게 해결하나요?**

1) 새로 클래스 추가 될 때마다 데이터 모아서 새로 training

2) example 몇 개만 찾아서 weight vector 하나 늘어난 것에 대해서만 estimation을 다시 한다. 이 때 과연 다른 기존에 있던 다른 weight과 parameter과 맞게 학습이 될 것인가에 대한 의문이 생길 것이다. 

-> 클래스가 굉장히 많고 클래스 하나하나의 의미를 다 알고 있다고 하면 클래스의 description을 가질 수 있고 그것으로  클래스 간의 관계를 파악할 수 있다 (ex . image classification할 때 description(ex)호랑이는 고양이과)이 클래스간의 관계를 알려준다.) 알려진 것중에는 zero shot, few shot learning / wasabi(Jason Weston) 이 잘 된다.

<br/>

**4. 임베딩에서 “가깝다”는 벡터 공간에서 코사인 유사도를 말하는 건가요? 아니면 다른 distance metrics 를 정의해서 사용하나요?**

word vector가 나온 후에 어떤 network이 씌여서 training 됐는지가 중요하고 여기에 따라서 적합한 metric이 달라진다. 만약 각 벡터들의 length를 normalize한 후 average를 했다면 cosine distance가 맞는 metric이 될 것이다. 

하지만 보통은 이렇게 하기 쉽지 않다. 그래서 어떤 metric이 쓰이는 지는 정확히 알 수 없지만 대부분 사람들은 cosine similarity가 괜찮다.. 고 말한다.

어떤게 최적인지는 어떻게 training이 됐는지와 어떤 downstream task 인지 ( 클러스터링을 하는지 다른걸 하는지 등등) 등 에 따라서 다르다. 즉, distance metric자체도 hyper parameter가 되고 여기서 model selection을 할 수 있다.

<br/>

**5. Capsule network로 텍스트 분류 문제를 사용하는건 어떤가요?**

text에선 큰 장점이 없다. sentence representation을 처음에 뽑아낸 후에 capsule net을 쓸 수 있겠지만 좀 더 시간이 지나봐야 알 듯 하다.

<br/>

**6. Attention 모델에서 전체 문장을 보지 않고 고정된 윈도우 사이즈를 정해서 하면 어떤가요?**

사이즈를 줄이려는 이유는 1) 성능이 좋아히지 않을까 2) computation efficenticy 인데, 사실 trade off관계라 선택이 필요하다. 실제로 구글 NLP 팀에서 ratio를 기준으로 나누는걸 진행했었다.

<br/>

**7. Self attention은 어떻게 최적화 되나요?**

일반적인 방법인 backpropogation으로 gradient계산하는걸로도 가능하고 SCD 쓰는것도 가능하다. 

Optimization을 어려운 이유는 training 초반에는 attention weight 이 제대 training이 안되어있기 때문에 parameter들이 다 작고 굉장히 flat한 상태이다. 이 상황에서 credit assignment를 할 수 있는가 하는 문제가 발생한다. 즉, summantion Term 부분에서 어떤 term들이 중요한 contribution을 했는가를 정해야 하는 데 만약 weight function이 flat 하게 다 똑같이 값을 주고 있었다면 누가 중요했는지 알 수 없고 learning이 진행이 잘 안되게 된다. 결론적으로Parameter initialization을 어떻게 하느냐가 굉장히 까다롭다.





































