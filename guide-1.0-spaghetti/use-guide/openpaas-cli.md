# OpenPaas CLi 가이드

## OpenPaas CLi 가이드.md

## 개요

### 문서 목적

본 문서는 OpenPaaS에 대한 설치 및 운영 관리를 위한 도구인 OpenPaaS CLI에 대해 기본 사용법 및 사용 예시를 통해 OpenPaaS를 이해하는데 목적이 있습니다.

### 범위

본 문서는 OpenPaaS CLI 분류 및 기본 사용법에 대해서 작성하였습니다.

### 참고 자료

본 문서는 Cloud Foundry의 CF Document를 참고로 작성하였습니다.

[_**https://docs.cloudfoundry.org/devguide/installcf/**_](https://docs.cloudfoundry.org/devguide/installcf/)

## OpenPaaS CLI기본 사용법

OpenPaaS CLI : OpenPaaS를 관리하기 위한 CLI 도구입니다.

CLI는 OpenPaaS배포와 Release를 관리하기 위해 도움을 주는 커맨드 라인 유틸리티로 사용법은 다음과 같습니다.

* **기본 Syntax**

```text
cf [global options] command <arguments...> [command options]
```

OpenPaaS command 명령어에 따라 약어를 제공해 줍니다. 예를 들어 App start CLI명령어는 start 이지만 st도 사용가능합니다.

* **약어 사용예시**

```text
$ cf start

$ cf st
```

OpenPaaS 명령어에 대괄호로 묶인 인자인 \[command options\]은 명령어에 따라 선택적으로 사용되고, command `<arguments>` 인자는 필수 인자입니다. OpenPaaS 운영 및 관리하기 위한 도구인 OpenPaaS CLI 아래와 같은 명령어들을 제공하고 있습니다.

## GETTING STARTED

### login

* **기본 Syntax**

```text
$ cf login [-a API_URL] [-u USERNAME] [-p PASSWORD] [-o ORG] [-s SPACE]
```

* **설명**

```text
OpenPaaS에 로그인 하기 위한 명령어
```

* **파라미터**

| 파라미터명 | 설명 | 필수\(O/X\) |
| :--- | :--- | :--- |
| -a API\_URL | CLI가 접속 하려는 OpenPaaS  URL Ex\) [https://api.10.244.0.34.xip.io](https://api.10.244.0.34.xip.io) | X |
| -u USERNAMEL | OpenPaaS에 접속하는 사용자 id | X |
| -p PASSWORD | OpenPaaS에 접속하는 사용자 password | X |
| -o ORG | OpenPaaS에 접속하는 사용자의 소속조직 명 | X |
| -s SPACE | OpenPaaS에 접속하는 사용자의 소속조직 스페이스직 명 | X |

* **사용예시**

```text
# 파라미터 지정한 경우
$ cf login --skip-ssl-validation -a https://api.10.244.0.34.xip.io -u admin -p admin -o crossent -s development

# 파라미터 지정하지 않을 경우
$ cf login
API endpoint: https://api.10.244.0.34.xip.io

Email> admin

Password>
Authenticating...
OK

Targeted org crossent

Select a space (or press enter to skip):
1. development
2. staged
3. oper

Space> 1
Targeted space development

API endpoint:   https://api.10.244.0.34.xip.io (API version: 2.29.0)   
User:           admin   
Org:            crossent   
Space:          development
```

### logout

* **기본 Syntax**

```text
$ cf logout
```

* **설명**

```text
cf에 logout합니다.
```

* **파라미터**

  -없음

* **사용예시**

```text
$ cf logout
```

### passwd

* **기본 Syntax**

```text
$ cf passwd
```

* **설명**

```text
OpenPaaS 사용자계정의 패스워드를 변경합니다.
```

* **파라미터**

  -없음

* **사용예시**

```text
$ cf passwd
Current Password>

New Password>

Verify Password>
Changing password...
OK
Please log in again
```

### target

* **기본 Syntax**

```text
$ cf target [-o ORG] [-s SPACE]
```

* **설명**

```text
로그인한 사용자가 사용할 Target 조직 및 스페이스 설정합니다.
```

* **파라미터**

| 파라미터명 | 설명 | 필수\(O/X\) |
| :--- | :--- | :--- |
| -o ORG | Target 조직 | X |
| -s SPACE | Target 스페이스 | X |

* **사용예시**

```text
# 파라미터 지정한 경우
$ cf target -o cf -s development
API endpoint:   https://api.10.244.0.34.xip.io (API version: 2.29.0)   
User:           admin   
Org:            cf   
Space:          development
# 파라미터 지정하지 않은 경우(현재 Target된 정보가 출력)
$ cf target
API endpoint:   https://api.10.244.0.34.xip.io (API version: 2.29.0)   
User:           admin   
Org:            cf
Space:          development
```

### api

* **기본 Syntax**

```text
$ cf api <URL>
```

* **설명**

```text
Target api를 조회하거나 target api URL을 설정합니다.
```

* **파라미터**

| 파라미터명 | 설명 | 필수\(O/X\) |
| :--- | :--- | :--- |
| URL | Api Target URL | O |

* **사용예시**

```text
$ cf api --skip-ssl-validation api.10.244.0.34.xip.io
```

### auth

* **기본 Syntax**

```text
$ cf auth <USERNAME> <PASSWORD>
```

* **설명**

```text
OpenPaaS login시 로그인만 되며 스페이스, 타겟은 지정되지 않습니다.
```

* **파라미터**

| 파라미터명 | 설명 | 필수\(O/X\) |
| :--- | :--- | :--- |
| USERNAME | 로그인 사용자 ID | O |
| PASSWORD | 로그인 사용자 PASSWORD | O |

* **사용예시**

```text
$ cf api --skip-ssl-validation api.10.244.0.34.xip.io
```

## APPS

### apps

* **기본 Syntax**

```text
$cf apps
```

* **설명**

```text
타겟 스페이스에 App 목록을 조회합니다.
```

* **파라미터**

  -없음

  * **사용예시**

  ```text
  $ cf apps
  ```

### app

* **기본 Syntax**

```text
  $cf app <APP_NAME>
```

* **설명**

```text
  App의 상태를 조회합니다.
```

* **파라미터**

| 파라미터명 | 설명 | 필수\(O/X\) |
| :--- | :--- | :--- |
| APP\_NAME | APP명 | O |

* **사용예시**

  ```text
  $ cf app spring-music
  ```

### push,p

* **기본 Syntax**

```text
  $ cf push <APP_NAME> [-b BUILDPACK_NAME] [-c COMMAND] [-d DOMAIN] [-f MANIFEST_PATH] [-i NUM_INSTANCES] [-k DISK] [-m MEMORY] [-n HOST] [-p PATH] [-s STACK] [-t TIMEOUT] [--no-hostname] [--no-manifest] [--no-route] [--no-start]
```

* **설명**

```text
  App을 OpenPaaS에 배포 하고 app을 Start합니다.
```

* **파라미터**

| 파라미터명 | 설명 | 필수\(O/X\) |
| :--- | :--- | :--- |
| APP\_NAME | push하는 App명\(지정하지 않으면 디렉토리명\) | O |
| -b BUILDPACK | custom빌드팩 URL   ex\) [https://github.com/OpenPaaSRnD/egov-java-buildpack](https://github.com/OpenPaaSRnD/egov-java-buildpack) | X |
| -c COMMAND | App start command | X |
| -d DOMAIN | App 도메인 | X |
| -f MANIFEST\_PATH | Manifest 파일 경로 | X |
| -i NUM\_INSTANCES | App 인스턴스 갯수 | X |
| -m MEMORY | 인스턴스 메모리 용량 | X |
| -k DISK | 디스크 사용 용량 | X |
| -n HOST | 호스트명   ex\) my-subdomain\) | X |
| -p PATH | App의 디렉토리 경로 또는 App file\(zip,war등\)경로 | X |
| -s STACK | App이 실행되는 운영체제 파일시스템\(default: cflinuxfs2\) | X |
| -t TIMEOUT | App이 실행되는동안 CLI가 대기하는 timeout시간 | X |
| --no-hostname | App에 root 도메인을 매핑 | X |
| --no-manifest | Manifest 파일을 무시합니다. | X |
| --no-route | Push된 앱에 라우트 정보를 삭제하고 App에 라우트 정보를 매핑하지 않음 | X |
| --no-start | App을 push하고 Start하지 않음 | X |
| --random-route | App에게 라우트 정보를 랜덤하게 생성 | X |

* **사용예시**

  ```text
  $ cf push spring-music
  ```

### scale

* **기본 Syntax**

```text
  $ cf scale <APP_NAME> [-i INSTANCES] [-k DISK] [-m MEMORY] [-f]
```

* **설명**

```text
  App의 메모리,디스크 크기 및 인스턴스 갯수를 조정합니다.
```

* **파라미터**

| 파라미터명 | 설명 | 필수\(O/X\) |
| :--- | :--- | :--- |
| APP\_NAME | APP명 | O |
| -i INSTANCES | 인스턴스 갯수 | X |
| -k DISK | 디스크 용량 | X |
| -m MEMORY | 메모리 용량 | X |
| -f | App 강제 restart | X |

* **사용예시**

  ```text
  $ cf scale spring-music -i 2 -m 512m
  ```

### delete

* **기본 Syntax**

```text
  $ cf delete <APP_NAME> [--f] [--r]
```

* **설명**

```text
  App을 삭제합니다.
```

* **파라미터**

| 파라미터명 | 설명 | 필수\(O/X\) |
| :--- | :--- | :--- |
| APP\_NAME | APP명 | O |
| --f | 확인 없이 App 삭제 | X |
| --r | App에 매핑된 라우트 정보 삭제 | X |

* **사용예시**

  ```text
  $  cf delete spring-music
  ```

### rename

* **기본 Syntax**

```text
  $ cf rename <APP_NAME> <NEW_APP_NAME>
```

* **설명**

```text
  App명을 변경합니다.
```

* **파라미터**

| 파라미터명 | 설명 | 필수\(O/X\) |
| :--- | :--- | :--- |
| APP\_NAME | APP명 | O |
| NEW\_APP\_NAME | 변경하려는 App명 | O |

* **사용예시**

  ```text
  $  cf rename spring-music new-spring-music
  ```

### start,st

* **기본 Syntax**

```text
  $ cf start <APP_NAME>
```

* **설명**

```text
  App을 기동 합니다.
```

* **파라미터**

| 파라미터명 | 설명 | 필수\(O/X\) |
| :--- | :--- | :--- |
| APP\_NAME | APP명 | O |

* **사용예시**

  ```text
  $  cf start spring-music
  ```

### stop,sp

* **기본 Syntax**

```text
  $ cf stop <APP_NAME>
```

* **설명**

```text
  App을 중지 합니다.
```

* **파라미터**

| 파라미터명 | 설명 | 필수\(O/X\) |
| :--- | :--- | :--- |
| APP\_NAME | APP명 | O |

* **사용예시**

  ```text
  $  cf stop spring-music
  ```

### restart, rs

* **기본 Syntax**

```text
  $ cf restart <APP_NAME>
```

* **설명**

```text
  App을 재기동 합니다.
```

* **파라미터**

| 파라미터명 | 설명 | 필수\(O/X\) |
| :--- | :--- | :--- |
| APP\_NAME | APP명 | O |

* **사용예시**

  ```text
  $cf restart spring-music
  ```

### restage, rg

* **기본 Syntax**

```text
  $ cf restage <APP_NAME>
```

* **설명**

```text
  App을 restage합니다.(환경변수 설정 또는 서비스 바인딩시 사용)
```

* **파라미터**

| 파라미터명 | 설명 | 필수\(O/X\) |
| :--- | :--- | :--- |
| APP\_NAME | APP명 | O |

* **사용예시**

  ```text
  $cf restage spring-music
  ```

### restart-app-instance

* **기본 Syntax**

```text
  $ cf restart-app-instance <APP_NAME> <INDEX>
```

* **설명**

```text
  App의 인스턴스중 특정 인스턴스를 재기동 합니다.
```

* **파라미터**

| 파라미터명 | 설명 | 필수\(O/X\) |
| :--- | :--- | :--- |
| APP\_NAME | APP명 | O |
| INDEX | 인스턴스 인덱스 | O |

* **사용예시**

  ```text
  $cf restart-app-instance spring-music 1
  ```

### events

* **기본 Syntax**

```text
      $ cf events <APP_NAME>
```

* **설명**

```text
    App에서 발생한 최근 Event정보를 조회합니다. (start/stop/scale등의 이력)
```

* **파라미터**

| 파라미터명 | 설명 | 필수\(O/X\) |
| :--- | :--- | :--- |
| APP\_NAME | APP명 | O |

* **사용예시**

  ```text
  $ cf events spring-music
  ```

### files

* **기본 Syntax**

```text
  $ cf files <APP_NAME> [PATH] [-i INSTANCE]
```

* **설명**

```text
  App의 file및 디렉토리 목록을 조회합니다.
```

* **파라미터**

| 파라미터명 | 설명 | 필수\(O/X\) |
| :--- | :--- | :--- |
| APP\_NAME | APP명 | O |
| PATH | APP의 디렉토리 | X |
| -i INSTANCE | App인스턴스 인덱스 | X |

* **사용예시**

  ```text
  $  cf files spring-music
  ```

### logs

* **기본 Syntax**

```text
  $ cf logs <APP_NAME> [--recent]
```

* **설명**

```text
  App에서 발생한 로그를 조회합니다.
```

* **파라미터**

| 파라미터명 | 설명 | 필수\(O/X\) |
| :--- | :--- | :--- |
| APP\_NAME | APP명 | O |
| PATH | APP의 디렉토리 | X |
| -i INSTANCE | App인스턴스 인덱스 | X |

* **사용예시**

  ```text
  $  cf logs spring-music
  ```

### env,e

* **기본 Syntax**

```text
  $ cf env  <APP_NAME>
```

* **설명**

```text
  App의 환경변수를 조회합니다.
```

* **파라미터**

| 파라미터명 | 설명 | 필수\(O/X\) |
| :--- | :--- | :--- |
| APP\_NAME | APP명 | O |

* **사용예시**

  ```text
  $ cf env spring-music
  ```

### set-env,se

* **기본 Syntax**

```text
  $ cf set-env <APP_NAME> <ENV_VAR_NAME> <ENV_VAR_VALUE>
```

* **설명**

```text
  App의 환경변수를 설정합니다. (적용시 restage필요)
```

* **파라미터**

| 파라미터명 | 설명 | 필수\(O/X\) |
| :--- | :--- | :--- |
| APP\_NAME | APP명 | O |
| ENV\_VAR\_NAME | App의 환경변수 Key | O |
| ENV\_VAR\_VALUE | App의 환경변수 Value | O |

* **사용예시**

  ```text
  $ cf se spring-music author Jim
  ```

### unset-env

* **기본 Syntax**

```text
  $ cf unset-env <APP_NAME> <ENV_VAR_NAME>
```

* **설명**

```text
  App에 설정된 환경변수를 삭제합니다.(적용시 restage필요)
```

* **파라미터**

| 파라미터명 | 설명 | 필수\(O/X\) |
| :--- | :--- | :--- |
| APP\_NAME | APP명 | O |
| ENV\_VAR\_NAME | App의 환경변수 Key | O |

* **사용예시**

  ```text
  $ cf unset-env spring-music author
  ```

### stacks

* **기본 Syntax**

```text
  $ cf stacks
```

* **설명**

```text
  OpenPaaS의 stack목록(운영체제 파일시스템) 목록을 조회합니다.
```

* **파라미터**
* 없음
* **사용예시**

  ```text
  $  cf stacks
  ```

### stack

* **기본 Syntax**

```text
  $ cf stack <STACK_NAME> [--guid]
```

* **설명**

```text
  OpenPaaS의 stack목록(운영체제 파일시스템) 목록을 조회합니다.
```

* **파라미터**

| 파라미터명 | 설명 | 필수\(O/X\) |
| :--- | :--- | :--- |
| APP\_NAME | APP명 | O |
| --guid | Stack guid를 조회 | X |

* **사용예시**

  ```text
  $  cf stack cflinuxfs2
  ```

### copy-source

* **기본 Syntax**

```text
  $ cf copy-source <SOURCE-APP> <TARGET-APP> [-o TARGET-ORG] [-s TARGET-SPACE] [--no-restart]
```

* **설명**

```text
  App의 소스를 다른 App에 복사합니다. 파일이 덥어 쓰이지 않으면 자동 restart합니다.
```

* **파라미터**

| 파라미터명 | 설명 | 필수\(O/X\) |
| :--- | :--- | :--- |
| SOURCE-APP | 원본 APP명 | O |
| TARGET-APP | 소스가 복사될 대상 App명 | X |
| -o TARGET-ORG | 타겟 조직 | O |
| -s TARGET-SPACE | 타겟 스페이스 | X |
| --no-restart | 소스 복사 후 restart하지 않음 | X |

* **사용예시**

  ```text
  $ cf copy-source spring-music another-music
  ```

### create-app-manifest

* **기본 Syntax**

```text
  $ cf create-app-manifest <APP_NAME> [-p /path/<app-name>-manifest.yml]
```

* **설명**

```text
  App의 manifest파일을 생성합니다.
```

* **파라미터**

| 파라미터명 | 설명 | 필수\(O/X\) |
| :--- | :--- | :--- |
| SOURCE-APP | 원본 APP명 | O |
| -p /path/.yml | 파일이 생성될 위치와 파일명\(-p 를 사용하지 않으면 자동생성된다\) | X |

* **사용예시**

  ```text
  $  cf create-app-manifest spring-music -p ./spring-music-manifest.yml
  ```

## SERVICES

### marketplace,m

* **기본 Syntax**

```text
  $ cf marketplace [-s SERVICE_NAME]
```

* **설명**

```text
  cf 마켓플레이스에서 제공하는 서비스 목록을 조회합니다.
```

* **파라미터**

| 파라미터명 | 설명 | 필수\(O/X\) |
| :--- | :--- | :--- |
| -s SERVICE\_NAME | 서비스의 plan이 조회된다. | X |

* **사용예시**

  ```text
  $  cf create-app-manifest spring-music -p ./spring-music-manifest.yml
  ```

### services,s

* **기본 Syntax**

```text
  $ cf services
```

* **설명**

```text
  타겟 스페이스에 서비스 인스턴스 목록을 조회합니다.
```

* **파라미터**

| 파라미터명 | 설명 | 필수\(O/X\) |
| :--- | :--- | :--- |
| -s SERVICE\_NAME | 서비스의 plan이 조회된다. | X |

* **사용예시**

  ```text
  $  cf create-app-manifest spring-music -p ./spring-music-manifest.yml
  ```

### service

* **기본 Syntax**

```text
  $ cf service <SERVICE_INSTANCE> [--guid]
```

* **설명**

```text
  서비스 인스턴스의 정보를 조회합니다.
```

* **파라미터**

| 파라미터명 | 설명 | 필수\(O/X\) |
| :--- | :--- | :--- |
| SERVICE\_INSTANCE | 서비스 인스턴스명 | O |
| --guid | 서비스 인스턴스의 Guid를 조회합니다. | X |

* **사용예시**

  ```text
  $ cf service spring-music-db
  ```

### create-service

* **기본 Syntax**

```text
  $ cf create-service <SERVICE> <PLAN> <SERVICE_INSTANCE> [-c PARAMETERS_AS_JSON] [-t TAGS]
```

* **설명**

```text
  마켓플레이스에서 제공하는 서비스로 서비스 인스턴스를 만든다.
```

* **파라미터**

| 파라미터명 | 설명 | 필수\(O/X\) |
| :--- | :--- | :--- |
| SERVICE | 마켓플레이스에 있는 서비스명 | O |
| PLAN | 서비스 플랜명 | O |
| SERVICE\_INSTANCE | 만들 서비스 인스턴스명 | O |
| -c PARAMETERS\_AS\_JSON | 서비스 설정정보를 json 형태로 입력   Ex\) -c '{"ram\_gb":4}' | X |
| -t TAGS | 서비스 인스턴스 테그 | X |

* **사용예시**

  ```text
  $ cf create-service spring-music-db silver p-mysql
  ```

### update-service

* **기본 Syntax**

```text
  $ cf update-service <SERVICE_INSTANCE> [-p NEW_PLAN] [-c PARAMETERS_AS_JSON] [-t TAGS]
```

* **설명**

```text
  서비스 인스턴스를 수정합니다.
```

* **파라미터**

| 파라미터명 | 설명 | 필수\(O/X\) |
| :--- | :--- | :--- |
| SERVICE\_INSTANCE | 서비스 인스턴스명 | O |
| -p NEW\_PLAN | 서비스 플랜명 | O |
| -c PARAMETERS\_AS\_JSON | 서비스 설정정보를 json 형태로 입력   Ex\) -c '{"ram\_gb":4}' | O |
| -t TAGS | 서비스 인스턴스 테그 | X |

* **사용예시**

  ```text
  $ cf update-service spring-music-db -p gold_plan
  ```

### delete-service

* **기본 Syntax**

```text
  $ cf delete-service SERVICE_INSTANCE [-f]
```

* **설명**

```text
  서비스 인스턴스를 삭제합니다.
```

* **파라미터**

| 파라미터명 | 설명 | 필수\(O/X\) |
| :--- | :--- | :--- |
| SERVICE\_INSTANCE | 서비스 인스턴스명 | O |
| -f | 삭제 확인 메시지 없이 서비스 인스턴스 삭제합니다. | X |

* **사용예시**

  ```text
  $ cf delete-service spring-music-db
  ```

### rename-service

* **기본 Syntax**

```text
  $ cf rename-service <SERVICE_INSTANCE> <NEW_SERVICE_INSTANCE>
```

* **설명**

```text
  서비스 인스턴스명을 수정합니다.
```

* **파라미터**

| 파라미터명 | 설명 | 필수\(O/X\) |
| :--- | :--- | :--- |
| SERVICE\_INSTANCE | 서비스 인스턴스명 | O |
| NEW\_SERVICE\_INSTANCE | 변경하려는 서비스 인스턴스명 | O |

* **사용예시**

  ```text
  $ cf rename-service spring-music-db new_spring-music-db
  ```

### create-service-key,csk

* **기본 Syntax**

```text
  $ cf create-service-key <SERVICE_INSTANCE> <SERVICE_KEY> [-c PARAMETERS_AS_JSON]
```

* **설명**

```text
  서비스 인스턴스의 key를 생성합니다.
```

* **파라미터**

| 파라미터명 | 설명 | 필수\(O/X\) |
| :--- | :--- | :--- |
| SERVICE\_INSTANCE | 서비스 인스턴스명 | O |
| SERVICE\_KEY | 서비스 인스턴스 key명 | O |
| -c PARAMETERS\_AS\_JSON | 서비스 인스턴스 설정\(JSON Parameter\) | X |

* **사용예시**

  ```text
  $ cf create-service-key spring-music-db mykey -c '{"permissions":"read-only"}'
  ```

### service-keys,sk

* **기본 Syntax**

```text
  $ cf service-keys <SERVICE_INSTANCE>
```

* **설명**

```text
  서비스 인스턴스의 key 목록을 조회합니다.
```

* **파라미터**

| 파라미터명 | 설명 | 필수\(O/X\) |
| :--- | :--- | :--- |
| SERVICE\_INSTANCE | 서비스 인스턴스명 | O |

* **사용예시**

  ```text
  $ cf service-keys spring-music-db
  ```

### service-key

* **기본 Syntax**

```text
  $ cf service-key <SERVICE_INSTANCE> <SERVICE_KEY> [--guid]
```

* **설명**

```text
  서비스 인스턴스의 key의 상세정보를 조회합니다.
```

* **파라미터**

| 파라미터명 | 설명 | 필수\(O/X\) |
| :--- | :--- | :--- |
| SERVICE\_INSTANCE | 서비스 인스턴스명 | O |
| SERVICE\_KEY | 서비스 인스턴스 key명 | O |
| --guid | 서비스 인스턴스 guid를 조회합니다. | X |

* **사용예시**

  ```text
  $ cf service-key spring-music-db mykey
  ```

### delete-service-key,dsk

* **기본 Syntax**

```text
  $ cf delete-service-key <SERVICE_INSTANCE> <SERVICE_KEY> [-f]
```

* **설명**

```text
  서비스 key를 삭제합니다.
```

* **파라미터**

| 파라미터명 | 설명 | 필수\(O/X\) |
| :--- | :--- | :--- |
| SERVICE\_INSTANCE | 서비스 인스턴스명 | O |
| SERVICE\_KEY | 서비스 인스턴스 key명 | O |
| --guid | 서비스 인스턴스 guid를 조회합니다. | X |

* **사용예시**

  ```text
  $ cf delete-service-key spring-music-db mykey
  ```

### bind-service,bs

* **기본 Syntax**

```text
  $ cf bind-service <APP_NAME> <SERVICE_INSTANCE> [-c PARAMETERS_AS_JSON]
```

* **설명**

```text
  App과 서비스 인스턴스를 바인딩합니다.<br> - 서비스 인스턴스와 APP을 바인딩해야 App에서 서비스 사용가능
```

* **파라미터**

| 파라미터명 | 설명 | 필수\(O/X\) |
| :--- | :--- | :--- |
| APP\_NAME | APP명 | O |
| SERVICE\_INSTANCE | 서비스 인스턴스 명 | O |
| -c PARAMETERS\_AS\_JSON | 바인딩 설정 파라미터 \(json형태\) | X |

* **사용예시**

  ```text
  $ cf bind-service spring-music spring-music-db -c '{"permissions":"read-only"}'

  $ cf bind-service spring-music spring-music-db -c ~/workspace/tmp/instance_config.json
  ```

### unbind-service,us

* **기본 Syntax**

```text
  $ cf unbind-service <APP_NAME> <SERVICE_INSTANCE>
```

* **설명**

```text
  App과 서비스 인스턴스를 언바인딩합니다.
```

* **파라미터**

| 파라미터명 | 설명 | 필수\(O/X\) |
| :--- | :--- | :--- |
| APP\_NAME | 서비스 인스턴스명 | O |
| SERVICE\_INSTANCE | 서비스 인스턴스 명 | O |

* **사용예시**

  ```text
  $ cf unbind-service spring-music spring-music-db
  ```

### create-user-provided-service,cups

* **기본 Syntax**

```text
  $ cf create-user-provided-service <SERVICE_INSTANCE> [-p CREDENTIALS] [-l SYSLOG-DRAIN-URL]
```

* **설명**

```text
  Market place에서 제공하는 서비스를 사용하지 않고 사용자가 별도의 서비스를 구성하여 APP과 바인딩합니다.
```

* **파라미터**

| 파라미터명 | 설명 | 필수\(O/X\) |
| :--- | :--- | :--- |
| SERVICE\_INSTANCE | 서비스 인스턴스명 | O |
| -p CREDENTIALS | 서비스 인스턴스 명 | X |
| -l SYSLOG-DRAIN-URL | 서비스 인스턴스 명 | X |

* **사용예시**

  ```text
  $ cf create-user-provided-service spring-music-db -p '{"username":"admin","password":"pa55woRD"}'
  ```

### update-user-provided-service,uups

* **기본 Syntax**

```text
  $ cf update-user-provided-service <SERVICE_INSTANCE> [-p CREDENTIALS] [-l SYSLOG-DRAIN-URL]
```

* **설명**

```text
  user-provided service instance 정보를 수정합니다.
```

* **파라미터**

| 파라미터명 | 설명 | 필수\(O/X\) |
| :--- | :--- | :--- |
| SERVICE\_INSTANCE | 서비스 인스턴스명 | O |
| -p CREDENTIALS | 서비스 인스턴스 명 | X |
| -l SYSLOG-DRAIN-URL | 서비스 인스턴스 명 | X |

* **사용예시**

  ```text
  $  cf update-user-provided-service spring-music-db -p '{"username":"admin","password":"pa55woRD"}'
  ```

## ORGS

### orgs,o

* **기본 Syntax**

```text
  $ cf orgs
```

* **설명**

```text
  조직정보 목록을 조회합니다...
```

* **파라미터**
  * 없음
* **사용예시**

  ```text
  $ cf orgs
  ```

### org

* **기본 Syntax**

```text
  $ cf org <ORG_NAME>
```

* **설명**

```text
  조직 상세 정보를 조회합니다.
```

* **파라미터**

| 파라미터명 | 설명 | 필수\(O/X\) |
| :--- | :--- | :--- |
| ORG\_NAME | 조직명 | O |
| --guid | 조직의 guid를 조회합니다. | X |

* **사용예시**

  ```text
  $ cf org cf
  ```

### create-org,co

* **기본 Syntax**

```text
  $ cf create-org <ORG_NAME> [-q QUOTA_NAME]
```

* **설명**

```text
  조직정보를 생성합니다.
```

* **파라미터**

| 파라미터명 | 설명 | 필수\(O/X\) |
| :--- | :--- | :--- |
| ORG\_NAME | 조직명 | O |
| -q QUOTA\_NAME | 조직에게 할당할 quota | X |

* **사용예시**

  ```text
  $cf create-org test -q default
  ```

### delete-org

* **기본 Syntax**

```text
  $ cf delete-org <ORG_NAME> [-f]
```

* **설명**

```text
  조직정보 목록을 조회합니다.
```

* **파라미터**

| 파라미터명 | 설명 | 필수\(O/X\) |
| :--- | :--- | :--- |
| ORG\_NAME | 조직명 | O |
| -f | 확인메시지 없이 조직정보 삭제합니다. | X |

* **사용예시**

  ```text
  $ cf delete-org cf -f
  ```

### rename-org

* **기본 Syntax**

```text
    $ cf rename-org <ORG_NAME> <NEW_ORG_NAME>
```

* **설명**

```text
  조직명을 변경합니다.
```

* **파라미터**

| 파라미터명 | 설명 | 필수\(O/X\) |
| :--- | :--- | :--- |
| ORG\_NAME | 조직명 | O |
| NEW\_ORG\_NAME | 변경할 조직명 | O |

* **사용예시**

  ```text
  $ cf rename cf new-cf
  ```

## SPACES

### spaces

* **기본 Syntax**

```text
  $ cf spaces
```

* **설명**

```text
  스페이스 목록을 가져온다.
```

* **파라미터**
  * 없음
* **사용예시**

  ```text
  $ cf spaces
  ```

### space

* **기본 Syntax**

```text
  $ cf space <SPACE_NAME>
```

* **설명**

```text
  스페이스 상세정보를 조회합니다.
```

* **파라미터**

| 파라미터명 | 설명 | 필수\(O/X\) |
| :--- | :--- | :--- |
| SPACE\_NAME | 스페이스명 | O |

* **사용예시**

  ```text
  $ cf space development
  ```

### create-space

* **기본 Syntax**

```text
  $ cf create-space <SPACE_NAME> [-o ORG_NAME] [-q SPACE-QUOTA-NAME]
```

* **설명**

```text
  스페이스 정보를 생성합니다.
```

* **파라미터**

| 파라미터명 | 설명 | 필수\(O/X\) |
| :--- | :--- | :--- |
| SPACE\_NAME | 스페이스명 | O |
| -o ORG\_NAME | 스페이스에 매핑될 조직명 | X |
| -q SPACE-QUOTA-NAME | 스페이스에 할당될 QUOTA명 | X |

* **사용예시**

  ```text
  $ cf create-space -o cf -q cf-space-quota
  ```

### delete-space

* **기본 Syntax**

```text
  $ cf delete-space <SPACE_NAME> [-f]
```

* **설명**

```text
  스페이스정보를 삭제합니다.
```

* **파라미터**

| 파라미터명 | 설명 | 필수\(O/X\) |
| :--- | :--- | :--- |
| SPACE\_NAME | 스페이스명 | O |
| -f | 삭제 확인메시지 없이 스페이스 삭제합니다. | X |

* **사용예시**

  ```text
  $ cf delete-space development
  ```

### rename-space

* **기본 Syntax**

```text
  $ cf rename-space <SPACE_NAME> <NEW_SPACE_NAME>
```

* **설명**

```text
  스페이스 명을 변경합니다.
```

* **파라미터**

| 파라미터명 | 설명 | 필수\(O/X\) |
| :--- | :--- | :--- |
| SPACE\_NAME | 스페이스명 | O |
| NEW\_SPACE\_NAME | 삭제 확인메시지 없이 스페이스 삭제합니다. | O |

* **사용예시**

  ```text
  $ cf rename-space development new_development
  ```

## DOMAINS

### domains

* **기본 Syntax**

```text
  $ cf domains
```

* **설명**

```text
  도메인 정보 목록을 조회합니다.
```

* **파라미터**
* 없음
* **사용예시**

  ```text
  $ cf domains
  ```

### create-domain

* **기본 Syntax**

```text
  $ cf create-domain <ORG_NAME> <DOMAIN>
```

* **설명**

```text
  도메인 정보 목록을 생성합니다. 생성된 도메인은 설정된 조직에서 사용가능하다.
```

* **파라미터**

| 파라미터명 | 설명 | 필수\(O/X\) |
| :--- | :--- | :--- |
| ORG\_NAME | 조직명 | O |
| DOMAIN | 도메인명 | O |

* **사용예시**

  ```text
  $ cf create-domain cf-org cf.or.kr
  ```

### delete-domain

* **기본 Syntax**

```text
  $ cf delete-domain <DOMAIN> [-f]
```

* **설명**

```text
  도메인 정보를 삭제합니다.
```

* **파라미터**

| 파라미터명 | 설명 | 필수\(O/X\) |
| :--- | :--- | :--- |
| DOMAIN | 도메인명 | O |
| -f | 삭제 확인메시지 없이 도메인을 삭제합니다. | X |

* **사용예시**

  ```text
  $ cf delete-domain cf.or.kr
  ```

### create-shared-domain

* **기본 Syntax**

```text
  $ cf create-shared-domain <DOMAIN>
```

* **설명**

```text
  공유 도메인정보를 생성한다
```

* **파라미터**

| 파라미터명 | 설명 | 필수\(O/X\) |
| :--- | :--- | :--- |
| DOMAIN | 조직명 | O |

* **사용예시**

  ```text
  $ cf create-shared-domain cf.or.kr
  ```

### delete-shared-domain

* **기본 Syntax**

```text
  $ cf delete-shared-domain <DOMAIN> [-f]
```

* **설명**

```text
  공유 도메인정보를 삭제합니다.
```

* **파라미터**

| 파라미터명 | 설명 | 필수\(O/X\) |
| :--- | :--- | :--- |
| DOMAIN | 조직명 | O |
| -f | 삭제 확인메시지 없이 도메인을 삭제합니다. | X |

* **사용예시**

  ```text
  $ cf delete-shared-domain cf.or.kr
  ```

## REOUTES

### routes, r

* **기본 Syntax**

```text
  $ cf routes
```

* **설명**

```text
  현재 조직/스페이스에 존재하는 라우트 정보목롤을 조회합니다.
```

* **파라미터**
  * 없음
* **사용예시**

  ```text
  $ cf routes
  ```

### create-route

* **기본 Syntax**

```text
  $ cf create-route <SPACE_NAME> <DOMAIN> [-n HOSTNAME]
```

* **설명**

```text
  공유 도메인정보를 삭제합니다...
```

* **파라미터**

| 파라미터명 | 설명 | 필수\(O/X\) |
| :--- | :--- | :--- |
| SPACE\_NAME | 스페이스명 | O |
| DOMAIN | 삭제 확인메시지 없이 공유 도메인을 삭제합니다.     - 도메인 정보가 입력되어있어야 합니다. | O |
| -n HOSTNAME | 호스트 명 | X |

* **사용예시**

  ```text
  $ cf create-route development cf.or.kr
  ```

### update-route

* **기본 Syntax**

```text
  $ cf update-route <SPACE_NAME> <DOMAIN> [-n HOSTNAME]
```

* **설명**

```text
  공유 도메인정보를 삭제합니다.
```

* **파라미터**

| 파라미터명 | 설명 | 필수\(O/X\) |
| :--- | :--- | :--- |
| SPACE\_NAME | 스페이스명 | O |
| DOMAIN | 삭제 확인메시지 없이 공유 도메인을 삭제합니다.     - 도메인 정보가 입력되어있어야 합니다. | O |
| -n HOSTNAME | 호스트 명 | X |

* **사용예시**

  ```text
  $ cf update-route development cf.or.kr
  ```

### check-route

* **기본 Syntax**

```text
  $ cf check-route <HOST> <DOMAIN>
```

* **설명**

```text
  라우트 정보가 존재하는지 체크합니다.
```

* **파라미터**

| 파라미터명 | 설명 | 필수\(O/X\) |
| :--- | :--- | :--- |
| HOST | 호스트 명 | O |
| DOMAIN | 삭제 확인메시지 없이 공유 도메인을 삭제합니다. | O |

* **사용예시**

  ```text
  $ cf check-route spring-music cf.or.kr
  ```

### map-route

* **기본 Syntax**

```text
  $ cf map-route <APP_NAME> <DOMAIN> [-n HOSTNAME]
```

* **설명**

```text
  App에게 URL route정보를 할당합니다.
```

* **파라미터**

| 파라미터명 | 설명 | 필수\(O/X\) |
| :--- | :--- | :--- |
| APP\_NAME | App명 | O |
| DOMAIN | App에게 할당할 도메인 | O |
| -n HOSTNAME | App에게 할당할 Host | X |

* **사용예시**

  ```text
  $ cf map-route spring-music cf.or.kr -n test
  ```

### unmap-route

* **기본 Syntax**

```text
  $ cf unmap-route <APP_NAME> <DOMAIN> [-n HOSTNAME]
```

* **설명**

```text
  App에게 URL route정보를 삭제합니다.
```

* **파라미터**

| 파라미터명 | 설명 | 필수\(O/X\) |
| :--- | :--- | :--- |
| APP\_NAME | App명 | O |
| DOMAIN | App에게 할당할 도메인 | O |
| -n HOSTNAME | App에게 할당할 Host | X |

* **사용예시**

  ```text
  $ cf unmap-route spring-music cf.or.kr -n spring-music
  ```

### delete-route

* **기본 Syntax**

```text
  $ cf delete-route <DOMAIN> [-n HOSTNAME] [-f]
```

* **설명**

```text
  App에게 URL route정보를 삭제합니다.
```

* **파라미터**

| 파라미터명 | 설명 | 필수\(O/X\) |
| :--- | :--- | :--- |
| DOMAIN | App에게 할당할 도메인 | O |
| -n HOSTNAME | App에게 할당할 Host | X |
| -f | 삭제 확인메시지 없이 라우트 정보를 삭제합니다. | X |

* **사용예시**

  ```text
  $ cf delete-route spring-music cf.or.kr -n spring-music
  ```

### delete-orphaned-routes

* **기본 Syntax**

```text
  $ cf delete-orphaned-routes [-f]
```

* **설명**

```text
  App에 매핑되지 않은 라우트 정보를 모두 삭제한다
```

* **파라미터**

| 파라미터명 | 설명 | 필수\(O/X\) |
| :--- | :--- | :--- |
| -f | 삭제 확인메시지 없이 라우트 정보를 삭제합니다. | X |

* **사용예시**

  ```text
  $ cf delete-orphaned-routes
  ```

## BUILDPACKS

### buildpacks

* **기본 Syntax**

```text
  $ cf buildpacks
```

* **설명**

```text
  빌드팩 목록을 조회합니다.
```

* **파라미터**
* 없음
* **사용예시**

  ```text
  $ cf buildpacks
  ```

### create-buildpack

* **기본 Syntax**

```text
  $ cf create-buildpack <BUILDPACK> <-p PATH> <-i POSITION> [--enable|--disable]
```

* **설명**

```text
  빌드팩을 생성합니다.
```

* **파라미터**

| 파라미터명 | 설명 | 필수\(O/X\) |
| :--- | :--- | :--- |
| BUILDPACK | 빌드팩명 | O |
| -p PATH | 빌드팩 경로 | O |
| -i POSITIONE | 빌드팩 auto-detection동안 빌드팩 체크 순서    ex\)1.2.3 | O |
| --enable | 스테이징시 사용 | X |
| --disable | 스테이징시 미사용 | X |

* **사용예시**

  ```text
  $ cf create-buildpack egov-buildpack ~/workspace/buildpack/egov -i 1
  ```

### update-buildpack

* **기본 Syntax**

```text
  $ cf update-buildpack <BUILDPACK> [-p PATH] [-i POSITION] [--enable|--disable] [--lock|--unlock]
```

* **설명**

```text
  빌드팩 정보를 수정합니다.
```

* **파라미터**

| 파라미터명 | 설명 | 필수\(O/X\) |
| :--- | :--- | :--- |
| BUILDPACK | 빌드팩명 | O |
| -p PATH | 빌드팩 경로 | O |
| -i POSITIONE | 빌드팩 auto-detection동안 빌드팩 체크 순서    ex\)1.2.3 | O |
| --enable | 스테이징시 사용 | X |
| --disable | 스테이징시 미사용 | X |

* **사용예시**

  ```text
  $ cf create-buildpack egov-buildpack ~/workspace/buildpack/egov -i 1
  ```

### delete-buildpack

* **기본 Syntax**

```text
  $ cf delete-buildpack <BUILDPACK_NAME> [-f]
```

* **설명**

```text
  빌드팩을 삭제합니다.
```

* **파라미터**

| 파라미터명 | 설명 | 필수\(O/X\) |
| :--- | :--- | :--- |
| BUILDPACK | 빌드팩명 | O |
| -f | 삭제 확인메시지 없이 빌드팩 정보를 삭제 | X |

* **사용예시**

  ```text
  $ cf delete-buildpack egov-buildpack
  ```

## USER ADMIN

### create-user

* **기본 Syntax**

```text
  $ cf create-user <USERNAME> <PASSWORD>
```

* **설명**

```text
  새로운 사용자 계정을 생성합니다.
```

* **파라미터**

| 파라미터명 | 설명 | 필수\(O/X\) |
| :--- | :--- | :--- |
| USERNAME | 사용자 ID | O |
| PASSWORD | 패스워드 | O |

* **사용예시**

  ```text
  $ cf create-user cfuser userpassword
  ```

### delete-user

* **기본 Syntax**

```text
  $ cf delete-user <USERNAME> [-f]
```

* **설명**

```text
    새로운 사용자 계정을 삭제합니다.
```

* **파라미터**

| 파라미터명 | 설명 | 필수\(O/X\) |
| :--- | :--- | :--- |
| USERNAME | 사용자 ID | O |
| -f | 삭제 확인메시지 없이 사용자 정보를 삭제 | X |

* **사용예시**

  ```text
  $ cf delete-user cfuser
  ```

### org-users

* **기본 Syntax**

```text
  $ cf org-users <ORG_NAME>
```

* **설명**

```text
  조직에 소속된 사용자를 조회합니다.
```

* **파라미터**

| 파라미터명 | 설명 | 필수\(O/X\) |
| :--- | :--- | :--- |
| ORG\_NAME | 조직명 | O |

* **사용예시**

  ```text
  $ cf org-users cforg
  ```

### set-org-role

* **기본 Syntax**

```text
  $ cf set-org-role <USERNAME> <ORG> <ROLE>
```

* **설명**

```text
  사용자에게 특정조직의 role을 설정합니다.
```

* **파라미터**

| 파라미터명 | 설명 | 필수\(O/X\) |
| :--- | :--- | :--- |
| USERNAME | 사용자명 | O |
| ORG | 조직명 | O |
| ROLE | 역할명    - OrgManager : 사용자 관리 및 plan설정/변경 권한   - BillingManager : 빌링계정 및 과금정보 생성 및 관리    - OrgAuditor : 조직 quota사용률 및 사용자 role을 조회 | O |

* **사용예시**

  ```text
  $ cf set-org-role cfuser cforg OrgManager
  ```

### unset-org-role

* **기본 Syntax**

```text
  $ cf unset-org-role <USERNAME> <ORG> <ROLE>
```

* **설명**

```text
  사용자에게 특정조직의 role을 설정을 해제합니다..
```

* **파라미터**

| 파라미터명 | 설명 | 필수\(O/X\) |
| :--- | :--- | :--- |
| USERNAME | 사용자명 | O |
| ORG | 조직명 | O |
| ROLE | 역할명    - OrgManager : 사용자 관리 및 plan설정/변경 권한   - BillingManager : 빌링계정 및 과금정보 생성 및 관리    - OrgAuditor : 조직 quota사용률 및 사용자 role을 조회 | O |

* **사용예시**

  ```text
  $ cf unset-org-role cfuser cforg OrgManager
  ```

### space-users

* **기본 Syntax**

```text
  $ cf space-users <ORG> <SPACE>
```

* **설명**

```text
  조직의 스페이스에 할당된 사용자 목록정보를 조회합니다.
```

* **파라미터**

| 파라미터명 | 설명 | 필수\(O/X\) |
| :--- | :--- | :--- |
| ORG | 조직명 | O |
| SPACE | 스페이스명 | O |

* **사용예시**

  ```text
  $ cf space-users development
  ```

### set-space-role

* **기본 Syntax**

```text
  $ cf set-space-role <USERNAME> <ORG> <SPACE> <ROLE>
```

* **설명**

```text
  사용자에게 조직의 스페이스에 role을 할당합니다.
```

* **파라미터**

| 파라미터명 | 설명 | 필수\(O/X\) |
| :--- | :--- | :--- |
| USERNAME | 사용자명 | O |
| ORG | 조직명 | O |
| SPACE | 스페이스명 | O |
| ROLE | 역할명     - SpaceManager: 스페이스의 관리자로 스페이스 내의 사용자 계정 관리 및 인스턴스 수, 서비스 바인딩 상태 및 스페이스 내의 리소스 상태를 조회 및 변경   - SpaceDeveloper: 서비스 관리로 App 배포   - SpaceAuditor: 서비스 관리로 App을 배포 | O |

* **사용예시**

  ```text
  $ cf set-space-role cfuser cforg development OrgManager
  ```

### unset-space-role

* **기본 Syntax**

```text
  $ cf unset-space-role <USERNAME> <ORG> <SPACE> <ROLE>
```

* **설명**

```text
  사용자에게 조직의 스페이스에 role을 회수합니다.
```

* **파라미터**

| 파라미터명 | 설명 | 필수\(O/X\) |
| :--- | :--- | :--- |
| USERNAME | 사용자명 | O |
| ORG | 조직명 | O |
| SPACE | 스페이스명 | O |
| ROLE | 역할명     - SpaceManager: 스페이스의 관리자로 스페이스 내의 사용자 계정 관리 및 인스턴스 수, 서비스 바인딩 상태 및 스페이스 내의 리소스 상태를 조회.   - SpaceDeveloper: 서비스 관리로 App 배포   - SpaceAuditor: 스페이스 내의 서비스 바인딩, 인스턴스 수, app사용률등을 조회 | O |

* **사용예시**

  ```text
  $ cf unset-space-role cfuser cforg development OrgManager
  ```

## ORG ADMIN

### quotas

* **기본 Syntax**

```text
  $ cf quotas
```

* **설명**

```text
  Quota 목록을 조회합니다.
```

* **파라미터**
  * 없음
* **사용예시**

  ```text
  $ cf quotas
  ```

### quota

* **기본 Syntax**

```text
  $ cf quota <QUOTA>
```

* **설명**

```text
  Quota의 상세정보를 조회합니다.
```

* **파라미터**

| 파라미터명 | 설명 | 필수\(O/X\) |
| :--- | :--- | :--- |
| USERNAME | QUOTA명 | O |

* **사용예시**

  ```text
  $ cf quota cf-quota
  ```

### set-quota

* **기본 Syntax**

```text
  $ cf set-quota <ORG> <QUOTA>
```

* **설명**

```text
  조직에게 QUOTA를 할당합니다.
```

* **파라미터**

| 파라미터명 | 설명 | 필수\(O/X\) |
| :--- | :--- | :--- |
| ORG | 직명 | O |
| QUOTA | QUOTA명 | O |

* **사용예시**

  ```text
  $ cf set-quota cf-quota
  ```

### create-quota

* **기본 Syntax**

```text
  $ cf create-quota <QUOTA> [-m TOTAL_MEMORY] [-i INSTANCE_MEMORY] [-r ROUTES] [-s SERVICE_INSTANCES] [--allow-paid-service-plans]
```

* **설명**

```text
  Quota정보를 생성합니다.
```

* **파라미터**

| 파라미터명 | 설명 | 필수\(O/X\) |
| :--- | :--- | :--- |
| QUOTA | QUOTA명 | O |
| -m TOTAL\_MEMORY | 메모리 할당량    Ex\) 1024M, 1G, 10G | X |
| -i INSTANCE\_MEMORY | App instance가 가질수 있는 최대할당량 \(-1은 무한대\)    Ex\) 1024M, 1G, 10G | X |
| -r ROUTES | 최대 라우트 수 | X |
| -s SERVICE\_INSTANCES | 최대 서비스 인스턴스 수 | X |
| --allow-paid-service-plans | 과금 서비스 plan 사용가능 | X |

* **사용예시**

  ```text
  $ cf create-quota cf-quota -m 500m -i 256m -r 2000 -s 500
  ```

### delete-quota

* **기본 Syntax**

```text
  $ cf delete-quota <QUOTA> [-f]
```

* **설명**

```text
  Quota정보를 삭제합니다.
```

* **파라미터**

| 파라미터명 | 설명 | 필수\(O/X\) |
| :--- | :--- | :--- |
| QUOTA | QUOTA명 | O |
| -f | 삭제 확인메시지 없이 QUOTA 정보를 삭제 | X |

* **사용예시**

  ```text
  $ cf delete-quota cf-quota
  ```

### update-quota

* **기본 Syntax**

```text
  $ cf update-quota <QUOTA> [-m TOTAL_MEMORY] [-i INSTANCE_MEMORY][-n NEW_NAME] [-r ROUTES] [-s SERVICE_INSTANCES] [--allow-paid-service-plans | --disallow-paid-service-plans]
```

* **설명**

```text
  Quota정보를 수정합니다.
```

* **파라미터**

| 파라미터명 | 설명 | 필수\(O/X\) |
| :--- | :--- | :--- |
| QUOTA | QUOTA명 | O |
| -m TOTAL\_MEMORY | 메모리 할당량    Ex\) 1024M, 1G, 10G | X |
| -i INSTANCE\_MEMORY | App instance가 가질수 있는 최대할당량 \(-1은 무한대\)    Ex\) 1024M, 1G, 10G | X |
| -n NEW\_NAME | QUOTA명 변경시 변경할 이름 | X |
| -r ROUTES | 최대 라우트 수 | X |
| -s SERVICE\_INSTANCES | 최대 서비스 인스턴스 수 | X |
| --allow-paid-service-plans | 과금 서비스 plan 사용가능 | X |
| --disallow-paid-service-plans | 과금 서비스 plan 사용 불가 | X |

* **사용예시**

  ```text
  $ cf update-quota cf-quota -m 500m -i 256m -r 2000 -s 500
  ```

### shared-private-domain

* **기본 Syntax**

```text
  $ cf shared-private-domain <ORG> <DOMAIN>
```

* **설명**

```text
  private도메인을 다른 조직과 공유합니다.
```

* **파라미터**

| 파라미터명 | 설명 | 필수\(O/X\) |
| :--- | :--- | :--- |
| QUOTA | QUOTA명 | O |
| DOMAIN | 도메인명 | O |

* **사용예시**

  ```text
  $ cf shared-private-domain cf-org sharedomain.or.kr
  ```

### unshared-private-domain

* **기본 Syntax**

```text
  $ cf unshared-private-domain <ORG> <DOMAIN>
```

* **설명**

```text
  다른 조직과 share한 도메인 정보를 unshare합니다.
```

* **파라미터**

| 파라미터명 | 설명 | 필수\(O/X\) |
| :--- | :--- | :--- |
| ORG | 도메인명 | O |
| DOMAIN | 도메인명 | O |

* **사용예시**

  ```text
  $ cf unshared-private-domain cf-org sharedomain.or.kr
  ```

## SPACE ADMIN

### space-quotas

* **기본 Syntax**

```text
  $ cf space-quotas
```

* **설명**

```text
  Space-quota정보 목록을 조회합니다.
```

* **파라미터**
* 없음
* **사용예시**

  ```text
  $ cf space-quotas
  ```

### space-quota

* **기본 Syntax**

```text
  $ cf space-quota <SPACE_QUOTA_NAME>
```

* **설명**

```text
  Space quota 상세정보를 조회합니다.
```

* **파라미터**

| 파라미터명 | 설명 | 필수\(O/X\) |
| :--- | :--- | :--- |
| SPACE\_QUOTA\_NAME | 스페이스 QUOTA명 | O |

* **사용예시**

  ```text
  $ cf space-quota cf-space-quota
  ```

### create-space-quota

* **기본 Syntax**

```text
  $ cf create-space-quota <QUOTA> [-i INSTANCE_MEMORY] [-m MEMORY] [-r ROUTES] [-s SERVICE_INSTANCES] [--allow-paid-service-plans]
```

* **설명**

```text
  스페이스 Quota정보를 생성합니다.
```

* **파라미터**

| 파라미터명 | 설명 | 필수\(O/X\) |
| :--- | :--- | :--- |
| QUOTA | QUOTA명 | O |
| -m TOTAL\_MEMORY | 메모리 할당량    Ex\) 1024M, 1G, 10G | X |
| -i INSTANCE\_MEMORY | App instance가 가질수 있는 최대할당량 \(-1은 무한대\)    Ex\) 1024M, 1G, 10G | X |
| -r ROUTES | 최대 라우트 수 | X |
| -s SERVICE\_INSTANCES | 최대 서비스 인스턴스 수 | X |
| --allow-paid-service-plans | 과금 서비스 plan 사용가능 | X |

* **사용예시**

  ```text
  $ cf create-space-quota cf-space-quota -i 2G -m 10G -r 3000 -s 200
  ```

### update-space-quota

* **기본 Syntax**

```text
      $ cf update-space-quota <SPACE-QUOTA-NAME> [-i MAX-INSTANCE-MEMORY] [-m MEMORY] [-n NEW_NAME] [-r ROUTES] [-s SERVICES] [--allow-paid-service-plans | --disallow-paid-service-plans]
```

* **설명**

```text
  스페이스 Quota정보를 수정합니다.
```

* **파라미터**

| 파라미터명 | 설명 | 필수\(O/X\) |
| :--- | :--- | :--- |
| SPACE-QUOTA-NAME | 스페이스 QUOTA명 | O |
| -i MAX-INSTANCE-MEMORY | App instance가 가질수 있는 최대할당량 \(-1은 무한대\)    Ex\) 1024M, 1G, 10G | X |
| -m MEMORY | 스페이스가 가질수 있는 최대 메모리 | X |
| -n NEW\_NAME | 변경하려는 SPACE-QUOTA명 | X |
| -r ROUTES | 스페이스가 가지는 최대 route 갯수 | X |
| -s SERVICES | 스페이스가 가지는 최대 서비스 인스턴스 갯수 | X |
| --allow-paid-service-plans | 과금 서비스 plan 사용가능 | X |
| --disallow-paid-service-plans | 과금 서비스 plan 사용 불가 | X |

* **사용예시**

  ```text
  $ cf update-space-quota cf-space-quota -i 2G -m 10G -r 3000 -s 200
  ```

### delete-space-quota

* **기본 Syntax**

```text
  $ cf delete-space-quota <SPACE-QUOTA-NAME>
```

* **설명**

```text
  스페이스 Quota정보를 삭제합니다.
```

* **파라미터**

| 파라미터명 | 설명 | 필수\(O/X\) |
| :--- | :--- | :--- |
| SPACE-QUOTA-NAME | 스페이스 QUOTA명 | O |
| -f | 삭제 확인메시지 없이 SPACE-QUOTA 정보를 삭제 | X |

* **사용예시**

  ```text
  $ cf delete-space-quota cf-space-quota
  ```

### set-space-quota

* **기본 Syntax**

```text
  $ cf set-space-quota <SPACE-NAME> <SPACE-QUOTA-NAME>
```

* **설명**

```text
  스페이스에 quota를 할당합니다.
```

* **파라미터**

| 파라미터명 | 설명 | 필수\(O/X\) |
| :--- | :--- | :--- |
| SPACE-NAME | 스페이스명 | O |
| SPACE-QUOTA-NAME | 스페이스 Quota명 | O |

* **사용예시**

  ```text
  $ cf set-space-quota development cf-space-quota
  ```

### unset-space-quota

* **기본 Syntax**

```text
  $ cf unset-space-quota SPACE QUOTA
```

* **설명**

```text
  스페이스에 할당된 quota를 회수합니다.
```

* **파라미터**

| 파라미터명 | 설명 | 필수\(O/X\) |
| :--- | :--- | :--- |
| SPACE | 스페이스명 | O |
| QUOTA | 스페이스 Quota명 | O |

* **사용예시**

  ```text
  $ cf unset-space-quota development cf-space-quota
  ```

## SERVICE ADMIN

### service-auth-tokens

* **기본 Syntax**

```text
  $ cf service-auth-tokens
```

* **설명**

```text
  서비스 인증 토큰 목록을 조회합니다.
```

* **파라미터**
  * 없음
* **사용예시**

  ```text
  $ cf service-auth-token
  ```

### create-service-auth-token

* **기본 Syntax**

```text
  $ cf create-service-auth-token <LABEL> <PROVIDER> <TOKEN>
```

* **설명**

```text
  스페이스에 할당된 quota를 회수합니다.
```

* **파라미터**

| 파라미터명 | 설명 | 필수\(O/X\) |
| :--- | :--- | :--- |
| LABEL | 서비스 토큰 라벨 | O |
| PROVIDER | 서비스 제공자 | O |
| TOKEN | 토큰명 | O |

* **사용예시**

  ```text
  $ cf create-service-auth-token token-label mysql token
  ```

### update-service-auth-token

* **기본 Syntax**

```text
  $ cf update-service-auth-token <LABEL> <PROVIDER> <TOKEN>
```

* **설명**

```text
  Service auth token 정보를 수정합니다.
```

* **파라미터**

| 파라미터명 | 설명 | 필수\(O/X\) |
| :--- | :--- | :--- |
| LABEL | 서비스 토큰 라벨 | O |
| PROVIDER | 서비스 제공자 | O |
| TOKEN | 토큰명 | O |

* **사용예시**

  ```text
  $ cf update-service-auth-token token-label mysql token
  ```

### delete-service-auth-token

* **기본 Syntax**

```text
  $ cf delete-service-auth-token <LABEL> <PROVIDER> [-f]
```

* **설명**

```text
  Service auth token 정보를 삭제합니다.
```

* **파라미터**

| 파라미터명 | 설명 | 필수\(O/X\) |
| :--- | :--- | :--- |
| LABEL | 서비스 토큰 라벨 | O |
| PROVIDER | 서비스 제공자 | O |
| -f | 삭제 확인메시지 없이 SERVICE TOKEN 정보를 삭제 | X |

* **사용예시**

  ```text
  $ cf delete-service-auth-token token-label mysql
  ```

### service-brokers

* **기본 Syntax**

```text
  $ cf delete-service-auth-token <LABEL> <PROVIDER> [-f]
```

* **설명**

```text
  Service Broker정보 목록을 조회합니다.
```

* **파라미터**
  * 없음
* **사용예시**

  ```text
  $ cf service-brokers
  ```

### create-service-broker

* **기본 Syntax**

```text
  $ cf create-service-broker <SERVICE_BROKER> <USERNAME> <PASSWORD> <URL>
```

* **설명**

```text
  Service Broker정보를 등록합니다.
```

* **파라미터**

| 파라미터명 | 설명 | 필수\(O/X\) |
| :--- | :--- | :--- |
| SERVICE\_BROKERABEL | 서비스 브로커명 | O |
| USERNAME | 사용자명 | O |
| PASSWORD | 패스워드 | O |
| URL | 서비스 브로커 URL | O |

* **사용예시**

  ```text
  $ cf create-service-broker mysql-service-broker admin password http://p-mysql.10.244.0.34.xip.io
  ```

### update-service-broker

* **기본 Syntax**

```text
  $ cf update-service-broker <SERVICE_BROKER> <USERNAME> <PASSWORD> <URL>
```

* **설명**

```text
  Service Broker정보를 등록합니다.
```

* **파라미터**

| 파라미터명 | 설명 | 필수\(O/X\) |
| :--- | :--- | :--- |
| SERVICE\_BROKERABEL | 서비스 브로커명 | O |
| USERNAME | 사용자명 | O |
| PASSWORD | 패스워드 | O |
| URL | 서비스 브로커 URL | O |

* **사용예시**

  ```text
  $ cf update-service-broker mysql-service-broker admin password http://p-mysql.10.244.0.34.xip.io
  ```

### delete-service-broker

* **기본 Syntax**

```text
  $ cf delete-service-broker <SERVICE_BROKER> [-f]
```

* **설명**

```text
  Service Broker정보를 삭제합니다.
```

* **파라미터**

| 파라미터명 | 설명 | 필수\(O/X\) |
| :--- | :--- | :--- |
| SERVICE\_BROKER | 서비스 브로커명 | O |
| -f | 삭제 확인메시지 없이 SERVICE BROKER 정보를 삭제 | X |

* **사용예시**

  ```text
  $ cf delete-service-broker mysql-service-broker
  ```

### rename-service-broker

* **기본 Syntax**

```text
  $ cf rename-service-broker <SERVICE_BROKER> <NEW_SERVICE_BROKER>
```

* **설명**

```text
  Service Broker명을 수정합니다.
```

* **파라미터**

| 파라미터명 | 설명 | 필수\(O/X\) |
| :--- | :--- | :--- |
| SERVICE\_BROKER | 서비스 브로커명 | O |
| NEW\_SERVICE\_BROKER | 변경할 서비스 브로커명 | O |

* **사용예시**

  ```text
  $ cf rename-service-broker mysql-service-broker new_mysql-service-broker
  ```

### migrate-service-broker

* **기본 Syntax**

```text
  $ cf migrate-service-instances <v1_SERVICE> <v1_PROVIDER> <v1_PLAN> <v2_SERVICE> <v2_PLAN>
```

* **설명**

```text
  서비스 인스턴스에서 사용하는 서비스 및 플랜을 다른 플랜으로 변경합니다. <br> - App이 사용하는 서비스를 다른 서비스로 변경하려 할때 사용합니다.
```

* **파라미터**

| 파라미터명 | 설명 | 필수\(O/X\) |
| :--- | :--- | :--- |
| v1\_SERVICE | 기존 서비스 명 | O |
| v1\_PROVIDER | 기존 서비스를 제공하는 제공자 | O |
| v1\_PLAN | 기존 서비스 인스턴스에서 사용하는 플랜 | O |
| v2\_SERVICE | 신규 서비스 명 | O |
| v2\_PLAN | 신규 서비스에서 사용하는 플랜 | O |

* **사용예시**

  ```text
  $ cf migrate-service-instances p-mysql mysql-provider silver  postgres silver
  ```

### purge-service-offering

* **기본 Syntax**

```text
  $ cf purge-service-offering <SERVICE> [-p PROVIDER]
```

* **설명**

```text
  cf와 서비스 브로커간의 정보 불일치를 해결할때 사용합니다. <br>   (migrate-service-instances 명령 이후 사용)
```

* **파라미터**

| 파라미터명 | 설명 | 필수\(O/X\) |
| :--- | :--- | :--- |
| SERVICE | 서비스 명 | O |
| -p PROVIDER | 서비스 제공자 | O |
| -f | 삭제 확인메시지 없이 서비스 정보를 삭제한다 | O |

* **사용예시**

  ```text
  $ cf purge-service-offering mysql
  ```

### service-access

* **기본 Syntax**

```text
  $ cf service-access
```

* **설명**

```text
  서비스 access 될 서비스 목록 조회합니다..
```

* **파라미터**
* 없음
* **사용예시**

  ```text
  $ cf service-access
  ```

### enable-service-access

* **기본 Syntax**

```text
  $ cf enable-service-access <SERVICE> [-p PLAN] [-o ORG]
```

* **설명**

```text
  조직 또는 서비스 plan을 서비스에 접근 가능하도록 설정합니다.
```

* **파라미터**

| 파라미터명 | 설명 | 필수\(O/X\) |
| :--- | :--- | :--- |
| SERVICE | 서비스 명 | O |
| -p PLAN | PLAN명 | O |
| -o ORG | 조직명 | O |

* **사용예시**

  ```text
  $ cf enable-service-access mysql -p silver -o cf-org
  ```

### disable-service-access

* **기본 Syntax**

```text
  $ cf disable-service-access <SERVICE> [-p PLAN] [-o ORG]
```

* **설명**

```text
  조직 또는 서비스 plan을 서비스에 접근 불가 하도록 설정합니다.
```

* **파라미터**

| 파라미터명 | 설명 | 필수\(O/X\) |
| :--- | :--- | :--- |
| SERVICE | 서비스 명 | O |
| -p PLAN | PLAN명 | O |
| -o ORG | 조직명 | O |

* **사용예시**

  ```text
  $ cf disable-service-access mysql -p silver -o cf-org
  ```

## SECURITY GROUP

### security-group

* **기본 Syntax**

```text
  $ cf security-group <SECURITY_GROUP>
```

* **설명**

```text
  시큐리티 그룹 상세정보를 조회합니다.
```

* **파라미터**

| 파라미터명 | 설명 | 필수\(O/X\) |
| :--- | :--- | :--- |
| SECURITY\_GROUP | 서큐리티 그룹명 | O |

* **사용예시**

  ```text
  $ cf security-group cf-security-group
  ```

### security-groups

* **기본 Syntax**

```text
  $ cf security-groups
```

* **설명**

```text
  시큐리티 그룹 목록을 조회합니다.
```

* **파라미터**
* 없음
* **사용예시**

  ```text
  $ cf security-groups
  ```

### create-security-group

* **기본 Syntax**

```text
  $ cf create-security-group <SECURITY_GROUP> <PATH_TO_JSON_RULES_FILE>
```

* **설명**

```text
  시큐리티 그룹정보를 생성합니다.
```

* **파라미터**

| 파라미터명 | 설명 | 필수\(O/X\) |
| :--- | :--- | :--- |
| SECURITY\_GROUP | 서큐리티 그룹명 | O |
| PATH\_TO\_JSON\_RULES\_FILE | 시큐리티 룰을 명세한 JSON 파일의 경로 및 파일명  ex\) rule 파일 작성 예제   \[     {         "protocol": "tcp",           "destination": "10.244.1.18",           "ports": "3306"    }   \] | O |

* **사용예시**

  ```text
  $ cf create-security-group cf-security-group ./rule.json
  ```

### update-security-group

* **기본 Syntax**

```text
  $ cf update-security-group <SECURITY_GROUP> <PATH_TO_JSON_RULES_FILE>
```

* **설명**

```text
  시큐리티 그룹정보를 수정합니다.
```

* **파라미터**

| 파라미터명 | 설명 | 필수\(O/X\) |
| :--- | :--- | :--- |
| SECURITY\_GROUP | 서큐리티 그룹명 | O |
| PATH\_TO\_JSON\_RULES\_FILE | 시큐리티 룰을 명세한 JSON 파일의 경로 및 파일명  ex\) rule 파일 작성 예제   \[     {         "protocol": "tcp",           "destination": "10.244.1.18",           "ports": "3306"    }   \] | O |

* **사용예시**

  ```text
  $ cf update-security-group cf-security-group ./rule.json
  ```

### delete-security-group

* **기본 Syntax**

```text
  $ cf delete-security-group <SECURITY_GROUP> [-f]
```

* **설명**

```text
  시큐리티 그룹정보를 삭제합니다.
```

* **파라미터**

| 파라미터명 | 설명 | 필수\(O/X\) |
| :--- | :--- | :--- |
| SECURITY\_GROUP | 서큐리티 그룹명 | O |
| -f | 삭제 확인메시지 없이 시큐리지 그룹 정보를 삭제합니다. | X |

* **사용예시**

  ```text
  $ cf update-security-group cf-security-group ./rule.json
  ```

### bind-security-group

* **기본 Syntax**

```text
  $ cf bind-security-group <SECURITY_GROUP> <ORG> <SPACE>
```

* **설명**

```text
  시큐리티 그룹 정보와 스페이스를 바인드 합니다.
```

* **파라미터**

| 파라미터명 | 설명 | 필수\(O/X\) |
| :--- | :--- | :--- |
| SECURITY\_GROUP | 서큐리티 그룹명 | O |
| ORG | 조직명 | O |
| SPACE | 스페이스명 | O |

* **사용예시**

  ```text
  $ cf update-security-group cf-security-group ./rule.json
  ```

### unbind-security-group

* **기본 Syntax**

```text
  $ cf unbind-security-group <SECURITY_GROUP> <ORG> <SPACE>
```

* **설명**

```text
  시큐리티 그룹 정보와 스페이스를 언바인드 합니다.
```

* **파라미터**

| 파라미터명 | 설명 | 필수\(O/X\) |
| :--- | :--- | :--- |
| SECURITY\_GROUP | 서큐리티 그룹명 | O |
| ORG | 조직명 | O |
| SPACE | 스페이스명 | O |

* **사용예시**

  ```text
  $ cf unbind-security-group cf-security-group cf-group development
  ```

### bind-staging-security-group

* **기본 Syntax**

```text
  $ cf bind-staging-security-group <SECURITY_GROUP>
```

* **설명**

```text
  App staging처리를 하기 위해 시큐리티 그룹을 설정합니다.
```

* **파라미터**

| 파라미터명 | 설명 | 필수\(O/X\) |
| :--- | :--- | :--- |
| SECURITY\_GROUP | 서큐리티 그룹명 | O |

* **사용예시**

  ```text
  $ cf bind-staging-security-group cf-security-group
  ```

### staging-security-groups

* **기본 Syntax**

```text
  $ cf staging-security-groups
```

* **설명**

```text
  Staging security group 정보 목록을 조회합니다.
```

* **파라미터**
  * 없음
* **사용예시**

  ```text
  $ cf staging-security-groups
  ```

### unbind-staging-security-group

* **기본 Syntax**

```text
  $ cf unbind-staging-security-group <SECURITY_GROUP>
```

* **설명**

```text
  App staging처리를 하기 위한 시큐리티 그룹을 설정을 해제 합니다.
```

* **파라미터**

| 파라미터명 | 설명 | 필수\(O/X\) |
| :--- | :--- | :--- |
| SECURITY\_GROUP | 서큐리티 그룹명 | O |

* **사용예시**

  ```text
  $ cf unbind-staging-security-group cf-security-group
  ```

### running-security-groups

* **기본 Syntax**

```text
  $ cf unbind-staging-security-group <SECURITY_GROUP>
```

* **설명**

```text
  실행중인 시큐리트 그룹 목록을 조회합니다.
```

* **파라미터**
  * 없음
* **사용예시**

  ```text
  $ cf unbind-staging-security-group cf-security-group
  ```

## ENVIRONMENT VARIABLE GROUPS

### running-environment-variable-group, revg

* **기본 Syntax**

```text
  $ cf running-environment-variable-group
```

* **설명**

```text
  실환경변수 내용을 조회합니다.
```

* **파라미터**
  * 없음
* **사용예시**

  ```text
  $ cf running-environment-variable-group
  ```

### staging-environment-variable-group, sevg

* **기본 Syntax**

```text
  $ cf staging-environment-variable-group
```

* **설명**

```text
  스테이징시 사용되는 환경변수 내용을 조회합니다.
```

* **파라미터**
  * 없음
* **사용예시**

  ```text
  $ cf staging-environment-variable-group
  ```

### set-staging-environment-variable-group, ssevg

* **기본 Syntax**

```text
  $ cf set-staging-environment-variable-group <ENV_VARIABLE>
```

* **설명**

```text
  스테이징시 사용되는 환경변수 내용을 설정한다
```

* **파라미터**

| 파라미터명 | 설명 | 필수\(O/X\) |
| :--- | :--- | :--- |
| ENV\_VARIABLE | 환경변수 내용으로 KEY/VALUE로 구성 | O |

* **사용예시**

  ```text
  $ cf set-staging-environment-variable-group '{"name":"value","name":"value"}'
  ```

### set-running-environment-variable-group, ssevg

* **기본 Syntax**

```text
  $ cf set-running-environment-variable-group <ENV_VARIABLE>
```

* **설명**

```text
  환경변수 내용을 설정 합니다.
```

* **파라미터**

| 파라미터명 | 설명 | 필수\(O/X\) |
| :--- | :--- | :--- |
| ENV\_VARIABLE | 환경변수 내용으로 KEY/VALUE로 구성된다. | O |

* **사용예시**

  ```text
  $ cf set-running-environment-variable-group '{"name":"value","name":"value"}'
  ```

## FEATURE FLAGS

### feature-flags

* **기본 Syntax**

```text
  $ cf feature-flags
```

* **설명**

```text
  feature flags 목록을 조회합니다.
```

* **파라미터**
  * 없음
* **사용예시**

  ```text
  $ cf feature-flags
  ```

### feature-flag

* **기본 Syntax**

```text
  $ cf feature-flag <FEATURE_NAME>
```

* **설명**

```text
  특정 Feature flag의 상태를 조회합니다.
```

* **파라미터**

| 파라미터명 | 설명 | 필수\(O/X\) |
| :--- | :--- | :--- |
| FEATURE\_NAME | Feature flag 명.   - feature flag에는 6가지가 있다.   1\)user\_org\_creation   2\) private\_domain\_creation   3\) app\_bits\_upload   4\) app\_scaling    5\) route\_creation   6\) service\_instance\_creation | O |

* **사용예시**

  ```text
  $ cf feature-flag app_bits_upload
  ```

### enable-feature-flag

* **기본 Syntax**

```text
  $ cf enable-feature-flag <FEATURE_NAME>
```

* **설명**

```text
  특정 Feature flag의 상태를 enable로 변경합니다.
```

* **파라미터**

| 파라미터명 | 설명 | 필수\(O/X\) |
| :--- | :--- | :--- |
| FEATURE\_NAME | Feature flag 명.   - feature flag에는 6가지가 있다.   1\)user\_org\_creation   2\) private\_domain\_creation   3\) app\_bits\_upload   4\) app\_scaling    5\) route\_creation   6\) service\_instance\_creation | O |

* **사용예시**

  ```text
  $ cf enable-feature-flag app_bits_upload
  ```

### disable-feature-flag

* **기본 Syntax**

```text
  $ cf disable-feature-flag <FEATURE_NAME>
```

* **설명**

```text
  특정 Feature flag의 상태를 disable로 변경합니다.
```

* **파라미터**

| 파라미터명 | 설명 | 필수\(O/X\) |
| :--- | :--- | :--- |
| FEATURE\_NAME | Feature flag 명.   - feature flag에는 6가지가 있다.   1\)user\_org\_creation   2\) private\_domain\_creation   3\) app\_bits\_upload   4\) app\_scaling    5\) route\_creation   6\) service\_instance\_creation | O |

* **사용예시**

  ```text
  $ cf disable-feature-flag app_bits_upload
  ```

## ADVANCE

### curl

* **기본 Syntax**

```text
  $ cf curl <PATH> [-i] [-v] [-X METHOD] [-H HEADER] [-d DATA] [--output FILE]
```

* **설명**

```text
  OpenPaaS CLI명령어가 아닌 OpenPaaS API를 호출합니다.
```

* **파라미터**

| 파라미터명 | 설명 | 필수\(O/X\) |
| :--- | :--- | :--- |
| PATH | Cf api path    Ex\) /v2/spaces/2d94e7ee-9805-408d-a1eb-ceac319e603b/summary | O |
| -i | Response header포함한 결과 | X |
| -v | Request/response에 CF\_TRACE enable된 내용 포함 | X |
| -X METHOD | HTTP method\(\(GET,POST,PUT,DELETE,etc\) | X |
| -H HEADER | Request에 Custom Header를 포함합니다. | X |
| -d DATA | Request에 Http data를 포함합니다. | X |
| --output FILE | Response결과를 stdout대신 FILE로 결과 저장 | X |

* **사용예시**

  ```text
  $ cf curl /v2/spaces/2d94e7ee-9805-408d-a1eb-ceac319e603b/summar
  ```

### config

* **기본 Syntax**

```text
  $ cf config [--async-timeout TIMEOUT_IN_MINUTES] [--trace true | false | path/to/file] [--color true | false] [--locale (LOCALE | CLEAR)]
```

* **설명**

```text
  CF CLI에 대한 설정.
```

* **파라미터**

| 파라미터명 | 설명 | 필수\(O/X\) |
| :--- | :--- | :--- |
| --async-timeout TIMEOUT\_IN\_MINUTES | CLI 명령 전송시 async timeout 설정 | X |
| --trace \(true / false / path/to/file   \) | CLI 명령 수행시 실행되는 cf api의 내용 출력 설정 | X |
| --color true / false | CLI 명령 수행시 실행되는 cf api의 내용 color 설정 | X |
| --locale \(LOCALE / CLEAR\) | CLI 명령 수행시 실행되는 cf api의 내용 locale 설정 | X |

* **사용예시**

  ```text
  $ cf curl /v2/spaces/2d94e7ee-9805-408d-a1eb-ceac319e603b/summar
  ```

### oauth-token

* **기본 Syntax**

```text
  $ cf oauth-token
```

* **설명**

```text
  사용자가 cf login후 CF에서 받은 token 값 조회합니다.
```

* **파라미터**
  * 없음
* **사용예시**

  ```text
  $cf oauth-token
  ```

## ADD/REMOVE PLUGIN REPOSITORY

### add-plugin-repo

* **기본 Syntax**

```text
  $ cf add-plugin-repo <REPO_NAME> <URL>
```

* **설명**

```text
  OpenPaaS CLI plugin repository(저장소)를 추가합니다.
```

* **파라미터**

| 파라미터명 | 설명 | 필수\(O/X\) |
| :--- | :--- | :--- |
| REPO\_NAME | Repository 명 | X |
| URL | Repository URL | X |

* **사용예시**

  ```text
  cf add-plugin-repo Diego-SSH http://plugins.cloudfoundry.org
  ```

### remove-plugin-repo

* **기본 Syntax**

```text
  $ cf remove-plugin-repo <REPO_NAME> <URL>
```

* **설명**

```text
  CLI plugin repository(저장소)를 삭제합니다.
```

* **파라미터**

| 파라미터명 | 설명 | 필수\(O/X\) |
| :--- | :--- | :--- |
| REPO\_NAME | Repository 명 | O |
| URL | Repository URL | O |

* **사용예시**

  ```text
  cf remove-plugin-repo Diego-SSH http://plugins.cloudfoundry.org
  ```

### list-plugin-repos

* **기본 Syntax**

```text
  $ cf list-plugin-repos
```

* **설명**

```text
  CLI에 추가된 plugin repository(저장소)목록을 조회합니다.
```

* **파라미터**
  * 없음
* **사용예시**

  ```text
  $cf list-plugin-repos
  ```

### repo-plugins

* **기본 Syntax**

```text
  $ cf repo-plugins [-r REPO_NAME]
```

* **설명**

```text
  Repository에 있는 플러그인 목록을 조회합니다.
```

* **파라미터**

| 파라미터명 | 설명 | 필수\(O/X\) |
| :--- | :--- | :--- |
| REPO\_NAME | Repository 명 | X |

* **사용예시**

  ```text
  $ cf repo-plugins
  ```

## ADD/REMOVE PLUGIN

### plugins

* **기본 Syntax**

```text
  $ cf plugins
```

* **설명**

```text
  추가된 plugin의 사용가능한 명령어 목록을 조회합니다.
```

* **파라미터**

| 파라미터명 | 설명 | 필수\(O/X\) |
| :--- | :--- | :--- |
| REPO\_NAME | Repository 명 | X |

* **사용예시**

  ```text
  $ cf repo-plugins
  ```

### install-plugin

* **기본 Syntax**

```text
  $ cf install-plugin < URL or LOCAL-PATH/TO/PLUGIN> [-r REPO_NAME]
```

* **설명**

```text
  추가된 plugin의 사용가능한 명령어 목록을 조회합니다.
```

* **파라미터**

| 파라미터명 | 설명 | 필수\(O/X\) |
| :--- | :--- | :--- |
| URL or LOCAL-PATH/TO/PLUGIN | Plugin URL 또는 로컬경로 또는 repository에 있는 플러그인명 | X |
| -r REPO\_NAME | Plugin repository명 | X |

* **사용예시**

  ```text
  $cf install-plugin 'Usage Report' -r CF-Community
  ```

