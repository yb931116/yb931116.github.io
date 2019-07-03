---
title: SOLID
date: 2019-06-28 11:15:23
author: Ho9
tags:
- SOLID
- web-development
- OOP
thumbnail: posts/http.png
---


## SOLID

---

객체지향 설계 5대 원칙인 SOLID 에 대해 알아보고, 예제를 통해 학습해보자

---

<!--more -->

### 객체지향 설계 5대 원칙 SOLID

- **SRP** ( Single reponsibility principle ) - 단일 책임 원칙
- **OCP** ( Open-closed principle ) - 개방 폐쇄 원칙
- **LSP** ( Liskov substitution principle ) - 리스코브 치환 원칙
- **ISP** ( Interface segregation principle ) - 인터페이스 분리 원칙
- **DIP** ( Dependency inversion principle ) - 의존 역전 원칙


##### 1.SRP
>객체는 오직 하나의 책임을 가져야한다. ( 객체는 오직 하나의 변경의 이유만을 가져야 한다. )

예제를 통해 확인하기 전에 객체지향에서의 책임과 의존에 대해 알아야할 필요가 있다.

좋은 글이 있어서 공유합니다.
[객체지향의 올바른 이해](https://effectiveprogramming.tistory.com/entry/%EA%B0%9D%EC%B2%B4%EC%A7%80%ED%96%A5%EC%9D%98-%EC%98%AC%EB%B0%94%EB%A5%B8-%EC%9D%B4%ED%95%B4-%EC%B1%85%EC%9E%84Responsibility?category=660012)


아래의 소스예제를 보자.


**Before**

<script src="https://gist.github.com/Inhog/c117bfbaa2cbd2a85026464309b31a46.js"></script>

위의 소스의 경우, UserDataService 클래스 안에 2가지 책임 (변경의 이유 2가지)를 갖고 있다.

먼저 userData를 insert, update 하는 코드와 msg와 address를 받아서 메일을 보내는 코드를 가지고 있는데 이와 같은 경우, 메일을 보내는 코드 관련 수정사항이 발생하게 되면 클래스명을 봤을때 전혀 상관이 없는 UserDataService 클래스를 수정해야하는 상황이 발생하게 된다.

이처럼 하나의 클래스가 2가지 이상이 책임을 지니게되면 클래스의 목적이 모호해지고 ~~예를 든 경우는 코드가 간단해서 영향을 받진않지만~~ 소스가 복잡한경우에는 소스 수정시 범위가 커져서 유지보수 또한 힘들어지게된다.


**After**

<script src="https://gist.github.com/Inhog/b226df86b6ffb690375e9989987c03fe.js"></script>


위의 예를 보면, 단순하지만 하나의 클래스에 하나의 책임을 갖게끔 수정하였다. 위와같이 단일 책임 원칙을 따라서 클래스의 목적을 명확히 함으로써 구조가 복잡해지거나 수정 사항이 넓어지는 것을 예방하고 기능을 구분할 수 있게 한다.



##### 2.OCP

>객체는 확장에 대해서는 개방적이고 수정에 대해서는 폐쇄적이어야 한다는 원칙이다.

즉 기존의 코드는 변경하지 않으면서 기능을 추가할 수 있도록 설계가 되어야 한다.

대표적인 예로 도형의 넓이를 구하는 소스가 있다.

**Before**

<script src="https://gist.github.com/Inhog/cf288012ddf81997e45a00d774ac2e79.js"></script>


위의 소스의 경우 width와 height를 담을 수 있는 객체를 통해 if else 문을 통해 조건에 따라 넓이를 구하는 값이 변하는 소스이다.

위와 같은 경우, 예제와 달리 분기처리할 값이 많아진다거나 계산하는 식이 변경된다면 기존 AreaCalculator클래스의 소스를 수정하여야만 한다. 이는 수정에 대해서 폐쇄적이지 못한 소스라고 볼 수 있다.

따라서 OCP를 따르기 위해, 수정해야하는 소스를 기존 코드는 변경하지않으면서 하위클래스에서 직접 수정할 수 있도록 변경한 소스가 아래의 소스이다.

**After**

<script src="https://gist.github.com/Inhog/89f804c93d22a3ad06fbda35b96c2e49.js"></script>


##### 3.LSP

> 자식클래스는 반드시 부모클래스를 대체할 수 있어야 한다.

즉 부모클래스가 있는 자리에 자식클래스가 들어가도 계획대로 잘 작동해야 한다는 것이다. 이는 상속의 본질인데 지키지 않으면 부모 클래스 본래의 의미가 변하기 때문에 is-a 관계가 형성되지 않는다.

LSP의 **Before** 예는 OCP로 대체되었다.

OCP의 Before 소스는 넓이를 구할때 마다 대체 가능한 인스턴스를 찾아서 해당 인스턴스의 넓이를 반환하는 데, 이런 로직의 경우 자식 클래스의 인스턴스가 부모클래스의 인스턴스를 대체할 수 있는지 확인하는 소스가 있기때문에 LSP 원칙을 위배한 것이라고 볼 수 있다. (LSP 원칙에 맞게 작성하였다면, 따로 확인하는 로직이 필요없을거라는 생각이다.)

**After**
<script src="https://gist.github.com/Inhog/91fc9151919c90bce8cf7a86c9e599b5.js"></script>

~~인터페이스에서 추상클래스로만 바뀐건..~~


After 소스의 경우, 부모클래스인 Shape 추상클래스를 상속받아 추상메서드를 구현하였고 AreaCalculator 클래스의 Area 메서드를 메인에서 동작할 때 자식클래스인 Circle, Rectangle, Triangle을 부모클래스인 Shape 자리에 대체해도 계획대로 동작함을 확인할 수 있었다.

##### 4.ISP

> 클라이언트의 세분화된 내용과 같은 세분화된 인터페이스를 만들자.

> 클라이언트는 사용되지 않는 인터페이스에 의존하도록 강요해서는 안된다.

즉, 한 클래스는 자신이 사용하지 않는 인터페이스는 구현하지 말아야 한다는 원리이다. 또한 이를 방지하기위해 하나의 큰 인터페이스를 여러개의 구체적인 인터페이스로 분리하는것을 의미한다.

**Before**

<script src="https://gist.github.com/Inhog/9314eab44bfa2666af75337f3c1375de.js"></script>

위의 예를 보면, Shape를 상속받은 모든 클래스는 인터페이스에 작성되어있는 메소드를 모두 구현한 소스를 확인할 수 있다.

각 클래스는 메소드명이 일치하는 메소드만 사용된다고 했을때, 사용되지않는 메소드까지 구현을 하고있는걸 확인할 수 있다.

**After**

<script src="https://gist.github.com/Inhog/59502dac491cfce19a09332acfbf0c7a.js"></script>

각 클래스에 따라 상속할 인터페이스를 개별화 하였고, 따로 상속받아 메소드를 구현한 예이다.


##### 5.DIP

> 상위 모듈은 하위 모듈에 의존해서는 안된다. 상위 모듈과 하위 모듈 모두 추상화에 의존해야 한다.

> 추상화는 세부 사항에 의존해서는 안된다. 세부사항이 추상화에 의존해야 한다.

예제를 보면서 이해해보자.

**Example**

<script src="https://gist.github.com/Inhog/89f804c93d22a3ad06fbda35b96c2e49.js"></script>


위의 예는 OCP 원칙을 적용한 예이다. DIP 원칙을 설명하기에 적절하다고 판단하여 가지고 왔다.

AreaCalculator클래스의 Area 메서드에서 인터페이스인 Shape에 의존하면서 인터페이스를 상속받아 구현한 클래스에 의존하지 않아도 되는 소스임을 확인할 수 있다.

즉 자신보다 변하기 쉬운 것에 의존하던 것을 추상화된 인터페이스나 상위클래스로 두어 변하기 쉬운 것의 변화에 영향받지 않게 하는것 이 의존 역전 원칙이다.


#### 참고 & 출처

http://doublem.org/SOLID_SRP_OCP/
http://doublem.org/SOLID_LSP_ISP_DIP/
https://namu.wiki/w/%EA%B0%9D%EC%B2%B4%20%EC%A7%80%ED%96%A5%20%ED%94%84%EB%A1%9C%EA%B7%B8%EB%9E%98%EB%B0%8D/%EC%9B%90%EC%B9%99#s-2.3
https://karenn.tistory.com/11
