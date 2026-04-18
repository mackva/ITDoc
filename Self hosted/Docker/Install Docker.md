### Установка Docker в Armbian

Скрипт автоматической установки Docker для Linux:
```sh
sudo apt-get update
sudo apt-get install -y curl
curl -fsSL https://get.docker.com -o get-docker.sh
chmod +x get-docker.sh
sudo ./get-docker.sh
rm get-docker.sh
```

```

Текущая версии Dockerа:
```sh
sudo docker version
```

Добавить пользователя pi в группу :
```sh
sudo usermod -aG docker pi
sudo usermod -aG ./ pi  (Была эта команда)

sudo shutdown -r now
```

Docker должен работать без sudo
```sh
docker version
```

#### Установка docker-compose

```sh
sudo apt-get install -y docker-compose
docker-compose version
```

