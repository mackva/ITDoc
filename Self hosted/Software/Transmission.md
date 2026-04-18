
docker-compose.yaml
```yaml
version: "2.1"
services:
  transmission:
    image: linuxserver/transmission:latest
    container_name: transmission
    environment:
      - PUID=1000
      - PGID=1000
      - TZ=Asia/Novosibirsk
    volumes:
      -  /opt/transmission/config:/config
      - /usbdrive/transmission/downloads:/downloads
      - /usbdrive/transmission/watch:/watch
    ports:
      - 9091:9091
      - 51413:51413
      - 51413:51413/udp
    restart: unless-stopped
```

Создать папку
```sh
sudo mkdir /usbdrive
```
Монтируем диск
```sh
sudo mount /dev/sda1 /usbdrive
```
Размонтируем диск
```sh
sudo umount /usbdrive
```
Получить PARTUUID
```sh
sudo blkid
```
```txt
/dev/sda1: UUID="30e5827c-9e45-45c9-ab5c-02d331a2d262" BLOCK_SIZE="4096" TYPE="ext4" PARTUUID="c32a5074-7f3f-f946-a683-d5c14a02f1b7"

```
Авто монтирование
```sh
sudo nano /etc/fstab
```
Монтирование по пути или по PARTUUID более надежный 
```txt
/dev/sda1 /usbdrive ext4 defaults 0 0

PARTUUID="c32a5074-7f3f-f946-a683-d5c14a02f1b7" /usbdrive ext4 defaults 0 0
```
Отобразить все смонтированы разделы 
```sh
df -h
```

Получить список ваших дисков
```sh
sudo fdisk -l
```

Чтобы выполнить операции на вашем диске
```sh
sudo fdisk /dev/sda
```
Используйте следующие сочетания клавиш в **fdisk**:
- Создайте новую таблицу разделов: **g** (для GPT используйте справку для других форматов)
- Создайте новый раздел: **n**
- Вы можете сохранить значения по умолчанию для первого раздела.
- Просто нажимайте Enter после каждого вопроса.
- Подтвердите нажатием Y, чтобы удалить подпись.
- И, наконец, напишите и выйдите из fdisk: w
Когда вы снова запустите fdisk -l, вы увидите новый раздел.
Вы можете следовать следующей части, чтобы отформатировать ее так, как вы хотите.
 
Форматируем диск в ext4
```sh
sudo mkfs -t ext4   /dev/sda1
```

#### Ссылки:
1) [Как изменить размер корневого раздела на Raspberry Pi/Orange Pi/Banana Pi](https://micro-pi.ru/%D0%B8%D0%B7%D0%BC%D0%B5%D0%BD%D0%B8%D1%82%D1%8C-%D1%80%D0%B0%D0%B7%D0%BC%D0%B5%D1%80-%D0%BA%D0%BE%D1%80%D0%BD%D0%B5%D0%B2%D0%BE%D0%B3%D0%BE-%D1%80%D0%B0%D0%B7%D0%B4%D0%B5%D0%BB%D0%B0/)
2) [Домашний сервер на Orange Pi — часть 2: подключение USB-диска](https://onlynix.ru/2020/03/13/domashnij-server-na-orange-pi-chast-2-podklyuchen/)