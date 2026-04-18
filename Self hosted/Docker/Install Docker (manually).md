#### Установка Docker на Ubuntu
В первую очередь, нам нужно обновить индексы пакетов
```sh
sudo apt update
```
Для установки докера потребуется дополнительно загрузить 4 пакета, а именно:
- curl — необходим для работы с веб-ресурсами;
- software-properties-common — пакет для управления ПО с помощью скриптов;
- ca-certificates — содержит информацию о центрах сертификации;
- apt-transport-https — необходим для передачи данных по протоколу HTTPS.

Скачаем их:
```sh
sudo apt install curl software-properties-common ca-certificates apt-transport-https -y
```
Флаг -y означает, что на все вопросы терминала ответом будет «Да».

 Импортируем GPG-ключ

GPG-ключ нужен для верификации подписей ПО. Он понадобится для добавления репозитория докера в локальный список. Импортируем GPG-ключ:
```sh
wget -O- https://download.docker.com/linux/ubuntu/gpg | gpg --dearmor | sudo tee /etc/apt/keyrings/docker.gpg > /dev/null
```

Добавим репозиторий для нашей версии Ubuntu, которая называется «Jammy». Для других версий ОС нужно использовать их кодовые имена, которые были перечислены в разделе «Системные требования». Выполняем команду:
```sh
echo "deb [arch=amd64 signed-by=/etc/apt/keyrings/docker.gpg] https://download.docker.com/linux/ubuntu jammy stable"| sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
```
В очередной раз обновляем индексы пакетов
```sh
sudo apt update
```
Проверяем репозиторий

Убедимся, что инсталляция будет осуществлена из нужного нам репозитория. Выполняем следующую команду:

```sh
apt-cache policy docker-ce
```
Главное убедиться, что установка будет осуществляться из репозитория докера. 

Устанавливаем докер
```sh
sudo apt install docker-ce -y
```

Проверим статус докера в системе:
```sh
sudo systemctl status docke
```

#### Ссылки: 
1) [Как установить Docker на Ubuntu 22.04: инструкция](https://timeweb.cloud/tutorials/docker/kak-ustanovit-docker-na-ubuntu-22-04)
