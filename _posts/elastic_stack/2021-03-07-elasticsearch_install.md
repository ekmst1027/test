---
title: "[Elasticsearch] Elasticsearch 설치"
excerpt: "Elasticsearch 설치"
toc: true
toc_sticky: true

categories:
  - Elastic_Stack
  - Elasticsearch
tags:
  - Elastic_Stack
  - Elasticsearch
  - Elasticsearch install
  - 엘라스틱서치 설치
---

## Elastic Search 설치

오늘은 Elastic Stack의 심장 Elasticsearch를 간단하게 설치해보겠습니다.

2021년 2월 18일에 출시된 7.11.1 버전을 다운로드 받겠습니다.
(참고로 Elasticsearch의 버전업 속도는 매우 빠르지만 설치 방법은 거의 동일합니다.)

다운로드는 [이곳](https://www.elastic.co/kr/downloads/elasticsearch)에서 할수 있습니다.  
각자 OS에 맞게 설치해주세요.  
저는 Mac OS (Big Sur)에 설치하겠습니다.  
Mac OS로 설치 실습을 진행하므로 터미널 기반으로 설치해보겠습니다.

### 설치

먼저 설치할 디렉토리를 만들고 이동합니다.

```shell
$ mkdir elastic_stack && cd elastic_stack
```

다운로드 사이트에서 다운로드 링크 주소를 복사해 wget명령어를 이용해 다운로드합니다.

```shell
$ wget https://artifacts.elastic.co/downloads/elasticsearch/elasticsearch-7.11.1-darwin-x86_64.tar.gz
```

타르볼 파일이 받아지면 압축을 해제하고 soft link를 걸어줍니다.

```shell
$ tar -zxf elasticsearch-7.11.1-darwin-x86_64.tar.gz
$ ln -s elasticsearch-7.11.1 elasticsearch
```

다음에 버전을 update하더라도 softlink를 걸면 보다 편하게 접근할 수 있습니다.

```shell
$ cd elasticsearch
$ ls
LICENSE.txt     README.asciidoc config          lib             modules
NOTICE.txt      bin             jdk.app         logs            plugins
```

압축 해제된 디렉토리를 보면 위와 같이 여러 디렉토리 및 파일들을 볼 수 있습니다.  
이 중 주로 사용하게될 디렉토리는 _bin_ 디렉토리와 _config_ 디렉토리입니다.
먼저 _config_ 디렉토리를 살펴보겠습니다.

```shell
$ cd config
$ ls
elasticsearch.yml jvm.options.d     role_mapping.yml  users
jvm.options       log4j2.properties roles.yml         users_roles
```

elasticsearch에 관한 설정은 elasticsearch.yml파일에서 주로 설정하게 됩니다.  
클러스터 구성관련 설정, port관련 설정, host설정 등등 대부분의 설정을 할 수 있습니다.
이번에는 클러스터 구성을 하지 않을 것이고, 엘라스틱서치를 빠르게 설치하여 띄워보는 목적이기 때문에 default 상태로 설치를 진행하겠습니다.

그럼 이제 드디어 실행을 해보겠습니다.

```
$ cd elasticsearch/bin
$ ./elasticsearch
...
[2021-03-07T16:39:43,998][INFO ][o.e.l.LicenseService     ] [igyeongmin-ui-MacBook-Pro.local] license [19e6a614-1cba-42fd-9765-a498385cdc81] mode [basic] - valid
[2021-03-07T16:39:44,001][INFO ][o.e.x.s.s.SecurityStatusChangeListener] [igyeongmin-ui-MacBook-Pro.local] Active license is now [BASIC]; Security is disabled
```

실행 후에 한참 로그가 나오고 마지막쯤에는 위와 같은 로그가 나옵니다. 제대로 실행되었는지 확인하기 터미널 창을 하나 더 띄우고 curl 명령어를 사용해 확인합니다.
참고로 default로 설정했기 때문에 elasticsearch는 9200 port를 통해 접속할 수 있습니다.

```
$ curl http://localhost:9200/
{
  "name" : "igyeongmin-ui-MacBook-Pro.local",
  "cluster_name" : "elasticsearch",
  "cluster_uuid" : "BG7lKICkRJ6B0dcH6aJjvw",
  "version" : {
    "number" : "7.11.1",
    "build_flavor" : "default",
    "build_type" : "tar",
    "build_hash" : "ff17057114c2199c9c1bbecc727003a907c0db7a",
    "build_date" : "2021-02-15T13:44:09.394032Z",
    "build_snapshot" : false,
    "lucene_version" : "8.7.0",
    "minimum_wire_compatibility_version" : "6.8.0",
    "minimum_index_compatibility_version" : "6.0.0-beta1"
  },
  "tagline" : "You Know, for Search"
}
```

위와 같은 로그가 나온다면 실행 성공입니다. curl명령어 말고도 브라우저에서 localhost:9200를 입력해 확인할 수도 있습니다.  
굉장히 쉽게 설치하여 실행해봤습니다.
간단하게 테스트 목적으로 설치했기 때문에 3 Step으로 설치하고 실행까지 했습니다.

1. 홈페이지에서 elasticsearch를 다운로드 한다.
2. 압축 파일을 푼다.
3. 실행한다.

하지만 테스트 목적이 아닌 실제 운영을 위해서 클러스터를 구성하고 노드마다 역할들을 부여하는 등의 설정을 한다면 elasticsearch.yml파일의 옵션들에 대해 알아보고 적절한 값을 지정해줘야 합니다.
오늘은 간단하게 설치하여 실행하는 것에 목적을 뒀기 때문에 여기까지 진행하고 다음에 elasticsearch.yml파일의 옵션에 대해 알아보겠습니다.
바로 다음 포스트에서는 elasticsearch를 편리하게 사용하도록 도와주는 시각화 툴 Kibana를 설치해보겠습니다.

**참고자료**

- [Elasticsearch 공식 사이트](https://www.elastic.co/kr/)
- [Elasticsearch 다운로드 페이지](https://www.elastic.co/kr/downloads/elasticsearch)
