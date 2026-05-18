docker-compose.yaml
```yaml
services:
  minidlna:
    image: vladgh/minidlna:latest
    container_name: minidlna
    network_mode: host
    restart: unless-stopped

    environment:
      - PUID=1000
      - PGID=1000
      - MINIDLNA_FRIENDLY_NAME=MyHomeServer
      - MINIDLNA_MEDIA_DIR=/media
      - TZ=Asia/Novosibirsk
      # Если нужно сканировать только конкретные папки:
      # - MINIDLNA_MEDIA_DIR_1=V,/media/videos
      # - MINIDLNA_MEDIA_DIR_2=A,/media/music
    volumes:
      - /usbdrive/transmission/:/media:ro
      - /opt/minidlna/config:/var/cache/minidlna
```
