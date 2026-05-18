docker-compose.yaml
```yaml
services:
  deepface:
    image: serengil/deepface
    ports:
      - 5005:5000
    restart: unless-stopped
```