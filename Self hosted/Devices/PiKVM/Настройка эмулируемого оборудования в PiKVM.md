
### Подготовка (режим записи)
Для внесения изменений переведите файловую систему в режим записи:
```bash
rw
````

### Изменение данных монитора (EDID)

Задает идентификатор производителя (MFC ID), название модели и включает поддержку аудио:
```bash
kvmd-edidconf --set-mfc-id=AUS --set-monitor-name=PA248QV --set-audio=1
```

### Настройка параметров OTG (HID/USB)
Для маскировки PiKVM под конкретное устройство (например, периферию Corsair) отредактируйте файл конфигурации:

```bash
nano /etc/kvmd/override.yaml
```

**Вставьте следующие параметры:**


```yaml
otg:
  vendor_id: 0x6940
  product_id: 0x6973
  manufacturer: Corsair
  product: Gaming RGB
  serial: 1000
  devices:
    audio:
      enabled: true
kvmd:
  msd:
    type: disabled
  hid:
    video:
      mfc_id: TTP
      product_id: 34953
      monitor_name: DELL
      serial: 2290649089
```


### Применение новых настроек

Перезапустите сервис `kvmd` для активации настроек и верните систему в безопасный режим «только чтение»:

```bash
systemctl restart kvmd
ro
```

---

#PiKVM #Hardware #Emulation #Config #Linux