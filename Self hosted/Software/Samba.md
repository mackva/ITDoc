docker-compose.yaml
```yaml
version: "2.1"
services:
  transmission:
    image: dperson/samba:latest
    container_name: samba
    environment:
      - PUID=1000
      - PGID=1000
      - TZ=Asia/Novosibirsk
    volumes:
      - /usbdrive/transmission/:/cloud:z
    ports:
      - 139:139
      - 445:445
      - 137:137/udp
      - 138:138/udp
    restart: unless-stopped
    command: '-u "user;password" -s "public;/cloud;yes;no;yes;user" -p'
```
Добавить пользователя
```sh
-u "<username;password>[;ID;group;GID]"
```

- `username` – пользователь;
- `password` – пароль;

Настройте рабочую группу (домен), которую должна использовать Samba.
```shell
-s "<name;/path>[;browse;readonly;guest;users;admins;writelist;comment]"

-s "public;/cloud/share;yes;no;yes;username1,username2" \
-s "storage1;/cloud/username1;yes;no;no;username1" \
-s "storage2;/cloud/username2;yes;no;no;username2"
```
- `name` – название раздела;
- `path` – путь до раздела в контейнере;
- `browsable` – no скрывает раздел из списка выбора;
- `readonly` – no позволяет записывать данные на раздел;
- `guest` – no отключает гостевой доступ;
- `users` – список разрешённых пользователей;
- `admins` – список пользователей администратора;
- `writelist` – список пользователей, которые могут писать в общий ресурс;
- `comment` – описание раздела;

Windows
```
file://IP
```
Far Manager
```
net://IP
```
MacOS
```
smb://user@IP
```
#### Ссылки:
1) [dperson/samba](https://hub.docker.com/r/dperson/samba)