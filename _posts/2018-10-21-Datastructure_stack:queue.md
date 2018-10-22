---
layout: post
title:  "Stack / Queue"
subtitle:   "2"
categories: pg
tags: python
comments: true


---



### 자료구조 1. Stack / Queue

##### <br/>

#### [github](https://github.com/Yeo0/Data-structure)

#### [이론](https://github.com/Yeo0/Data-structure/blob/master/stack-queue.pdf)

#### 1. Stack

```python
#추상 자료형 (ADT) 구현
class StackAdt:
    # 데이터의 추가
    def push(self, data):
        pass
    # 데이터의 꺼내오기
    def pop(self):
        pass
    # 데이터 참조하기
    def top(self):
        pass
    
    #sub func
    # 비어있는지 확인
    def isEmpty(self):
        pass
    # 꽉 차있는지 확인
    def isFull(self):
        pass
    # 리스트 사이즈 출력
    def size(self):
        pass
    # 리스트 전체 출력
    def display(self):
        pass
    

        
class ArrayStack(StackAdt):
   def __init__(self, max_length=30):
     
     self.items = []
     self.high = 0  # high: 데이터를 ㅊ저장할 최신 위치
     self.max_length = max_length

   def push(self, data):
     if self.isFull():  # push할 수 있는지 확인
       raise Exception('스택이 꽉 찼습니다!')

     self.items.append(data)
     self.high += 1
     
     
   def pop(self):
       if self.isEmpty(): # pop할 수 있는지 확인
           raise Exception('스택이 비었습니다!')
 
       self.high -= 1
       data = self.items[self.high] #제일 먼저 들어온게 제일 위에
       del self.items[self.high]
  
       return data


   def top(self):
      if self.isEmpty():
          raise Exception('스택이 비었습니다!')

      return self.items[self.high - 1] # pop예정인 데이터를 참조한다. index 0부터 시작

   def isEmpty(self):
      return self.high == 0  # high이 0이면, 저장된 데이터가 하나도 없는 것 / push할 때마다 +1

   def isFull(self):
      # high==ㅇ max_length와 동일할 때 꽉참.
      return self.high == self.max_length
   
   def stackSize(self):
     if self.isEmpty():
         raise Exception('스택이 비었습니다!')
    
     return len(self.items)
    
   def display(self):
     if self.isEmpty():
       raise Exception('스택이 비었습니다!')
       
     for index in range(self.high):
         print(self.items[index])
         
```

```python
stack=ArrayStack()
stack.push(3)
stack.push(4)
stack.push(8)
stack.display()
stack.stackSize()
stack.pop()
stack.pop()
stack.display()
stack.push(7)
stack.top()
stack.stackSize()
stack.pop()
stack.stackSize()
stack.isEmpty()
```

<br/>

<br/>

#### 2. Queue

```python
class QueueAdt:
    # 데이터의 추가
    def enqueue(self, data):
        pass
    # 데이터의 꺼내오기
    def dequeue(self):
        pass
    #sub func
    # 데이터 참조하기
    def front(self):
        pass
    # 비어있는지 확인
    def isEmpty(self):
        pass
    # 꽉 차있는지 확인
    def isFull(self):
        pass
    # 리스트 전체 출력
    def display(self):
        pass
    
class ArrayQueue(QueueAdt):

     
   def __init__(self, max_length=30):

       self.items = []
       self.size = self.first = self.last = 0 #순서가 있기 때문에. / size 큐 크기
       self.max_length = max_length
       
   def enqueue(self, data):
       if self.isFull():  # enqueue할 수 있는지 확인
           raise Exception('큐가 꽉 찼습니다!')
           
       self.items.append(data)    
       self.items[self.last] = data
       self.last += 1
       self.size += 1


   def dequeue(self):
       if self.isEmpty(): # dequeue 수 있는지 확인
           raise Exception('큐가 비었습니다!')
 
       data = self.items[self.first]
       self.items[self.first]=None
       
       self.first += 1
       self.size -= 1
       
       return data

   def front(self):
       if self.isEmpty():
           raise Exception('큐가 비었습니다!')
       return self.items[self.first]
       
   def isEmpty(self):
       return self.size == 0  
   
   def isFull(self):
     
       return self.size == self.max_length
   
   def queueSize(self):
       if self.isEmpty():
          raise Exception('큐가 비었습니다!')

       return self.size
    
   def display(self):
       if self.isEmpty():
          raise Exception('큐가 비었습니다!')
       
       for index in range(self.size):
          print(self.items[index])
```

```
queue=ArrayQueue()
queue.enqueue(3)
queue.enqueue(4)
queue.display()
queue.queueSize()
queue.dequeue()
queue.queueSize()
queue.dequeue()
queue.display()
queue.enqueue(7)
queue.front()
queue.queueSize()
queue.dequeue()
queue.display()
queue.isEmpty()


```

