---
title: "[Elastic_Stack] Kibana 설치"
excerpt: "Kibana 설치"
toc: true
toc_sticky: true

categories:
  - Elastic_Stack
  - Kibana
tags:
  - Elastic_Stack
  - Kibana
  - Kibana install
  - 키바나 설치
---

## Kibana 설치

오늘은 `Elastic Stack을 들여다보는 창` Kibana를 설치해보겠습니다.

이전에 받았던 Elasticsearch의 버전과 동일하게 2021년 2월 18일에 출시된 7.11.1 버전을 다운로드 받겠습니다.  
참고로 Elasticsearch의 경우 jdk가 내장되어 있어 따로 설치가 필요하지 않지만, Kibana의 경우 jdk가 설치되어 있어야 합니다.

다운로드는 [이곳](https://www.elastic.co/kr/downloads/kibana)에서 할수 있습니다.
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
$ wget https://artifacts.elastic.co/downloads/kibana/kibana-7.11.1-darwin-x86_64.tar.gz
```

타르볼 파일이 받아지면 압축을 해제하고 soft link를 걸어줍니다.

```shell
$ tar -zxf kibana-7.11.1-darwin-x86_64.tar.gz
$ ln -s kibana-7.11.1-darwin-x86_64 kibana
```

다음에 버전을 update하더라도 softlink를 걸면 보다 편하게 접근할 수 있습니다.

```shell
$ cd kibana
$ ls
LICENSE.txt  README.txt   config       node         package.json src
NOTICE.txt   bin          data         node_modules plugins      x-pack
```

압축 해제된 디렉토리를 보면 위와 같이 여러 디렉토리 및 파일들을 볼 수 있습니다.  
이 중 주로 사용하게될 디렉토리는 _bin_ 디렉토리와 _config_ 디렉토리입니다.

kibana 관한 설정은 _config_ 디렉토리의 kibana.yml파일에서 주로 설정하게 됩니다.  
클러스터 구성관련 설정, port관련 설정, host설정 등등 대부분의 설정을 할 수 있습니다.
elasticsearch에서도 별다른 설정을 하지 않았고 디폴트로 사용할 예정이므로 수정작업은 하지 않겠습니다.

### 실행

그럼 이제 실행을 해보겠습니다.

```
$ cd kibana/bin
$ ./kibana
...
  log   [17:16:07.347] [info][listening] Server running at http://localhost:5601
  log   [17:16:08.531] [info][plugins][watcher] Your basic license does not support watcher. Please upgrade your license.
  log   [17:16:08.535] [info][crossClusterReplication][plugins] Your basic license does not support crossClusterReplication. Please upgrade your license.
  log   [17:16:08.535] [info][kibana-monitoring][monitoring][monitoring][plugins] Starting monitoring stats collection
  log   [17:16:08.567] [info][server][Kibana][http] http server running at http://localhost:5601
```

실행 후에 한참 로그가 나오고 마지막쯤에는 위와 같은 로그가 나옵니다. 따로 설정을 바꾸지 않았기 때문에 디폴트로 5601포트를 사용하고 있습니다. 확인을 위해 웹 브라우저에서 http://localhost:5601를 입력하고 접속해봅니다.

![kibana첫화면](/assets/images/2021-03-07-kibana-install/kibana-1.png)

위와같이 kibana화면이 나온다면 실행 성공입니다.
두번째 섹션의 Ingest your data의 Add data탭을 누르면 Elastic에서 제공하는 샘플 데이터를 Add 할 수 있습니다.

![kibana샘플데이터](/assets/images/2021-03-07-kibana-install/kibana-2.png)

Add data에서 맨 오른쪽 Sample data 탭을 누르고 모든 데이터를 Add 해봅니다.

![kibana메뉴화면](/assets/images/2021-03-07-kibana-install/kibana-3.png)

Add 된 데이터는 Discover 화면에서 확인이 가능합니다.
왼쪽에 햄버거 탭을 누르면 숨겨져있던 여러 메뉴들이 나오는데요, 그 중에서 Discover를 클릭해봅니다.

![kibana discover](/assets/images/2021-03-07-kibana-install/kibana-4.png)

Discover에서 Add된 데이터를 이렇게 확인할 수 있습니다.
보다 의미있고 재미있는 작업들을 하려면 먼저 Elasticsearch의 Index 개념과 Kibana의 인덱스 패턴, Time picker 조절하는 법 등등 알아야 할 부분들이 많은데요, 천천히 다음 포스팅을 통해서 설명하겠습니다.
그럼 오늘은 간략하게 Kibana를 설치해봤다는것에 의의를 두고 오늘 포스팅은 마치겠습니다.

**참고자료**

- [Kibana 다운로드 페이지](https://www.elastic.co/kr/downloads/kibana)
