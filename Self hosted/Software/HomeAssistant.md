docker-compose.yaml
```yaml
version: '3.0'

services:
  homeassistant:
    container_name: homeassistant
    image: "ghcr.io/home-assistant/home-assistant:stable"
    ports:
      - "8123:8123"
    volumes:
      - /opt/homeassistant/config:/config
      - /etc/localtime:/etc/localtime:ro
      - /run/dbus:/run/dbus:ro
    environment:
      - TZ=Asia/Novosibirsk
    restart: unless-stopped
    privileged: true
    network_mode: host
```