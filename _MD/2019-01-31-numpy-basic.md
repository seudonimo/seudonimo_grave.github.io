

1. [Numpy - Basic]
2. [Numpy - Broadcasting] - 작성 중
3. [Numpy - DL functions] - 작성 중

--------

# Numpy Basic

python에서 tensorflow등을 통해 Deep Learning 관련 연산을 할 때, 꼭 필요한 package라고 할 수 있는 numpy에 대해 정리한다. numpy가 없어도 tensorflow를 못하는건 아니지만, numpy를 통해 코드 간소화, 처리 능력이 확연히 달라지기 때문에 꼭 정리할 필요가 있다.



### numpy package
numpy는 python에서 computer sicence 관련 계산을 위한 필수적인 package이며 DL분야(?)에서도 필수(!)적인 역할을 담당한다. numpy는 아래와 같은 기능을 제공한다

> 1. powerful N-dimensional array object
> 2. Sophiscated (broadcasting) functions
> 3. tools for intergrating C/C++ and Fortran code
> 4. useful linear algebra, Fourier transform, and random number capabilities

numpy가 DL에서 많이 쓰이는 이유는 vector 연산때문이라고 할 수 있는데 실제로 for loop 보다 작은 code line, operation time으로 동작 가능하다.

------
## ndarray

### array

```
np.array()
np.zeros
np.ones
np.empty
np.arange

```



### numpy array

numpy에서 array는 동일한 자료형의 값들의 모임을 의미하고, 배열의 차원을 rank, 각 차원의 크기를 tuple로 표시하는 것을 shape라고 한다.
> 예를 들어 2 * 3의 2차원 array에서 rank는 2, shape는 (2, 3)이다.

### numpy array operation
#### basic operations
``` python
import numpy as np

x = np.array([[1, 2], [3, 4]], dtype = np.float64)
y = np.array([[5, 6], [7, 8]], dtype = np.float64)

print("x+y")
print(np.add(x, y))
#[[6, 8]
# [10, 12]]

print("x-y")
print(np.substract(x, y))
#[[-4, -4]
# [-4, -4]]
```
행렬의 +, - 연산은 예상(?)과 마찬가지로 아래와 같다.
$$
x = \left[\begin{array}{r} 1&2\\
3&4\end{array}\right], 	
y = \left[\begin{array}{r} 5&6\\
7&8\end{array}\right],
x + y = \left[\begin{array}{r} 6&8\\
10&12\end{array}\right], x - y = \left[\begin{array}{r} -4&-4\\
-4&-4\end{array}\right]
$$


#### multiplication operations

numpy package는 computer science관련 계산에 장점이 있는 만큼 곱 연산(multiplication operation) 에서 편리한 연산자를 제공한다. multiply연산은 요소 별, 혹은 성분 곱 연산을 제공하며, 행렬 곱은 dot 연산자를 통해 구할 수 있다.
$$
x = \left[\begin{array}{r} 1&2\\
3&4\end{array}\right], 	
y = \left[\begin{array}{r} 5&6\\
7&8\end{array}\right],
x * y = \left[\begin{array}{r} 5&12\\
21&32\end{array}\right], 
x ∙ y = \left[\begin{array}{r} 19&22\\
43&50\end{array}\right]
$$


```python
print('x*y")
print(np.multiply(x, y))
#[[5, 12]
# [21, 32]]

print('x dot y")
print(np.dot(x, y))
#[[19, 22]
# [43, 50]]
```

dot 연산자 덕분에 vector의 내적, 스칼라 등의 연산에 용이하게 쓰이



#### Other operations

$$

$$

```python
# 나누기
print(np.divide(x, y))
#[[0.2,, 0.33333]
# [0.42857, 0.5]]

print(np.sqrt(x))

print(x.T)
```

