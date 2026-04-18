
Перезагрузить систему
```sh
sudo shutdown -r now
```
Выключить компьютер
```sh
sudo shutdown now
```
Отмена запланированной перезагрузки или выключения
```sh
sudo shutdown -c
```
Просмотр компьютеров в локальной сети
```sh
echo 192.168.1.{1..254}|xargs -n1 -P0 ping -c1|grep "bytes from"
```


Скопировать с **локального компьютер** на **удалённый сервер**
```
scp /local/dir/file.txt username@remoteHost:/remote/dir/

scp D:\temp\55\vpn_server.config pi@192.168.0.150:/opt/softethervpn/data/
```

Скопировать с  **удалённого сервера** на **локальный компьютер** 
```
scp username@remoteHost:/remote/dir/file.txt /local/dir/

scp pi@192.168.0.150:/opt/softethervpn/data/vpn_server.config D:\temp\55
```


Поиск и замена  подстроки `Foo` на `Bar` в файлах с именем **serilog.json** в каталоге `/app/`. 
```sh
find /app/ -type f -name "serilog.json" -print0 | xargs -0 sed -i 's|Foo|Bar|g'
```

Выводящая информацию о системе.
```sh
uname -a

Linux nanopi2 6.1.53-current-sunxi64 #1 SMP Wed Sep 13 07:43:05 UTC 2023 aarch64 GNU/Linux
```
#### Ссылки: 
1) [Список из полезных команд Linux](https://micro-pi.ru/%D0%BF%D0%BE%D0%BB%D0%B5%D0%B7%D0%BD%D1%8B%D0%B5-%D0%BA%D0%BE%D0%BC%D0%B0%D0%BD%D0%B4%D1%8B-linux-raspberry-pi/)