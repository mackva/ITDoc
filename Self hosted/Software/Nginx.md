Установка
```sh
sudo apt install nginx
```
Запуск\\Остановка\\Перезапуск смотри [[Systemctl]]

Проверить синтаксические ошибки в конфиге
```sh
sudo nginx -t
```

#### Настройка Basic Auth в Nginx
```sh
sudo apt install apache2-utils
```
Создаем файл со списком пользователей и паролей
```sh
sudo htpasswd -c /путь/к/файлу имя_пользователя
sudo htpasswd -c /etc/nginx/auth.basic pi
```
Добавим пользователя developer
```sh
sudo htpasswd /etc/nginx/auth.basic developer
```

Для того чтобы защитить паролем все ваши сайты просто добавьте эти директиву в секцию `http` файла `etc/nginx/nginx.conf`
```
auth_basic "Restricted area";  
auth_basic_user_file /etc/nginx/auth.basic;
```

Для защиты только определённой URL добавьте эти же директивы в нужный блок location в файле `/etc/nginx/nginx.conf`
```
    location /git/ {
       ...
       auth_basic "Restricted area";
       auth_basic_user_file /etc/nginx/auth.basic;
    }
```

Если же наоборот надо разрешить доступ для определённого location 
```
    location /git/ {
       ...
       auth_basic "off";
    }
```

Дальше перезапускаем nginx
```sh
sudo service nginx restart
```

