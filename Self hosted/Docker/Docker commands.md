
Остановка всех контейнеров
```
docker stop $(docker ps -a -q)
```

Удаление всех контейнеров
```
docker rm $(docker ps -a -q)
```

Отобразить списка всех контейнеров
```
docker ps -a
```

Скопировать из **хоста** в **контейнер**
```
docker cp <путь к файлу на хост машине> containerid:<путь к файлу в контейнере>

docker cp /opt/softethervpn/vpn_server.config softethervpn:/usr/vpnserver/vpn_server.config 

```

Скопировать из **контейнер** в **хост** 
```
docker cp containerid:<путь к файлу на хост машине> <путь к файлу на хост машине>

docker cp  softethervpn:/usr/vpnserver/vpn_server.config /opt/softethervpn/vpn_server.config

```
