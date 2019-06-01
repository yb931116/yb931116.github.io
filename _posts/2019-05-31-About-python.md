---
layout: post
title: Python에 대하여
categories:
  - python 
# feature_image: ""
tags:
  - pypy
  - cpython
  - 파이썬
---
> 요즘 부쩍 Python을 많이 사용한다. Java코드를 보다가 오랜만에 Python코드를 보면 마치 그 느낌이 수필을 읽다가 시를 읽는 느낌이다. 그만큼이나 Python은 간결한 스타일을 지향한다.

대부분의 내용은 [위키피디아](https://ko.wikipedia.org/wiki/%ED%8C%8C%EC%9D%B4%EC%8D%AC)와 [점프 투 파이썬](https://wikidocs.net/book/1)의 내용을 기반으로 작성되었다.

### python
파이썬은 플랫폼 독립적이며, 인터프리터 방식의, 객체지향적, 동적타이핑 대화형 언어이다. 

### code style
파이썬을 사용하면서 가장 다르다고 느꼈던 것이 

1. 블록 대신 들여쓰기를 사용하는 것
2. 삼항연산자

였다.

C나 Java에서 함수, 클래스, if, for 등을 구분하기 위해 사용하는 것이 블록({})인데 Python에서는 블록을 찾아 볼 수 없다. Python에서는 블록대신 **들여쓰기**를 사용한다.


- c  
```c
int factorial(int x) {
    if(x == 0)     {
        return 1;
    }     else     {
        return x * factorial(x - 1);
    }
}
```

- python   
```python
//wikipedia의 예
def factorial(x):
    if x == 0:
        return 1
    else:
        return x * factorial(x - 1)
```

파이썬을 처음 사용하면서 다른 분이 작성한 삼항연산자를 한참을 들여다 본 경험이있다. Java에서 삼항연산자를 즐겨썼다면 처음엔 아주 헷갈릴 수 있지만, 정말 아름다운 Python의 삼항연산자를 보시라.  

- python - 삼항연산자
```python
def factorial(x):
    return 1 if x==0 else x * factorial(x - 1)
```

그냥 영어다. Python의 삼항연산자는 정말 그냥 영어문장이다.


### Interpreted language
Python은 대표적인 인터프리터 언어다. Java처럼 미리 .class파일로 컴파일한 후에 JVM이 실행하는 것이 아니라. 바로바로 Python 인터프리터가 코드를 한 줄 한 줄 읽어내려가며 실행한다. compile이 필요없으므로 코드의 수정이 빠르게 반영되고, 실행시간 역시 단축된다. 다만 성능은 조금 떨어질 수 있다.

#### Python 인터프리터의 종류
구현체라고도 불리우는 Python의 인터프리터는 종류가 어려가지이다. 
1. CPython: 가장 대표적인 python.org에서 내려받는 Python은 인터프리터가 C언어로 구현되어 있으며 구분을 위해 CPythond이라고도 불리운다.
2. PyPy: Python으로 구현한 인터프리터를 사용한다. 내부적으로 JIT(Just in Time) 컴파일러를 구현하여, 자주쓰이는 코드들을 캐싱하기때문에 더 높은 성능을 낸다.
3. JPython: Java로 구현한 인터프리터를 사용한다. JVM위에서 실행이 가능하다.

### Dynamic typing
JavaScript처럼 데이터타입을 지정하지 않는다. 그냥 `변수명 = 값`이다. 따라서
1. Python의 변수는 타입을 가지지 않으며 값자체가 타입을 가지고,
2. 변수는 그 값을 참조한다.

```python 
a = 1
b = "python"
c = [1,2,3]
```
_ _ _
 파이썬에서 `import antigravity`하면 이스터에그가 나온다!
