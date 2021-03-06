---
layout: post
title: Docker database
date: 2021-05-03
category: docker
author: jhhong0509
short-description: How to connect to database when we start database on the docker
---
------

# 도커 데이터베이스

### 컨테이너 실행

데이터베이스를 도커에서 열수도 있다.

``` dockerfile
docker run -it --rm postgres
```

이렇게 데이터베이스를 열수는 있지만, localhost로 접근은 불가능하다.

도커 컨테이너는 각각 **독립된 환경**에서 실행되기 때문이다.

### 도커 데이터베이스에 연결

다른 컨테이너에서 다른 컨테이너로 연결하려면 별도의 태그 설정이 필요하다.

개별적인 컨테이너는 다른 컨테이너의 존재를 알지 못하기 때문에 `--link` 태그를 붙여줘야 한다.

> `--link` 태그는 참조할 컨테이너를 지정한다.

``` dockerfile
docker run -it --rm \
	-p 8080:8080 \
	--link DB컨테이너 \
	컨테이너
```

위와 같은 방식으로 별개의 컨테이너를 연결시켜 준다.