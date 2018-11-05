---
layout: post
title:  "DFS / BFS"
subtitle:   "3"
categories: pg
tags: python
comments: true



---



### 알고리즘 2. DFS / BFS<br/>

#### [github](https://github.com/Yeo0/Data-structure)

#### [이론](https://github.com/Yeo0/Data-structure/blob/master/stack-queue.pdf)

#### 1. DFS

```python
graph = {'A': set(['B', 'C']),
         'B': set(['A', 'D', 'E']),
         'C': set(['A', 'F']),
         'D': set(['B']),
         'E': set(['B', 'F']),
         'F': set(['C', 'E'])}

def dfs(graph, start):
    visited = []
    stack = [start]

    while stack:
        n = stack.pop()
        if n not in visited:
            visited.append(n)
            print("set(visited)=,",set(visited))
            stack += graph[n] - set(visited)
            print("stack=",stack)
            print("visited=",visited)
    return visited

dfs(graph,'A')
```

<br/>

#### 2. BFS

```python
graph = {'A': set(['B', 'C']),
         'B': set(['A', 'D', 'E']),
         'C': set(['A', 'F']),
         'D': set(['B']),
         'E': set(['B', 'F']),
         'F': set(['C', 'E'])}


def bfs(graph, start):
    visited = []
    queue = [start]

    while queue:
        n = queue.pop(0)
        if n not in visited:
            visited.append(n)
            queue += graph[n] - set(visited)
            print("queue=",queue)
            print("visited=",visited)
    return visited

bfs(graph,'A')

```



