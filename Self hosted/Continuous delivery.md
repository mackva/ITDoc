docker-compose.yaml
```yaml
version: '3.8'
services:
  missjulia:
    image: 192.168.1.31:3000/mackva/missjulia.telegram.bot:master
    platform: linux/aarch64
    container_name: missjulia
    restart: unless-stopped
    ports:
      - "8080:80"
    environment:
      - BotConfiguration__BotToken=MYTOKEN
      - BotConfiguration__HostAddress=https://my.site/AssistantBot
```

Заменить `MYTOKEN`, `MYHOST` в docker-compose.yaml


#### Ссылки:
1) [Introduction to GitHub Actions](https://docs.docker.com/build/ci/github-actions/)
2) 