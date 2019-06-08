---
layout: post
title: Http Protocol
author: Bong5
category:
  - Java
  - Keywords
  - web-development
summary: Http Protocol에 대한 간략한 요약
thumbnail: posts/http.png
---

## Http Protocol

---
웹 개발을 함에 있어 Http Servlet, Http Protocol 등 보다 원론적인 개념에 대해 많이 부족함을 느껴 다시 한번 정리하는 기회를 갖겠다.

---

### Http Protocol
 <img src="/assets/images/httpProtocol.png" width="100%" height="auto">

 <br>

 위 사진에서 잘 나타내듯 **Http Protocol**은 웹 브라우저와 웹 서버 사이에서 데이터를 요청하고 응답받기 위한 **통신 규약**으로 정의된다.

 웹 브라우저가 웹서버에 요청을 보낼 때의 HTTP protocol의 Layout은 대략적으로 아래와 같은데, 헤더 부분에서는 웹브라우저 정보, 요청 URL 등에 대한 정보가 주를 이룬다.
 - GET / HTTP / 1.1 => <u>요청 라인</u>
 - HOST : www.naver.com => <u>(일반헤더 | 요청헤더 | 엔티티헤더)</u>
 ...
 - CRLF (header와 body를 구분하기 위한 공백)
 - 메시지 본문(body부분으로 보통 POST method에서 request parameter가 표시됨)

 <br>

 또한 웹서버가 응답을 보낼 때의 HTTP protocol의 Layout을 살펴보면 마찬가지로 응답에 대한 상세 정보를 담은 헤더를 확인 할 수 있고, 메시지 본문(Body)에는 웹브라우저에 보여줄 본문 데이터, 즉 HTML이 온다.
 - HTTP/ 1.1 200 OK => HTTP 응답 코드
 - Server : nginx => (일반헤더|응답헤더|엔티티헤더)
 ...
 - CRLF
 - 메시지 본문(응답 본문, html)

 #### 예제 소스코드
 위에서 살펴본 Http protocol은 클라이언트와 서버간의 데이터를 주고받는 통신 규칙임을 알았다.
 그렇다면 누구든지 위의 규약에 맞게끔 기술만 해주고 서버에 넘겨준다면 응답을 받을수 있음을 의미한다. 이를 소스코드를 통해 한번 직접 확인해보자.

 **참고**. 현재 웹사이트 정책상 http의 취약성 때문에 대부분의(정상적이라면 전부) 웹사이트가 https 기반으로 작동하기 때문에 필자는 로컬에 간단한 http 웹페이지를 구축하여 테스트 하였다.

###### 로컬 웹페이지
 <img src="/assets/images/httpProtocol1.png" width="100%" height="auto">

 위 사진을 보면 알 수 있듯 간단한 URL을 통한 GET 요청에 대한 결과를 보여주는 웹 페이지이다. 이를 아래의 코드와 같이 HTTP Protocol 규약에 맞추어 전송을 해보자.
 <script src="https://gist.github.com/BongHoLee/b166eb81a2c332b47bc2a10dd39cf09a.js"></script>

Socket을 통해 서버(192.168.219.153)에 /home을 요청하고 그 결과를 outputStream으로 받아 출력을 해준다. 처음 설명한 내용과 전혀 다를게 없다. 그렇다면 응답의 결과는 어떨까?
 <img src="/assets/images/httpProtocol2.png" width="100%" height="auto">

 위에서 알 수 있듯 응답 요청라인, 헤더 정보와 더불어 html을 메시지 부분에 출력하여 보여준다. 이를 통해 HTTP protocol의 규약은 대략적으로 어떻게 생겨먹었고 또한 이를 어떻게 요청하고 응답받는지를 확인했다.

자 그럼 이제 HTTP Protocol에서 가장 많이 쓰이는 GET / POST에 대해 실습을 해보자.

###### GET Method
- URL?key=value&key=value 형태
- URL에 요청 파라미터가 그대로 드러난다.
- 데이터 조회(SELECT)에 적합하다.
- URL 링크 및 검색에서 주로 사용된다.
- 바이너리 및 대용량 데이터 전송이 제한된다.
  - 요청라인과 헤더 필드의 최대 크기가 제한되기 때문

 <img src="/assets/images/httpProtocol3.png" width="100%" height="auto">
  <img src="/assets/images/httpProtocol4.png" width="100%" height="auto">

위와 같이 성과 이름을 입력 후 submit을 수행하게 되면 URL에 데이터와 함께 요청되는것을 볼 수 있다. 이를 Http Proxy(charles)를 통해 Http Protocol 레이아웃으로 살펴보면

#### Request
<img src="/assets/images/httpProtocol5.png" width="100%" height="auto">

#### Response
<img src="/assets/images/httpProtocol6.png" width="100%" height="auto">

보시다시피 HTTP Protocol 요청/응답 레이아웃에 맞게 표현된 것을 확인할 수 있다.
Get 요청은 Body 없이 Header(요청 라인)에 파라미터가 표현된것에 유의하자.

###### POST Method
- GET과 달리 헤더가 아닌 메시지 Body 부분에 파라미터를 삽입하여 전송
- URL에 데이터가 포함되지 않기 때문에 최소한의 외부 노출이 방지된다. (보안에 유리한건 아니다. GET과 마찬가지로 보안에 취약)
- 메시지 Body에 데이터가 포함되기 때문에 실행 결과를 공유 불가(메일로 첨부하는 등)
- 바이너리 및 대용량 데이터 전송이 가능함.

<img src="/assets/images/httpProtocol7.png" width="100%" height="auto">
 <img src="/assets/images/httpProtocol8.png" width="100%" height="auto">

 위에서는 Post 방식으로 요청을 한 결과를 보여준다. Get방식과 달리 URL에 파라미터 데이터가 노출되지 않고 Body부에 삽입되어져 전송된다. Protocol Layout을 통해 확인해보자.

#### Request
 <img src="/assets/images/httpProtocol9.png" width="100%" height="auto">

 #### Response
  <img src="/assets/images/httpProtocol10.png" width="100%" height="auto">

  위의 Request를 보면 알 수 있듯 요청 헤더가 아닌 Body 부분에 파라미터가 삽입되어 전송되는것에 유의하자!

  #### 마무리
  지금까지 간단하게 Http Protocol Layout에 대해서 살펴보았다. 프로그래밍을 하는데에 있어 정말 간단한 부분만 다루었기 때문에 보다 더 심도있는 학습이 필수적이다.

  이후에는 Http Servlet, WAS 등이 해당 HTTP PROTOCOL을 어떻게 처리하는지에 대해서 간단하게 학습해보고 리뷰하는 기회를 갖도록 하겠다.








###참고 및 출처
  - 자바 웹개발 워크북
