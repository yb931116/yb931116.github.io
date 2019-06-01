---
layout: post
title: 'Jekyll를 이용한 GoLabs 기술 블로그 설치'
author: jason.yu
date: 2019-03-05 15:30
tags: [Jekyll,Markdown]
---

본 포스팅에서는 Windows 환경과 Linux(Centos 7) 환경에서 Jekyll 설치와 Github Pages를 이용한 무료 호스팅 방법, 로컬 구동법을 알아보고, 블로그 문서 작성을 위한 간단한 Markdown 문법을 알아봅니다.

Jekyll(지킬) 이란?
-----------
Jekyll은 정적 웹 페이지 생성기입니다. 사용자가 웹 페이지의 내용에 해당되는 마크다운 형식의 텍스트 파일을 작성하면 Jekyll은  작성 된 파일들을 모아 디자인과 기능이 적용 된 html 문서로 변환해 줍니다. Github Pages에는 Jekyll이 내장되어 있습니다. 따라서 사용자는 Jekyll로 만들어진 웹 페이지를 Github 서버에 무료로 호스팅 할 수 있습니다.

Windows 설치방법
----------
- Clone Repository<br>
적당한 경로에 GoLabs 기술 블로그 Repository를 Clone하고 해당 경로로 이동합니다.

```
git clone https://github.com/golabs7/golabs7.github.io.git

... 생략 ...

cd golabs7.github.io.git

```

- Ruby(루비) 설치<br>
gem 명령을 이용하여 Jekyll을 설치하기 위해 Ruby를 설치해줍니다.
아래 링크로 접속하여 DEVKIT(개발자도구)가 포함 된 2.5.x 이상 버전의 Ruby를 다운로드하여 설치합니다.<br>
[----링크----](https://rubyinstaller.org/downloads/)<br>
설치 패키지를 종료하기 전 화면에서 Dev Chain을 설치하겠냐는 물음에 체크하여 Dev Chain 또한 설치해줍니다.<br>
잠시 후 나타나는 cmd창에서 3을 입력하여 설치를 진행합니다.<br>
설치가 끝나면 cmd 창을 닫습니다.

- Jekyll 설치<br>
gem 명령어를 통해 Jekyll과 실행에 필요한 패키지를 설치합니다.

```
gem install jekyll

... 생략 ...

gem install bundler

... 생략 ...

bundler install (5분정도 걸립니다.)

... 생략 ...


```

- Jekyll 로컬 서버 구동

```

bundle exec jekyll serve

```

Windows에서 Jekyll 구동 시 인코딩 에러가 발생 할 수 있습니다.<br> 
에러 발생 시 콘솔창에 chcp 65001 입력 후 명령을 실행합니다.<br><br>

```
chcp 65001
bundle exec jekyll serve

```

웹 브라우저 주소창에 localhost:4000을 입력하여 서버에 접속합니다.

Linux 설치방법
----------

Linux 환경에서 설치하는 방법은 매우 간단합니다. <br>

- Clone Repository<br>
적당한 경로에 GoLabs 기술 블로그 Repository를 Clone하고 해당 경로로 이동합니다.

```
git clone https://github.com/golabs7/golabs7.github.io.git

... 생략 ...

cd golabs7.github.io.git
```


- 의존관계에 해당하는 요구조건 충족 확인

```
sudo yum install ruby ruby-dev build-essential
```

위 명령은 Jekyll 구동에 필요한 Ruby 요소들을 자동으로 확인하고 설치해줍니다.

- Jekyll 설치

```
gem install jekyll bundler
```

- Jekyll 로컬 서버 구동

```

jekyll serve

```

웹 브라우저 주소창에 localhost:4000을 입력하여 서버에 접속합니다.


블로그 내용 작성 방법
============

글 쓰기
-----

1. `_posts` 디렉토리에 `yyyy-mm-dd-slug.md` 파일로 복사(or 이동).
 - slug: 해당 포스트의 고유 키로 url의 일부로 사용. 왠만하면 특수문자없이 영문자,숫자,-(하이픈),.(점)...만 사용.
 - yyyy,mm,dd: 발행 년,월,일.
 - 참고: 최종적으로 포스트의 url(permalink)는 http://tech.inswave.com/yyyy/mm/dd/slug/
2. 파일 상단에 [front matter] 작성
 - layout: post # 레이아웃(필수). `page` 레이아웃을 사용하면 목록에 보이지 않는 글을 쓸 수 있음.
 - title: '제목' # 제목(필수)
 - author: `lastname.firstname` # 필자(필수). 왠만하면 회사 아이디(예: iolo.fitzowen) 사용
 - tags: `[tag1,tag2,tag3,...]` # 태그 목록(선택). 왠만하면 특수문자없이 영소문자,숫자,-(하이픈),.(점)...만 사용.
 - image: http://... # 커버이미지 url(선택)
 - date: `YYYY-MM-DD HH:MM:SS` # 발행일(필수)
3. 처음 글을 쓰는 필자이라면 **글쓴이 등록**(필수)
4. 유력한(?) 태그가 새로 등장했다면 **태그 등록**(선택)

필자 등록
-------

1. `_authors` 디렉토리에 `lastname.firstname.md` 이름으로 필자 정보 파일 추가
 - 참고: 최종적으로 사용자 포스트 목록 페이지의 url은 http://tech.inswave.com/authors/lastname.firstname/
2. 파일 상단에 [front matter] 작성
 - layout: author # 레이아웃(필수)
 - name: `lastname.firstname` # post의 author와 매칭(필수). 왠만하면 회사 아이디(예: iolo.fitzowen) 사용. 왠만하면 특수문자없이 영소문자,숫자,-(하이픈),.(점)...만 사용.
 - title: ... # 왠만하면 한글이름 사용( 필수)
 - image: http://... # 프로필 이미지(필수)
 - cover: http://... # 작성자 커버 이미지(선택)
3. 내용은 필요없음

태그 등록
-------

1. `_tags` 디렉토리에 `tag-name.md` 이름으로 필자 정보 파일 추가
 - 참고: 최종적으로 사용자 포스트 목록 페이지의 url은 http://tech.inswave.com/tags/tag-name/
2. 파일 상단에 [front matter] 작성
 - layout: tag # 레이아웃(필수)
 - name: `tag-name` # post의 tags 배열의 항목과 매칭(필수). 왠만하면 특수문자없이 영소문자,숫자,-(하이픈),.(점)...만 사용.
 - title: ... # 좀 더 길고 구체적인 설명(필수)
 - image: http://... # 태그 이미지(선택)
3. 내용은 필요없음


마크다운
======
텍스트 기반의 마크업언어로 2004년 존그루버에 의해 만들어졌음

헤더
----

큰제목: 문서 제목

```
This is an H1
=============
```

This is an H1
=============

작은제목: 문서 부제목

```
This is an H2
-------------
```

This is an H2
-------------

글머리: 1~6까지만 지원

```
# This is a H1
## This is a H2
### This is a H3
#### This is a H4
##### This is a H5
###### This is a H6
```
# This is a H1
## This is a H2
### This is a H3
#### This is a H4
##### This is a H5
###### This is a H6


BlockQuote
----------


이메일에서 사용하는 ```>``` 블럭인용문자를 이용한다.

```
> This is a blockqute.
```

> This is a blockqute.

이 안에서는 다른 마크다운 요소를 포함할 수 있다.

```
> ### This is a H3
> * List
>	```
>	code
>	```
```

> ### This is a H3
> * List
>	```
>	code
>	```


목록
----


순서있는 목록은 숫자와 점을 사용

```
1. 첫번째
2. 두번째
3. 세번째
```

1. 첫번째
2. 두번째
3. 세번째


순서없는 목록(글머리 기호)

```
* 빨강
  * 녹색
    * 파랑

+ 빨강
  + 녹색
    + 파랑

- 빨강
- 녹색
- 파랑
```

* 빨강
  * 녹색
    * 파랑

+ 빨강
  + 녹색
    + 파랑

- 빨강
- 녹색
- 파랑


혼합해서 사용하는 것도 가능

코드
----

4개의 공백 또는 하나의 탭으로 들여쓰기를 만나면 변환되기 시작하여 들여쓰지 않은 행을 만날때까지 변환이 계속된다.```<pre><code>  ~~~ </code></pre>```와 동일

```
This is a normal paragraph:

    This is a code block.
end code block.
```

This is a normal paragraph:

    This is a code block.
end code block.


backtick을 이용해서 코드 블럭을 표시할 수 있다.

    ```
    This is a code block.
    ```

```
This is a code block.
```

수평선
-----


아래 줄은 모두 수평선(```<hr/>```)을 만든다. 마크다운 문서를 미리보기로 출력할 때 *페이지 나누기* 용도로 많이 사용한다.

```
* * *
***
*****
- - -
---------------------------------------
```

* * *
***
*****
- - -
---------------------------------------



링크
----

* 링크

```
syntax: [Title](link)
```

syntax: [Title](link)

* 자동연결

```
<http://example.com/>
<address@example.com>
```

<http://example.com/>
<address@example.com>

강조
----

```
*single asterisks*
_single underscores_
**double asterisks**
__double underscores__
~~cancelline~~
```

*single asterisks*<br/>
_single underscores_<br/>
**double asterisks**<br/>
__double underscores__<br/>
~~cancelline~~


테이블
----

```
| foo | bar |
| --- | --- |
| baz | bim |
```

| foo | bar |
| --- | --- |
| baz | bim |


이미지
----

```
![Alt text](/path/to/img.jpg)
![Alt text](/path/to/img.jpg "Optional title")
```
![석촌호수 러버덕](http://cfile6.uf.tistory.com/image/2426E646543C9B4532C7B0)

사이즈 조절 기능은 없기 때문에 ```<img width="" height=""></img>```를 이용한다.


참고 링크
======

* [GitHub Page](https://pages.github.com/)
* [jekyll vs hexo](https://trends.google.com/trends/explore?cat=31&date=2008-01-01%202018-01-31&q=jekyll,hexo)
* [Jekyll](https://jekyllrb-ko.github.io/)
* [지킬로 깃허브에 무료 블로그 만들기](https://nolboo.kim/blog/2013/10/15/free-blog-with-github-jekyll/)
* [kakao 기술 블로그가 GitHub Pages로 간 까닭은](http://tech.kakao.com/2016/07/07/tech-blog-story/)
* [kakao 기술 블로그](http://tech.kakao.com/)
* [kakao 기술 블로그 github 저장소](https://github.com/kakao/kakao.github.io)
* [레진코믹스 기술 블로그](http://tech.lezhin.com/)
* [레진코믹스 기술 블로그 github 저장소](https://github.com/lezhin/lezhin.github.io)
* [마크다운](https://nolboo.kim/blog/2014/03/25/github-flavored-markdown/)
* [GFM Spec](https://github.github.com/gfm/)

