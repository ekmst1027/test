---
title: "[Elastic_Stack] Kibana 설치"
excerpt: "Elastic Stack을 들여다보는 창 Kibana 설치"
toc: true
toc_sticky: true

categories:
  - Elastic_Stack
  - Elasticsearch
tags:
  - Elastic_Stack
  - Elasticsearch
  - Kibana
---

## Kibana 설치

### Kibana란

> Kibana는 Elasticsearch 데이터를 시각화하고 Elastic Stack을 탐색하여 쿼리 부하 추적부터 앱을 통해 요청이 흐르는 방식에 이르기까지 모든 것을 할 수 있습니다.

위의 문구는 Elaticsearch [공식 홈페이지](https://www.elastic.co/kr/kibana)에서 Kibana 대한 설명으로 쓰여있는 문구입니다. Elastic Stack에서 시각화를 담당하는 Kibana는 Elasticsearch를 통해 구축한 Index의 data를 확인하는 기본적인 기능 뿐만 아니라 여러 시각화 그래프를 그린 후 대시보드를 만들수 있도록 지원하며 유료버전에서는 Machine Learning 등 고급 기능들을 손쉽게 사용할 수 있도록 지원합니다.

이전에 받았던 Elasticsearch의 버전과 동일하게 2020년 4월 1일에 출시된 7.6.2 버전을 다운로드 받겠습니다.  
참고로 Elasticsearch와 마찬가지로 jdk가 있어야 하며 jdk가 설치되지 않았다면 미리 설치해야 합니다.(물론 Elasticsearch도 미리 설치하여 같이 활용합니다.)

다운로드는 [이곳](https://www.elastic.co/kr/downloads/kibana)에서 할수 있습니다. 각자 OS에 맞게 설치해주세요. 참고로 저는 Mac OS에 설치합니다.

### 설치

먼저 설치할 디렉토리를 만들고 이동합니다.

```shell
$ mkdir elastic_stack && cd elastic_stack
```

다운로드 사이트에서 다운로드 링크 주소를 복사해 wget명령어를 이용해 다운로드합니다.

```shell
$ wget https://artifacts.elastic.co/downloads/kibana/kibana-7.6.2-darwin-x86_64.tar.gz
```

타르볼 파일이 받아지면 압축을 해제하고 soft link를 걸어줍니다.

```shell
$ tar -zxf kibana-7.6.2-darwin-x86_64.tar.gz
$ ln -s kibana-7.6.2-darwin-x86_64 kibana
```

다음에 버전을 update하더라도 softlink를 걸면 보다 편하게 접근할 수 있습니다.

```shell
$ cd kibana
$ ls -al
total 3432
drwxr-xr-x    18 kyeongmin  staff      576  3 26 18:41 .
drwxr-xr-x     9 kyeongmin  staff      288  5  3 01:18 ..
-rw-r--r--     1 kyeongmin  staff     2269  3 26 16:22 .i18nrc.json
-rw-r--r--     1 kyeongmin  staff    13675  3 26 16:22 LICENSE.txt
-rw-r--r--     1 kyeongmin  staff  1728134  3 26 16:22 NOTICE.txt
-rw-r--r--     1 kyeongmin  staff     4057  3 26 16:22 README.txt
drwxr-xr-x     5 kyeongmin  staff      160  3 26 16:23 bin
drwxr-xr-x     5 kyeongmin  staff      160  3 26 16:22 built_assets
drwxr-xr-x     4 kyeongmin  staff      128  3 26 16:22 config
drwxr-xr-x     2 kyeongmin  staff       64  3 26 16:22 data
drwxr-xr-x     9 kyeongmin  staff      288  3 26 16:23 node
drwxr-xr-x  1287 kyeongmin  staff    41184  3 26 16:22 node_modules
drwxr-xr-x     4 kyeongmin  staff      128  3 26 16:22 optimize
-rw-r--r--     1 kyeongmin  staff      738  3 26 16:22 package.json
drwxr-xr-x     2 kyeongmin  staff       64  3 26 16:22 plugins
drwxr-xr-x    12 kyeongmin  staff      384  3 26 16:22 src
drwxr-xr-x    11 kyeongmin  staff      352  3 26 16:22 webpackShims
drwxr-xr-x     9 kyeongmin  staff      288  3 26 16:22 x-pack
```

압축 해제된 디렉토리를 보면 위와 같이 여러 디렉토리 및 파일들을 볼 수 있습니다.  
이 중 주로 사용하게될 디렉토리는 _bin_ 디렉토리와 _config_ 디렉토리입니다.
먼저 _config_ 디렉토리를 살펴보겠습니다.

```shell
$ cd config
$ ls -al
total 24
drwxr-xr-x   4 kyeongmin  staff   128  3 26 16:22 .
drwxr-xr-x  18 kyeongmin  staff   576  3 26 18:41 ..
-rw-r--r--   1 kyeongmin  staff  3009  3 26 16:22 apm.js
-rw-r--r--   1 kyeongmin  staff  5249  3 26 16:22 kibana.yml
```

kibana 관한 설정은 kibana.yml파일에서 주로 설정하게 됩니다.  
클러스터 구성관련 설정, port관련 설정, host설정 등등 대부분의 설정을 할 수 있습니다.
elasticsearch에서도 별다른 설정을 하지 않았고 디폴트로 사용할 예정이므로 수정작업은 하지 않겠습니다.

### 실행

그럼 이제 실행을 해보겠습니다.

```
$ cd kibana/bin
$ ./kibana &
...
log   [16:22:34.150] [info][status][plugin:vega@7.6.2] Status changed from uninitialized to green - Ready
log   [16:22:38.103] [warning][reporting] Generating a random key for xpack.reporting.encryptionKey. To prevent pending reports from failing on restart, please set xpack.reporting.encryptionKey in kibana.yml
log   [16:22:38.167] [info][status][plugin:reporting@7.6.2] Status changed from uninitialized to green - Ready
log   [16:22:38.251] [info][listening] Server running at http://localhost:5601
log   [16:22:38.792] [info][server][Kibana][http] http server running at http://localhost:5601
```

background로 실행하기 위해 뒤에 &를 붙였습니다. 그럼 실행 후에 한참 로그가 나오고 마지막쯤에는 위와 같은 로그가 나옵니다. 따로 설정을 바꾸지 않았기 때문에 디폴트로 5601포트를 사용하고 있습니다. 확인을 위해 웹 브라우저에서 http://localhost:5601를 입력하고 접속해봅니다.

![kibana첫화면](/assets/images/2020-05-03-kibana-install/kibana-1.png)

위와같이 kibana화면이 나온다면 실행 성공입니다. 나중에 테스트를 할지도 모르니 Try our sample data를 클릭한 후 샘플 데이터들을 Add해줍니다.

![kibana샘플데이터](/assets/images/2020-05-03-kibana-install/kibana-2.png)

잠시 후 데이터가 Add되고 다시 접속해보면 아래와 같은 홈 화면을 볼 수 있습니다.

![kibana홈화면](/assets/images/2020-05-03-kibana-install/kibana-3.png)

많은 것을 할 수 있는 화면인데, 제가 알기로는 유료버전으로만 사용할 수 있는 것들이 있는데 30일까지는 테스트할 수 있도록 해주는것으로 알고있습니다만.. 확실하지는 않습니다. 또한 라이센스 정책에 따라 완전 오픈소스 버전이 아니더라도 basic 버전까지는 개인적으로 테스트는 가능하나 해당 버전을 이용해 수익을 창출하면 안되는 것으로 알고있습니다. Elastic 공식 홈페이지에서 라이센스 정책을 확인하거나 문의해보는것이 가장 좋습니다. 나중에라도 확실하게 알게 된다면 수정하여 올바른 정보가 되도록 하겠습니다. 이번에는 일단 설치하는데 의의를 두는 것으로 하겠습니다.
