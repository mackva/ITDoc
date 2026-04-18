
docker-compose.yaml
```yaml
version: '3.5'

services:
  app:
    image: nextcloud
    restart: unless-stopped
    ports:
      - 8888:80
    volumes:
      - /opt/nextcloud/nextcloud-data:/var/www/html
    environment:
      - POSTGRES_HOST=postgres
      - POSTGRES_PASSWORD=MYPAS
      - POSTGRES_DB=nextcloud_db
      - POSTGRES_USER=MYUSER
    networks:
      - postgres

networks:
  postgres:
    name: postgres-net
    driver: bridge
```
Заменить `MYUSER` и `MYPAS` в docker-compose.yaml