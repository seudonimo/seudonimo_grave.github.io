---
layout: post
title:  "Big-O Notation"
author: "Seudonimo"
tags: Big-O algorithm 코테
---

# Big-O Notation
Computer Science분야에서 알고리즘이란 어떤 문제를 해결하기 위한 방법이고, 이 문제를 해결하기 위한 방법은 아주 다양하다. 이 다양한 방법들 중에서 어떤 방법이 좋은지를 비교하기 위해서 알고리즘마다 시간복잡도(Time Complexity), 공간복잡도(Space Complexity)를 계산해서 효율성을 예측할 수 있는데, 이중 시간복잡도를 계산하는 방법들중 가장 많이 쓰이는 방법이 바로 Big-O 표기법이다. 



## Features

### 상수항 무시
Big-O Notation은 입력하는 data의 양이 충분히 크다고 가정하며, 알고리즘의 성능은 입력 데이터의 양(n)에 따라 영향받는다고 가정하기때문에, 상수항 같은 부분은 무시한다
$$
O(2N) => O(N)
$$

### 작은 지수항 무시

 Big-O Notation은 n이 충분히 많다고 생각하기 때문에 가장 영향력이 큰 지수항 외의 다른 작은 항들은 무시한다.
$$
O(N^3 + 100N^2 + 1000) => O(N^3)
$$


### Big-O별 실행 속도

실행속도는 아래의 순서대로 빠르다
$$
O(1) > O(log_{}{N}) > O(N) > O({N}log_{}{N}) > O(N^2)>  O(a^N) > O(N!)
$$
그래프로 비교하면 아래와 같다.

![](img\Big-O_1.jpeg)

-----

## 예제

1. **O(1)**

   ```python
   def example(n):
   	for i in range(1000):
       	print(i)
   
   ```

   

2. **O(n)**

   ```python
   def example(n):
       for i in range(n):
       	print(n)
   
   ```

   

3. **O(log2n)**

   ```python
   def example(n):
       for i in range(0, n, i*2):
       	print(n)
   
   ```

   

4. **O(n^2)**

   ```python
   def example(n):
   	for i in range(n):
           for j in range(n):
               print(i*j)
   ```

   