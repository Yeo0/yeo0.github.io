---
layout: post
title:  "Sorting(1)"
subtitle:   "1"
categories: pg
tags: python
comments: true

---



## 알고리즘 _1. 정렬 (1)

##### <br/>

#### [github](https://github.com/Yeo0/Study/tree/master/Algorithm)

#### [이론](https://github.com/Yeo0/Study/blob/master/Algorithm/Algorithm_1.pdf)

#### 1. Bubble Sort

```python
N=int(input("배열 크기를 입력하세요: "))

inputlist=[]

for i in range(N):
	element = input("배열의 원소를 입력해 주세요: ")
	inputlist.append(element)


print(inputlist)


def Bubblesort_asc(x):
	for start in range(len(x)):
		for i in range(1,len(x)-start):
			if x[i-1]>x[i]:
				temp=x[i-1]
				x[i-1]=x[i]
				x[i]=temp
	return x

print(Bubblesort_asc(inputlist))
```

<br/>

#### 2. Selection Sort

```python
N=int(input("배열 크기를 입력하세요: "))

inputlist=[]

for i in range(N):
	element = input("배열의 원소를 입력해 주세요: ")
	inputlist.append(element)


print(inputlist)

def Selectionsort_asc(x):
	for i in range(len(x)-1):
		min=i
		for j in range(i+1,len(x)):	
			if x[j] < x[min]:
				min=j
		temp=x[i]
		x[i]=x[min]
		x[min]=temp
	return x


print(Selectionsort_asc(inputlist))



```

<br/>

#### 3. Insertion Sort

```python
N=int(input("배열 크기를 입력하세요: "))

inputlist=[]

for i in range(N):
	element = input("배열의 원소를 입력해 주세요: ")
	inputlist.append(element)


print(inputlist)

def Insertionsort_asc(x):
	for i in range(len(x)):
		current=x[i]
		j=i-1
		while(j>=0 and x[j]>current):
			x[j+1]=x[j]
			j=j-1
		x[j+1]=current
	return x


print(Insertionsort_asc(inputlist))

```

<br/>

#### 4. Merge Sort

```python
N=int(input("배열 크기를 입력하세요: "))

inputlist=[]

for i in range(N):
	element = input("배열의 원소를 입력해 주세요: ")
	inputlist.append(element)


print(inputlist)

def Mergesort(x) :
    
    if len(x) <=1 :
        return x
    
    mid = int(len(x)//2) #split index
    left = x[:mid]
    right = x[mid:]
    
    left=Mergesort(left)
    right=Mergesort(right)

    result = []
    
    while len(left)>0 or len(right)>0 :
        
        if len(left)>0 and len(right)>0 :
            if left[0]<=right[0] :
                result.append(left[0])
                left = left[1:]
            else :
                result.append(right[0])
                right = right[1:]
                
        elif len(left)>0 :
            result.append(left[0])
            left = left[1:]
            
        else :
            result.append(right[0])
            right = right[1:]
            
    return result
       
print(Mergesort(inputlist))
```



