#### Чтобы установить сервер Ubuntu:
1) Скачиваем с [официального сайта](https://ubuntu.com/download/server) образ ubuntu-22.04.3-live-server-amd64.
2) Создайте загрузочную флешку с помощью rufus 
3) Загружаемся с флешки
![[rufus-4.3p.exe]]

Отключаем LVM
Разбивка диска: оставляем 1Гб под EFI (создаётся автоматический), остальное EXT4 под "корень"

Your name Ваше имя, Your server name хост,  Pick a username  логин.

Ubunta Pro  не нужна.

OpenSSH  нужен

Snaps  пропускаем


Устанавливаем Docker и Docker Compose [[Install Docker]]

Устанавливаем [[Postgres]]

Устанавливаем [[Gitea]]
