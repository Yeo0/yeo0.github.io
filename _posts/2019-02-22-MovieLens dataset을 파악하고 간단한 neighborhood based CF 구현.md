---
layout: post
title: "MovieLens dataset을 파악하고 간단한 neighborhood based CF 구현"
subtitle: "8"
categories: data
tags: rs
comments: true





---



# Recommendation System_Day7

- DAY7 _ MovieLens dataset을 파악하고 간단한 neighborhood based CF 구현
- 본문의 **출처**는 제목 링크와 같습니다.

<br/>

---

### [Building collaborative filtering model from scratch](https://www.analyticsvidhya.com/blog/2018/06/comprehensive-guide-recommendation-engine-python/)

- [data download link](https://grouplens.org/datasets/movielens/100k/)

- [jupyter notebook link](https://github.com/Yeo0/Recommendation-system/blob/master/Day7_Recommendation%20system_%20Building%20collaborative%20filtering%20model%20from%20scratch.ipynb)




1) load package / read data

```python
import pandas as pd
%matplotlib inline
import matplotlib
import matplotlib.pyplot as plt
import numpy as np
from sklearn.metrics.pairwise import pairwise_distances

#users
u_cols = ['user_id', 'age','sex','occupation', 'zip_code']
users = pd.read_csv('2_2_data_ml-100k/u.user', sep="|", names=u_cols, encoding='latin-1')

#ratings
r_cols = ['user_id','movie_id','rating','unix_timestamp']
ratings = pd.read_csv('2_2_data_ml-100k/u.data', sep='\t', names=r_cols, encoding='latin-1')

#items
i_cols = ['movie id', 'movie title' ,'release date','video release date', 'IMDb URL', 'unknown', 'Action', 'Adventure',
'Animation', 'Children\'s', 'Comedy', 'Crime', 'Documentary', 'Drama', 'Fantasy',
'Film-Noir', 'Horror', 'Musical', 'Mystery', 'Romance', 'Sci-Fi', 'Thriller', 'War', 'Western']
items = pd.read_csv('2_2_data_ml-100k/u.item', sep='|', names=i_cols,
encoding='latin-1')

r_cols=['user_id', 'movie_id', 'rating', 'unix_timestamp']
ratings_train= pd.read_csv('2_2_data_ml-100k/ua.base', sep='\t', names=r_cols, encoding='latin-1')
ratings_test= pd.read_csv('2_2_data_ml-100k/ua.test', sep='\t', names=r_cols, encoding='latin-1')
ratings_train.shape, ratings_test.shape
```

<br/>

2) build model

```python
n_users = ratings.user_id.unique().shape[0] # 중복값제외하고 행 개수 
n_items = ratings.movie_id.unique().shape[0]

data_matrix = np.zeros((n_users, n_items))


for line in ratings.itertuples():
    data_matrix[line[1]-1, line[2]-1]=line[3]
    
#cosine similarity
user_similarity = pairwise_distances(data_matrix, metric='cosine')
item_similarity = pairwise_distances(data_matrix.T, metric='cosine')

def predict(ratings, similarity, type='user'):
    if type =='user':
        mean_user_rating = ratings.mean(axis=1) #row 방향 
        ratings_diff = (ratings - mean_user_rating[:,np.newaxis]) #np.newaxis - mean_user_rating 과 같은 foarmat 위해 
                                                                  #a[:,np.newaxis] : 열방향 재배열 / a[np.newaxis,:] : 행방향 재배열
        pred = mean_user_rating[:,np.newaxis] +  similarity.dot(ratings_diff) / np.array([np.abs(similarity).sum(axis=1)]).T
    elif type == 'item':
        pred = ratings.dot(similarity) / np.array([np.abs(similarity).sum(axis=1)])

    return pred
        
    
user_pred = predict(data_matrix, user_similarity, type='user')
item_pred = predict(data_matrix, item_similarity, type='item')

```

