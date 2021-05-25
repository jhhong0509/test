---
layout: post
title: What is DockerFile
date: 2021-05-03
category: docker
author: jhhong0509
short-description: Introduce dockerfile
---
------

# Dockerfile

### Dockerfile이란?

우리는 매번 도커 컨테이너를 생성하고, 이미지를 받아오고, 그 안에서 여러 도구를 사용하는 설정을 해왔다.

하지만 이렇게 번거로운 일을 매번마다 하는것은 매우 귀찮기 때문에, 이러한 작업을 하나의 파일로 만들어 정리하는데, 그것이 Dockerfile이다.

> Dockerfile을 작성하는것 또한 귀찮고, 짜증날 수 있다.
>
> 하지만 이러한 작업은 나중에 서비스의 장애를 줄여주는 과정이니, 그냥 하도록 하자

### Dockerfile의 작성 과정

1. Dockerfile 작성
2. 이미지 생성 실패
3. 수정
4. 이미지 생성 성공
5. 지울건 지우고, 합칠건 합쳐준다. (효율화)
6. 1번으로

### Dockerfile 작성 방법

``` docker
FROM ubuntu:latest

LABEL key=value
RUN (명령어)
RUN (명령어)

ADD 이미지
WORKDIR 디렉토리
EXPOSE 포트
CMD 명령어
```

``` dockerfile
FROM 환경:태그
```

위 문법은 최신의 ubuntu 버전에서 실행하겠다는 의미이다.

``` dockerfile
LABEL key=value
```

위 문법은 이미지에 메타데이터를 추가한다.

> 메타데이터란 어떤 목적을 가지고 만들어진 데이터를 부르는 이름이다.
>
> 일정한 규칙을 가지고 데이터마다 부여되며 수많은 데이터중 찾는 데이터를 효율적으로 검색하기 위해 사용된다.

작성자 정보, 타이틀, 버전 등 정보를 작성할 때 사용된다.

``` dockerfile
RUN (명령어)
```

위 문법은 shell script 또는 명령을 실행해 준다.

컨테이너 내부에서 명령을 실행해 준다.

>  별도의 입력(install을 할 때 설치 할지 여부를 묻는 것 처럼)을 할 수 없다.
>
>  -y 태그를 통해 미리 입력시켜 줘야 한다.

``` dockerfile
ENTRYPOINT ["<커맨드>", "<파라미터1>", "<파라미터2>"] 또는
ENTRYPOINT ["<커맨드>"]
```

컨테이너를 띄울 때 항상 실행되어야 하는 커맨드를 지정할 때 사용된다.

Docker 이미지를 하나의 실행 파일처럼 만들고 싶을 때 좋다.

> 컨테이너가 실행될때 해당 명령어가 실행되고, 프로세스가 죽을때 알아서 종료되기 때문이다.

``` dockerfile
ADD 파일 추가할 위치
```

이미지에 파일을 추가시켜 준다.

해당 파일을 설정해준 디렉토리에 추가한다.

``` dockerfile
COPY (저장될 위치 및 이름) (가져올 파일)
```

ADD 와 매우 비슷하다.

가져올 파일에서 파일을, 저장될 위치에 해당 이름으로 저장된다.

```dockerfile
WORKDIR 위치
```

명령어를 실행할 디렉토리를 설정한다.

평소에 사용하던 CD와 동일한 역할을 한다.

``` dockerfile
EXPOSE 포트
```

이미자가 노출할 포트를 설정한다.

``` dockerfile
CMD 명령어
```

컨테이너가 시작될때마다 실행될 명령어

Dockerfile에서 한번만 사용할 수 있다.

``` dockerfile
ENV 키 값
```

환경 변수 값을 세팅해 줄 수 있다.

secret key와 같은 값들을 설정해 줄 때 사용된다.

``` Dockerfile
ARG 이름=기본값
```

> 기본값은 생략 가능

docker를 build할때 해당 이름으로 값을 넣어줄 수 있다.

> docker build --build-arg 이름=값

만약 값을 넣어주지 않으면 기본값이 들어가게 된다.

설정된 값은 ${이름} 처럼 사용될 수 있다.

### docker build

- Dockerfile을 빌드하여 이미지로 만드는 것이다.

docker build -t 이름 ./ 처럼 사용할 수 있다.

> -t (-tag)는 이미지의 이름을 지정하는 것이다.
>
> > 참고로 이미지의 이름은 Docker Hub에 namespace/이름:속성 과 같은 형태로 저장된다.
> >
> > docker의 공식 이미지들은 namespace에 library가 들어가고, 유저가 만든 이미지는 namespace에 사용자의 이름이 들어가게 된다.
>
> 만약 파일 이름이 Dockerfile이 아니라면, -f 태그로 직접 지정시킬 수 있다.

> 맨 뒤에 ./는 dockerfile의 위치를 가리킨다.

.dockerignore 파일 수정을 통해 이미지를 빌드할 때 특정 디렉토리 혹은 파일을 제외시킬 수 있다.