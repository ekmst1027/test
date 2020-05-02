---
title: "Elastic Search 설치"
excerpt: "Elastic Search 설치"
toc: true
toc_sticky: true

categories:
  - Elastic Stack
  - Elasticsearch
tags:
  - Elastic Stack
  - Elasticsearch
---

## Elastic Search 설치

### Elasticsearch란

> Elasticsearch는 시간이 갈수록 증가하는 문제를 처리하는 분산형 RESTful 검색 및 분석 엔진입니다. Elastic Stack의 핵심과도 같은 Elasticsearch는 데이터를 중앙에 저장하여 예상 가능한 항목을 탐색하거나 예상치 못한 항목을 밝혀낼 수 있도록 지원합니다.

위의 문구는 Elaticsearch [공식 홈페이지](https://www.elastic.co/kr/elasticsearch)에 Elasticsearch에 대한 설명으로 쓰여있는 문구입니다. 실제로 많은 회사에서도 검색엔진, 로깅, 보안 등등의 목적으로 많이 사용된다는 Elastic Stack의 심장인 Elasticsearch를 설치해보겠습니다. (우선 이번 포스트는 설치에 집중하고, 구체적인 설명은 다른 포스트를 통해 하겠습니다.)

2020년 4월 1일에 출시된 7.6.2 버전을 다운로드 받겠습니다.  
참고로 Elasticsearch는 jdk가 있어야 하며 jdk가 설치되지 않았다면 미리 설치해야 합니다.

다운로드는 [이곳](https://www.elastic.co/kr/downloads/elasticsearch)에서 할수 있습니다. 각자 OS에 맞게 설치해주세요. 참고로 저는 Mac OS에 설치합니다.

### 설치

먼저 설치할 디렉토리를 만들고 이동합니다.

```shell
$ mkdir elastic_stack && cd elastic_stack
```

다운로드 사이트에서 다운로드 링크 주소를 복사해 wget명령어를 이용해 다운로드합니다.

```shell
$ wget https://artifacts.elastic.co/downloads/elasticsearch/elasticsearch-7.6.2-darwin-x86_64.tar.gz
```

타르볼 파일이 받아지면 압축을 해제하고 soft link를 걸어줍니다.

```shell
$ tar -zxf elasticsearch-7.6.2-darwin-x86_64.tar.gz
$ ln -s elasticsearch-7.6.2 elasticsearch
```

다음에 버전을 update하더라도 softlink를 걸면 보다 편하게 접근할 수 있다.

```shell
$ cd elasticsearch
$ ls -al
total 1072
drwxr-xr-x  12 kyeongmin  staff     384  3 26 15:38 .
drwxr-xr-x   6 kyeongmin  staff     192  5  2 23:35 ..
-rw-r--r--   1 kyeongmin  staff   13675  3 26 15:28 LICENSE.txt
-rw-r--r--   1 kyeongmin  staff  523209  3 26 15:36 NOTICE.txt
-rw-r--r--   1 kyeongmin  staff    8164  3 26 15:28 README.asciidoc
drwxr-xr-x  23 kyeongmin  staff     736  3 26 15:39 bin
drwxr-xr-x   9 kyeongmin  staff     288  3 26 15:39 config
drwxr-xr-x   3 kyeongmin  staff      96  3 26 15:39 jdk.app
drwxr-xr-x  42 kyeongmin  staff    1344  3 26 15:38 lib
drwxr-xr-x   2 kyeongmin  staff      64  3 26 15:36 logs
drwxr-xr-x  38 kyeongmin  staff    1216  3 26 15:39 modules
drwxr-xr-x   2 kyeongmin  staff      64  3 26 15:36 plugins
```

압축 해제된 디렉토리를 보면 위와 같이 여러 디렉토리 및 파일들을 볼 수 있다.  
이 중 주로 자주 사용하게될 디렉토리는 _bin_ 디렉토리와 _config_ 디렉토리입니다.
먼저 _config_ 디렉토리를 살펴보겠습니다.

```shell
$ cd config
$ ls -al
total 72
drwxr-xr-x   9 kyeongmin  staff    288  5  3 00:04 .
drwxr-xr-x  12 kyeongmin  staff    384  3 26 15:38 ..
-rw-r-----   1 kyeongmin  staff   2831  3 26 15:28 elasticsearch.yml
-rw-r-----   1 kyeongmin  staff   2301  3 26 15:28 jvm.options
-rw-r-----   1 kyeongmin  staff  17545  3 26 15:36 log4j2.properties
-rw-r-----   1 kyeongmin  staff    473  3 26 15:36 role_mapping.yml
-rw-r-----   1 kyeongmin  staff    197  3 26 15:36 roles.yml
-rw-r-----   1 kyeongmin  staff      0  3 26 15:36 users
-rw-r-----   1 kyeongmin  staff      0  3 26 15:36 users_roles
```

elasticsearch에 관한 설정은 elasticsearch.yml파일에서 주로 설정하게 됩니다.  
클러스터 구성관련 설정, port관련 설정, host설정 등등 대부분의 설정을 할 수 있습니다.
이번에는 클러스터 구성을 하지 않을 것이고, 왠만한 설정은 디폴트상태로 둘 예정입니다. 하지만 data와 log 관련해서는 따로 디렉토리를 만들어서 설정하겠습니다.

```
$ vi elasticsearch.yml
# ----------------------------------- Paths ------------------------------------
# Path to directory where to store the data (separate multiple locations by comma):
#
path.data: /path/to/data
#
# Path to log files:
#
path.logs: /path/to/log
```

29라인부터 37라인까지가 data와 log 관련한 디렉토리 설정 부분입니다.
주석을 제거하시고 원하는 path로 설정하면 됩니다.

그럼 이제 드디어 실행을 해보겠습니다.

```
$ cd elasticsearch/bin
$ ./elasticsearch &
...
[2020-05-03T00:45:38,265][INFO ][o.e.x.i.a.TransportPutLifecycleAction] [igyeongmin-ui-MacBook-Pro.local] adding index lifecycle policy [watch-history-ilm-policy]
[2020-05-03T00:45:38,374][INFO ][o.e.x.i.a.TransportPutLifecycleAction] [igyeongmin-ui-MacBook-Pro.local] adding index lifecycle policy [ilm-history-ilm-policy]
[2020-05-03T00:45:38,472][INFO ][o.e.x.i.a.TransportPutLifecycleAction] [igyeongmin-ui-MacBook-Pro.local] adding index lifecycle policy [slm-history-ilm-policy]
[2020-05-03T00:45:38,674][INFO ][o.e.l.LicenseService     ] [igyeongmin-ui-MacBook-Pro.local] license [ff0c81e7-58a4-48dd-8a71-a9cc0e3731e1] mode [basic] - valid
[2020-05-03T00:45:38,675][INFO ][o.e.x.s.s.SecurityStatusChangeListener] [igyeongmin-ui-MacBook-Pro.local] Active license is now [BASIC]; Security is disabled
```

background로 실행하기 위해 뒤에 &를 붙였습니다. 그럼 실행 후에 한참 로그가 나오고 마지막쯤에는 위와 같은 로그가 나옵니다. 제대로 실행되었는지 확인하기 위해 curl 명령어를 사용해 확인합니다.

```
$ curl http://localhost:9200/
{
  "name" : "igyeongmin-ui-MacBook-Pro.local",
  "cluster_name" : "elasticsearch",
  "cluster_uuid" : "kRkRHYVARPK8_Em5gIjheA",
  "version" : {
    "number" : "7.6.2",
    "build_flavor" : "default",
    "build_type" : "tar",
    "build_hash" : "ef48eb35cf30adf4db14086e8aabd07ef6fb113f",
    "build_date" : "2020-03-26T06:34:37.794943Z",
    "build_snapshot" : false,
    "lucene_version" : "8.4.0",
    "minimum_wire_compatibility_version" : "6.8.0",
    "minimum_index_compatibility_version" : "6.0.0-beta1"
  },
  "tagline" : "You Know, for Search"
}
```

위와 같은 로그가 나온다면 실행 성공입니다. curl명령어 말고도 브라우저에서 localhost:9200를 입력해 확인할 수도 있습니다.  
참 설치까지는 굉장히 쉽습니다. 하지만 이제부터 어떻게 활용할지... 그것이 문제입니다.
그럼 다음에는 어떻게 활용하는지까지 포스팅해보도록 하겠습니다.
