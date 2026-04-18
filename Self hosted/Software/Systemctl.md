#### Добавление в автозапуск

```sh
sudo nano /etc/systemd/system/loophole.service
```

```txt
[Unit]
Description=loophole
After=network.target

[Service]
User=pi
Group=pi

ExecStart=/opt/loophole/loophole http 80 --hostname mackva
ExecReload=/bin/kill -HUP $MAINPID
KillMode=process
IgnoreSIGPIPE=true

Restart=always
RestartSec=3
Type=simple

[Install]
WantedBy=multi-user.target
```

```txt
[Unit]
Description=AssistantBot
After=network.target

[Service]
User=pi
Group=pi

WorkingDirectory=/home/pi/AssistantBot/
ExecStart=/home/pi/AssistantBot/Telegram.Bot.Examples.WebHook

Restart=always
RestartSec=10
KillSignal=SIGINT
SyslogIdentifier=assistantbot-identifier

Environment=ASPNETCORE_ENVIRONMENT=Production
Environment=DOTNET_PRINT_TELEMETRY_MESSAGE=false

[Install]
WantedBy=multi-user.target
```


Добавить юнит в автозагрузку
```sh
sudo systemctl enable loophole
```
Запуск юнита
```sh
sudo systemctl start loophole
```
Перезагрузка юнита
```sh
sudo systemctl restart dnsserver.service
```
Статус юнита
```sh
sudo systemctl status loophole
```


#### Удалить службу
```sh
sudo systemctl stop <имя_службы>
sudo systemctl disable <имя_службы>
sudo rm /etc/systemd/system/<имя_службы>
sudo systemctl daemon-reload
```


#### Каталоги хранения юнитов
`/usr/lib/systemd/system` – юниты поставляемые вместе с системой и устанавливаемыми приложениями  
`/run/systemd/system` – юниты созданные динамически (в рантайме)  
`/etc/systemd/system` – юниты системного администратора (тут и будем хранить наши)

#### [Unit]
- **Description** – описание юнита для большего понимания
- **Documentation** – документация по процессу sshd
- **After** – зависимость, т.е. в данном случае запускать юнит только после запуска network.target и sshd-keygen.target
- **Wants** – еще одна зависимость, означает желательно. В примере Wants=sshd-keygen.target, т.е. желательно чтобы было запущено sshd-keygen.target . Желательно но не обязательно.
#### [Service]
**Type** – типы запуска служб. Могут быть
- **simple** (по умолчанию) – происходит незамедлительный запуск этой службы, с учетом того что процесс не разветвляется (fork). Не используйте simple если пользуетесь очередностью запуска. Одно исключение это активация сокета.
- **forking** – служба считается запущенной после того, после разветвления процесса с завершением родительского процесса. Используется для запуска классических демонов исключая случаи, когда в таком поведении процесса нет необходимости. Также желательно указать PIDFile=, чтобы systemd мог отслеживать основной процесс.
- **oneshot** – удобен для скриптов, которые выполняют одно задание и завершаются. При необходимости можно задать параметр RemainAfterExit=yes, чтобы systemd считал процесс активным даже после его завершения.
- **notify** – идентичен параметру simple, но с оговоркой, что демон пошлет systemd сигнал о своей готовности. Эталонная реализация данного уведомления представлена в libsystemd-daemon.so.
- **dbus** – служба считается находящейся в состоянии готовности, когда указанный параметр BusName появляется в системной шине DBus.
- **idle** – откладывается выполнение двоичного файла службы до момента выполнения всех остальных задач. В остальном поведение аналогично simple.

Далее в разделе **Service**

- **EnvironmentFile** – файлы переменного окружения
- **ExecStart** – полный путь к исполняемому файлу программы с параметрами запуска
- **ExecReload** – полный пусть к исполняемому файлу программы с параметрами перезапуска программы
- **KillMode** – указывается как будет завершен процесс. В данному случае параметр process говорит о том что будет закрыт только главный процесс
- **Restart** – перезагрузка процесса, параметр on-failure указывает на автоматическую перезагрузку в случает отказа процесса
- **RestartSec** – время ожидания через которое процесс должен перезагрузиться
#### [Install]

- **WantedBy** – указывает на каком уровне запуска стартует сервис, параметр multi-user.target указывает на запуск в многопользовательском режиме без графики

#### Ссылки:
1) [Создание простого systemd unit](https://newadmin.ru/sozdanie-prostogo-systemd-unit/)
2) [Запуск приложений на .NET в качестве службы на Linux-системе с systemd ](https://habr.com/ru/companies/timeweb/articles/759966/)