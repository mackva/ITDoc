docker-compose.yaml
```yaml
version: "3"
services:
  adguardhome:
    image: adguard/adguardhome
    container_name: adguardhome
    ports:
      # Plain DNS
      - 53:53/tcp
      - 53:53/udp   
      # AdGuard Home Admin Panel
      - 3001:3000/tcp
    volumes:
      - /opt/adguardhome/work:/opt/adguardhome/work
      - /opt/adguardhome/conf:/opt/adguardhome/conf
      - /etc/localtime:/etc/localtime:ro
    restart: unless-stopped
```

Решение проблемы  "Error starting userland proxy: listen tcp4 0.0.0.0:53: bind: address already in use"

sudo mkdir /etc/systemd/resolved.conf.d
sudo nano /etc/systemd/resolved.conf.d/adguardhome.conf

```conf
[Resolve]
DNS=127.0.0.1
DNSStubListener=no
```
