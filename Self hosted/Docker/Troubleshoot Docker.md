#### Исправление ошибки вида "http: server gave HTTP response to HTTPS client"

^3ca791

Для Linux система добавите в файла /etc/docker/daemon.json
```JSON
{
  "insecure-registries": [
    "192.168.1.31:3000"
  ]
}
```
И перезапустите docker daemon 
```sh
sudo systemctl restart docker
```
Для Windows система, docker desktop => Settings => Docker Engine добавить "insecure-registries" как для linux, и применить настройки.

#### Docker Hub заблокировал доступ для пользователей из России. 

##### Текст ошибки
```
Error response from daemon: error parsing HTTP 403 response body

Error response from daemon: pull access denied for nginx, repository does not exist or may require 'docker login'
```

#### 1. Зеркала
Через конфиг докера (как зеркало docker.io)

| Операционная система | Путь к файлу конфигурации                    |
| -------------------- | -------------------------------------------- |
| Linux, regular setup | /etc/docker/daemon.json                      |
| Linux, rootless mode | ~/.config/docker/daemon.json                 |
| macOS                | ~/.docker/daemon.json                        |
| OrbStack             | Settings -> Docker -> Advanced engine config |
| Windows              | C:\ProgramData\docker\config\daemon.json     |
| Docker Desktop       | Preferences -> Docker engine                 |

daemon.json
```json
"registry-mirrors": ["https://mirror.gcr.io", "https://dockerhub.timeweb.cloud"]
```

```sh
systemctl restart docker
```
#### Ссылки: 
1) [Блокировка Docker Hub для России. Без паники разбираемся как работать дальше](https://habr.com/ru/articles/818565/)
2) [huecker.io](huecker.io)
