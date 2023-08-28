## TL;DR

```shell
apt install software-properties-common
add-apt-repository ppa:rabbitmq/rabbitmq-erlang
apt update && apt upgrade
apt install erlang
apt install elixir
apt install inotify-tools
mix local.hex
mix archive.install hex phx_new
```

## phoenix getting started

공식문서

https://hexdocs.pm/phoenix/Phoenix.html


## phoenix 실행해보기 문제가 생겼다!

<img width="1392" alt="스크린샷 2023-08-03 오전 1 23 20" src="https://github.com/Hansanghyeon/phoenix_getting_started/assets/42893446/1ee43976-4b18-47dd-b6f2-f612a6f59a35">

```shell
apt install erlang
```

elixir만 설치해서 생긴 문제였다.

## 실행중에 나오는 에러!

```shell
# 처음에 ecto 문제인지 알고 이렇게 설치했다 
mix phx.new hello --no-ecto
cd hello
mix phx.server
```

<img width="1392" alt="image" src="https://github.com/Hansanghyeon/phoenix_getting_started/assets/42893446/10a4315d-4600-4dce-a21b-b86dac10a090">

```log
[error] `inotify-tools` is needed to run `file_system` for your system, check https://github.com/rvoicilas/inotify-tools/wiki for more information about how to install it. If it's already installed but not be found, appoint executable file with `config.exs` or `FILESYSTEM_FSINOTIFY_EXECUTABLE_FILE` env.
```

### ask chatGPT

해당 오류 메시지는 `phoenix` 프레임워크의 `file_system` 기능을 실행할 때 `inotify-tools`가 필요하다는 내용입니다. `inotify-tools`는 Linux에서 파일 시스템 이벤트를 모니터링하는데 사용되는 도구입니다. 이 도구가 설치되어 있지 않거나 실행 파일을 찾을 수 없을 때 이 오류가 발생할 수 있습니다.

이 문제를 해결하려면 다음 단계를 따르면 됩니다:

1. `inotify-tools` 설치: `inotify-tools`를 시스템에 설치해야 합니다. 먼저, 시스템에 설치되어 있는지 확인합니다. 대부분의 Linux 배포판에서는 패키지 관리자를 통해 설치할 수 있습니다. 예를 들어, Ubuntu/Debian 기반 시스템에서는 다음 명령을 사용하여 설치합니다:

```
sudo apt-get update
sudo apt-get install inotify-tools
```

다른 배포판에서는 해당 배포판의 패키지 관리자를 사용하여 설치할 수 있습니다.

2. 실행 파일 찾기: `inotify-tools`가 이미 설치되어 있지만 실행 파일이 발견되지 않는 경우, `phoenix` 설정 파일인 `config.exs`에 `FILESYSTEM_FSINOTIFY_EXECUTABLE_FILE` 환경 변수를 설정하여 실행 파일의 경로를 지정할 수 있습니다. 예를 들어:

```elixir
# config.exs

config :file_system, fsinotify_executable_file: "/path/to/inotifywait"
```

실행 파일의 경로를 정확하게 입력해야 합니다. 경로를 확인하려면 터미널에서 `which inotifywait` 명령을 실행하거나 `inotify-tools`를 설치한 위치를 살펴봅니다.

3. 프로젝트 다시 시작: 설정을 변경한 후에는 `phoenix` 프로젝트를 다시 시작해야 변경사항이 적용됩니다.

위 단계를 따라 하나 이상의 방법으로 문제를 해결할 수 있어야 합니다. `inotify-tools`를 설치하고 실행 파일 경로를 제대로 설정하면 `file_system` 기능을 원활하게 사용할 수 있을 것입니다.

### 해결되었다!

```shell
apt-get install inotify-tools
```

설치후에

<img width="1392" alt="image" src="https://github.com/Hansanghyeon/phoenix_getting_started/assets/42893446/62ba5bd4-fcb3-40f2-8ba5-92f68ecda70d">
