---
layout: post
title: QueryString vs PathParameter
date: 2021-05-03
category: helpful-information
author: jhhong0509
short-description: Gap between QueryString and PathParameter
---
------

# Query String vs Path Parameter

### 공통점

1. 사용자가 입력하는 데이터를 전송하는 방법중 하나.이다.
2. 미리 협의된 데이터를 URI를 통해 전송한다.
3. 길이의 제한이 있다.(URI의 최대 길이에 제한이 있다.)

### 쿼리 스트링이란?

?키=값&키=값 과 같은 형태로, 여러개의 파라미터를 전송할 수 있다.

> naver.com/post?name=홍정현&gender=male
>
> 이 URI는 post 라는 URI로 name이라는 이름의 파라미터로 홍정현 이라는 값과, gender 이라는 이름의 파라미터로 male 이라는 값이 간다.

보통 필터링을 할때 사용된다.

> 페이징 처리를 할때 페이지와 사이즈와 같은 것이 포함된다.

### Path Parameter

/값 과 같은 형태로 값을 넘긴다.

> naver.com/post/1
>
> 이 URI는 post라는 uri로 1 이라는 값을 넘겨준다.

보통 어떤 값을 특정할때 사용된다.

> 특정 게시글과 같은걸 보고싶을 때 사용된다.

/post/{type}/{id} 과 같은 형태로 한번에 여러개를 받을수도 있다.

### 차이점

1. 전송되는 형태가 다르다.
2. 사용되는 때가 다르다.