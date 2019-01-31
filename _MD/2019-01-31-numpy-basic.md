# Numpy Basic

python에서 tensorflow등을 통해 Deep Learning 관련 연산을 할 때, 꼭 필요한 package라고 할 수 있는 numpy에 대해 정리한다. numpy가 없어도 tensorflow를 못하는건 아니지만, numpy를 통해 코드 간소화, 처리 능력이 확연히 달라지기 때문에 꼭 정리할 필요가 있다.

##### Content
1. [Numpy - Basic]
2. [Numpy - Broadcasting]
3. [Numpy - DL functions]

### numpy package
numpy는 python에서 computer sicence 관련 계산을 위한 필수적인 package이며 DL분야(?)에서도 필수(!)적인 역할을 담당한다. numpy는 아래와 같은 기능을 제공한다

> 1. powerful N-dimensional array object
> 2. Sophiscated (broadcasting) functions
> 3. tools for intergrating C/C++ and Fortran code
> 4. useful linear algebra, Fourier transform, and random number capabilities

numpy가 DL에서 많이 쓰이는 이유는 vector 연산때문이라고 할 수 있는데 실제로 for loop 보다 작은 code line, operation time으로 동작 가능하다.

------
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

print('x*y")
print(np.multiply(x, y))
#[[5, 12]
# [21, 32]]

print('x dot y")
print(np.dot(x, y))
#[[19, 22]
# [43, 50]]

print(np.divide(x, y))
#[[0.2,, 0.33333]
# [0.42857, 0.5]]

print(np.sqrt(x))
```
Matlab과는 달리, numpy에서의 곱(multiply)는 요소별 곱이다. Numpy에선 행렬 곱(dot)을 지원하며, 덕분에 vector의 내적, 스칼라 등의 연산에 용이하다.
