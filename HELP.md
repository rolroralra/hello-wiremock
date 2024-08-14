### 1. **Podman 설치 확인**

먼저, Mac에서 Podman이 설치되어 있는지 확인하세요. 설치되지 않았다면 다음 명령어를 사용해 설치할 수 있습니다.

```bash
brew install podman
```

Podman을 설치한 후, 다음 명령어로 가상 머신을 설정하고 시작하세요.

```bash
podman machine init
podman machine start
```

### 2. **Podman의 Docker 호환 설정**

Mac에서 Podman을 Docker CLI 및 Docker Compose와 함께 사용하려면 `podman-docker`를 설정할 필요가 있습니다. 이는 Docker 명령어가 Podman을 통해 실행되도록 하는 설정입니다.

#### 2.1. **Podman 소켓 활성화**

Podman은 Mac에서 기본적으로 rootless 모드로 실행됩니다. Docker CLI가 Podman의 데몬 소켓에 연결할 수 있도록 소켓을 활성화해야 합니다.

```bash
podman machine ssh -- systemctl --user enable --now podman.socket
```

이 명령어는 가상 머신 내에서 Podman 소켓을 활성화합니다.

#### 2.2. **Docker CLI 및 Compose와 연결**

Podman 소켓을 활성화한 후, 환경 변수를 설정하여 Docker CLI와 Docker Compose가 Podman 소켓에 연결되도록 해야 합니다. `.zshrc`, `.bashrc` 또는 현재 터미널 세션에 다음을 추가하세요:

```bash
export DOCKER_HOST=unix://$HOME/.local/share/containers/podman/machine/podman.sock
```

이렇게 하면 Docker CLI 명령어를 사용하여 Podman을 제어할 수 있습니다.

#### 2.3. **Podman Compose 사용 (선택사항)**

Docker Compose 대신 `podman-compose`를 사용할 수도 있습니다. 이는 Podman에 최적화된 Compose 도구입니다.

```bash
pip3 install podman-compose
```

이제 `podman-compose` 명령어를 사용하여 Docker Compose 파일을 실행할 수 있습니다.

```bash
podman-compose up
```

### 3. **docker-compose.yaml 파일의 `version` 경고 해결**

Docker Compose 파일에서 `version` 필드를 제거하는 것이 좋습니다. 이는 최신 Docker Compose에서는 `version` 필드가 필요하지 않기 때문입니다.

수정 전:

```yaml
version: '3.8'
services:
  web:
    image: nginx
    ports:
      - "80:80"
```

수정 후:

```yaml
services:
  web:
    image: nginx
    ports:
      - "80:80"
```

### 4. **Podman 및 Docker Compose 테스트**

설정이 완료되었으면, Docker Compose 파일을 실행하여 설정이 정상적으로 동작하는지 확인합니다.

```bash
docker-compose up
```

만약 문제가 발생하지 않는다면, Docker Compose가 Podman을 통해 정상적으로 실행되는 것입니다.

### 5. **Podman 데몬 관리**

Podman은 Mac에서 가상 머신을 통해 실행되므로, Podman을 사용할 때마다 다음 명령어로 가상 머신을 시작해야 합니다.

```bash
podman machine start
```

작업이 끝나면 가상 머신을 중지할 수 있습니다.

```bash
podman machine stop
```