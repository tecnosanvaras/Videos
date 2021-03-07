## Docker Compose utilizados en el vídeo

## Heimdall
```
version: "2.1"
services:
  heimdall:
    image: ghcr.io/linuxserver/heimdall
    container_name: heimdall
    environment:
      - PUID=1000
      - PGID=1000
      - TZ=Europe/Madrid
    volumes:
      - /path/to/config:/config
    ports:
      - 9001:80
      - 40443:443
    restart: unless-stopped
```

