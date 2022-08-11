---
layout: post
title:  "Python Lambda Expression"
author: "Seudonimo"
---

# Lambda Expression
Lambda Expression은 함수를 하나의 식(Expression)으로 표현한 inline function으로 단 한 줄로 파이썬에서 def로 정의된 함수와 같은 역할을 간단히 구현할 수 있으며 주로 함수의 인자로 많이 사용할 수 있다. 


## Syntax
사용 문법은 아래와 같으며 표현식의 결과값이 반환된다.
``` python
lambda arguments : expression
```

## Simple Example
### Single Argument

입력 변수 a에 10을 더한 값을 표현하는 함수는 아래와 같다.
``` python
def add_ten(a):
    return a + 10

x = add_ten(a)
```
이를 람다 표현식으로 아래처럼 표현할 수 있다.
``` python
x = lambda a : a + 10
print(x(5))
```

### Multiple arguments
람다 표현식은 여러개의 arguments를 처리할 수 있다.
```
x = lambda a, b : a*b
print(x(5, 6))
```
<br/><br/>
-------
## Power of Lambda Expression
### Multiple usage
람다 표현식의 장점은 function 내부의 inline으로 표현하는 익명함수(anonymous function)일 것이다.
아래의 예제처럼 하나의 명세로 여러가지의 function을 정의할 수 있다.
``` python
def myfunc(n):
    return lambda a: a * n

my_double = myfunc(2)
my_triple = myfunc(3)

print(my_double(10))
print(my_triple(10))
```

### Inline function as function arguments

#### List sorting key 
List의 element들이 single data가 아닌 tuple, list같은 다른 data structure인 경우, 람다 표현식을 sort하는 key arguments로 사용할 수 있다.
``` python
Li = [(1, 11), (2, 8), (4, 7), (5, 5), (3, 8)]
print(sorted(Li))
# Simple : [(1, 11), (2, 8), (3, 8), (4, 7), (5, 5)]

print(sorted(Li, key = lambda a : -a[0]))
# Reversed : [(5, 5), (4, 7), (3, 8), (2, 8), (1, 11)]

print(sorted(Li, key = lambda a : a[0]))
# key is 1st : [(1, 11), (2, 8), (3, 8), (4, 7), (5, 5)]

print(sorted(Li, key = lambda a : a[1]))
# key is 2nd : [(5, 5), (4, 7), (2, 8), (3, 8), (1, 11)]

print(sorted(Li, key = lambda a : a[0] + a[1]))
# key is sum : [(2, 8), (5, 5), (4, 7), (3, 8), (1, 11)]
```

#### Map iterator
Map을 이용해 List를 생성시, iterator로 사용할 수 있다.

``` python
list(map(lambda x: x+10, [10, 20, 30]))
# [20, 30, 40]
```

#### filter iterator
List에서 필요한 요소들만 반환할 수 있다.
``` python
li = [1, 2, 3, 4, 5, 6, 7, 8]
rslt = list(filter(lambda x : x > 4 and x < 7, li))
# [5, 6]
```

