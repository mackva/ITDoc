docker-compose.yaml
```yaml

version: '3.8'
services:
  openclaw-gateway:
    image: ghcr.io/openclaw/openclaw:latest
    container_name: openclaw-gateway
    restart: unless-stopped
    init: true
    ports:
      - "8888:80"
      - "18789:18789"
    volumes:
      - /opt/openclaw:/home/node/.openclaw
    environment:
      - MISTRAL_API_KEY=KEY
      - OPENCLAW_GATEWAY_BIND=0.0.0.0:18789
```