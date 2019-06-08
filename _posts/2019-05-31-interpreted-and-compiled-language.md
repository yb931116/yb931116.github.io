---
layout: post
title: 인터프리터 언어와 컴파일 언어
categories:
  - overall
# feature_image: ""
tags:
  - 스크립트언어
---
> 학원에서 java를 배웠고, 요즘은 python과 javascript를 많이 사용하고 있다. python과 javascript는 인터프리터 언어, java는 컴파일 언어(인터프리터 언어이기도 한단다)라고 하는데, 인터프리터 언어와 컴파일 언어의 차이에 대해서 알아보자.

> 좋은 묘사들  
- []컴파일러가 번역기라면 인터프리터는 통역기](https://namu.wiki/w/%EC%BB%B4%ED%8C%8C%EC%9D%BC%EB%9F%AC?from=%EC%BB%B4%ED%8C%8C%EC%9D%BC)


### Example of Compiled/Interpreted language
1. [Compiled Language](https://en.wikipedia.org/wiki/Compiled_language)
  - C++
  - Objective-c
    - Swift
  - COBOL
  - Go
  - _C#_(to bytecode)
  - _JAVA_(to bytecode) 등

2. [Interpreted Language](https://en.wikipedia.org/wiki/Interpreted_language)
  - JavaScript
  - python
  - ruby 등

Compiled Language에 C#과 JAVA는 '(to bytecode)'라고 적어놓았는데 뒤에서 자세히 살펴보자.

### Compiled Language
compile(r)는 영어로 엮다(하는 사람), 편집하다(하는 사람)이라는 뜻을 가지고 있다. 실제 컴파일 언어는 우리가 작성한 코드 **전체**를 컴퓨터가 이해할 수 있는 언어에 가깝거나 이해할 수 있는 기계어, 어셈블리어, bytecode와 같은 다른 형태의 언어로 **컴파일**하는 과정을 거치는 언어이다. 여기서 중요한 것은 **전체**코드라는 점이다. 컴파일 언어는 우리가 작성한 코드 전체를 컴파일하여 컴퓨터가 이해할 수 있(거나 이해할 수 있는 언어에 가까운)는 언어로 바꾼다.

java와 C#이 위에서 italic처리되어 (to bytecode)라고 표현해 놓은것은 JIT(Just in Time)이라고도 불리우는 컴파일러 언어의 성격과 인터프리터 언어의 성격을 둘 다가지는 언어이기 때문이다. Java에 대해 보자면,
1. Java Compiler는 우리가 작성한 Java코드를 JVM(Java Virtual Machine)이 이해할 수 있는 bytecode형태로 컴파일한다. 
2. JVM은 컴파일러에 의해 변환된 bytecode(*.class파일)를 인터프리터로서 실행, 해석 한다.
3. Java Compiler를 통해 생성되는 bytecode는 운영체제에 관계없이 모두 같으며, 각 운영체제별 JVM이 bytecode를 환경에 맞게 해석한다.

### Interpreted Language
interpret(er)는 영어로 해석하다(하는 사람)이라는 뜻을 가지고 있다. 위에서 컴파일 언어가 컴파일러에 의해 **전체**코드를 컴파일하여 컴퓨터가 이해할 수 있는 언어로 바꾸어준다고 했는데, 인터프리터 언어는 그 컴파일의 행위를 **전체**가 아닌 **한 줄단위**로 수행한다.  


### Advantage&Disadvantage 
Compiled Language 
  - Advantage 
    - 미리 컴퓨터가 해석하기 좋은 언어로 변경해 놓기 때문에 실행속도가 인터프리터 언어에 비해 빠르다.
  - Disadvantage
    - 모든 소스코드를 통째로 컴파일하여 저급언어로(기계어)만들어야 하기 때문에 빌드타임이 오래걸린다.
    - 소스코드 수정 시에도 다시 해당 코드파일을 다시 컴파일해야 하므로 수정에도 시간이 오래걸린다.

Interpreted Language
  - Advantage
    - 따로 빌드타임에 소요되는 시간이 없으므로 신속하게 실행 가능
    - 전체 소스코드를 다시 컴파일 할 필요가 없으므로 일부 소스코드 수정이 빠르게 반영
  - Disadvantage
    - 신속한 실행은 가능하지만 실행속도(성능)은 컴파일 언어에 비해 다소 떨어짐
