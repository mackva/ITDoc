### NAS Agestar NCB3AST/NSB3AS/NSB3AST/NSB3AS1T

#### Замена  SATA-HDD/USB диска 
1) Заходим в веб морду http://192.168.1.27. admin/root
2) Форматируем подключенное устройство в файловую систему ext3 (а может xfs?)
3) Задаем пароль для FTP доступа пользователя admin. admin/admin
4) Копируем  tweakpack.tar.gz  в /mnt/data/public
5) Заходим по телнету на 192.168.1.27 root
6) Переходим в папку, где лежит архив `cd /mnt/data/public`
7) Распаковываем его `tar xzvf tweakpack.tar.gz` 
8) Переходим в распакованную папку `cd tweakpack`
9) Даем себе права на исполнение скрипта `chmod 755 install.sh`
10) Если прошивать не нужно то из install.sh нужно удалить 1-3 этапы `vi install.sh` Удалить строку dd
11) Запускаем скрипт `./install.sh`

>Внимание: Когда закончиться работа скрипта, Вам нужно будет перезагрузить Ваш NAS. После чего она станет доступен по адресу `http://<NAS IP>:9091`  user/password

12) Настройки храниться в `/conf/.config/settings.json`
13) На веб-морде, в меню **Tools**, добавлен параграф **WGET downloader** для управления wget. Его конфигурационный файл находиться по пути `/conf/.cron/web2wget.conf`
#### SAMBA по умолчанию отключена.
1) Для **_ВКЛЮЧЕНИЯ_** редактируем файл `vi /conf/.cron/rc.kill`
2) Нажимаем INSERT
3) "Закомментируем" следующие записи:
```
#killall -9 smbd  
#killall -9 nmbd
```
4) Нажимаем Esc, и, чтобы сохранить, вводим ZZ
5) Выполняем перезагрузку `/etc/init.d/rc.reboot`

#### Авто запуск

`\etc\init.d\rc.sysinit\rc.sysinit  =>  /conf/.cron/rc.sys`

```
if [ ! -d /mnt/data/public ]; then
    if [ -d /mnt/port1/P1_A_1 ]; then
       mkdir -p /mnt/data/public
       mount --bind /mnt/port1/P1_A_1 /mnt/data/public
    fi
fi
```

#### Файлы:
![tweakpack.tar.gz](tweakpack.tar.gz)
![pkg.tar.gz](pkg.tar.gz)
![sqfs.tar.gz](sqfs.tar.gz)

#### Ссылки: 
- [Обзор NSB3AST / NSB3AS](https://forum.ru-board.com/topic.cgi?forum=88&topic=5552)
- [Обсуждение NAS Agestar NCB3AST/NSB3AS/NSB3AST/NSB3AS1T](https://forum.ixbt.com/topic.cgi?id=109:112)
- [BusyBox](https://ru.wikipedia.org/wiki/BusyBox)
- [Установка и настройка transmission-daemon Ubuntu server 20.04](https://habr.com/ru/articles/658463/)

