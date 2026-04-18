#### Чтобы установить сервер armbian:
1) Скачиваем с [Armbian](https://www.armbian.com/nanopi-k1-plus/) образ Armbian Bookworm Minimal.
2) Создайте загрузочную флешку с помощью win32diskimager 
3) Загружаемся с флешки
![[win32diskimager.zip]]
#### Как войти?
```
root/1234

en-US
```
#### Как обновить прошивку и пакеты?
```
sudo apt update
sudo apt upgrade
```

#### Armbian-config
```
sudo armbian-config

nanopi1
192.168.1.11
```

#### Устанавливаем Docker и Docker Compose [[Install Docker]]
#### Ссылки: 
1) [Armbian Quick Start Guide](https://docs.armbian.com/User-Guide_Getting-Started/)