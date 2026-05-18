
docker-compose.yaml
```yaml
version: "3"

services:
  gitea:
    image: gitea/gitea:1.21.4
    container_name: gitea
    environment:
      - USER_UID=1000
      - USER_GID=1000
      - GITEA__database__DB_TYPE=postgres
      - GITEA__database__HOST=postgres:5432
      - GITEA__database__NAME=gitea_db
      - GITEA__database__USER=MYUSER
      - GITEA__database__PASSWD=MYPAS
      # [Service]
      - GITEA__service__REQUIRE_SIGNIN_VIEW=true
      # [OpenID]
      - GITEA__openid__ENABLE_OPENID_SIGNIN=false
      - GITEA__openid__ENABLE_OPENID_SIGNUP=false
    restart: unless-stopped
    networks:
      - postgres
    volumes:
      - /opt/gitea/gitea-data:/data
      - /etc/timezone:/etc/timezone:ro
      - /etc/localtime:/etc/localtime:ro
    ports:
      - "3000:3000"
      - "222:22"
      
networks:
  postgres:
    name: postgres-net
    driver: bridge
```

Заменить `MYUSER` и `MYPAS` в docker-compose.yaml

Для Gitea добавить прав для 1000
```sh
sudo chown -R 1000:1000 /opt/gitea/gitea-data
```

#### Gitea-runner

Настройки => Действия => Раннеры => Создать новый раннер => `MYTOKEN`

docker-compose.yaml
```yaml
version: "3.8"
services:
  runner:
    image: gitea/act_runner:nightly
    container_name: gitea-runner
    restart: unless-stopped
    environment:
      - GITEA_INSTANCE_URL=http://gitea:3000
      - GITEA_RUNNER_REGISTRATION_TOKEN=MYTOKEN
      - GITEA_RUNNER_NAME=MiniPC-Runner
    volumes:
      - /opt/gitea-runner/gitea-runner-data:/data
      - /var/run/docker.sock:/var/run/docker.sock
      
networks:
  postgres:
    name: postgres-net
    driver: bridge

```

Заменить `MYTOKEN` в docker-compose.yaml

Так же нужно настроить [[Continuous Integration in Gitea]]
