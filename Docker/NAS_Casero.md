# Instalación de Open Media Vault en Nuestra Raspberry Pi

Todos los contenedores que aquí encontrais, tienen su autor y por tanto sus derechos de autor.
Ninguno de ellos me pertenece y podeis encontrarlos en la web de Docker Hub: https://hub.docker.com/.
La mayoria tienen su documentación en el github del creador y solo hago un resumen aquí de los utilizados en mis vídeos.
En la descripción de todos ellos teneis los enlaces a la documentación y el github de su creador.

Al igual que vosotros, los que habeis llegado hasta aquí, soy también usuario de YouTube y es muy triste ver vídeos en los que el Youtuber del canal utiliza la información realizada por otros sin tan siquiera mencionar al autor y de donde han sacado esa información.

Quiero agradecer de todo corazón a todas las personas que nos permiten disfrutar con sus muchas horas de trabajo, de un material como el que yo mismo utilizo.

Gracias, gracias, gracias.

...................................


Para la instalación de Open Media Vault en la Raspberry, primero tenemos que instalar Raspberry pi OS lite.
Una vez instalado y configurado según las indicaciones del vídeo (https://www.youtube.com/watch?v=EGLbhnGFxvQ) lanzamos el siguiente comando:
```
wget -O - https://github.com/OpenMediaVault-Plugin-Developers/installScript/raw/master/install | sudo bash
```


# Docker Compose utilizados en el vídeo

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

## Plex
```
version: "2.1"
services:
  plex:
    image: linuxserver/plex:bionic
    container_name: plex
    network_mode: host
    environment:
      - PUID=1000
      - PGID=1000
      - VERSION=docker
      - UMASK_SET=022
    volumes:
      - /path/to/Docker/plex/library:/config
      - /path/to/Docker/plex/tvseries:/tv
      - /path/to/Peliculas:/movies
    restart: unless-stopped
```

## Jellyfin
```
version: "2.1"
services:
  jellyfin:
    image: ghcr.io/linuxserver/jellyfin
    container_name: jellyfin
    environment:
      - PUID=1000
      - PGID=1000
      - TZ=Europe/Madrid
    restart: "unless-stopped"
    network_mode: host
    volumes:
      - /path/to/Docker/jellyfin/config:/config
      - /path/to/Docker/jellyfin/cache:/cache
      - /path/to/Peliculas:/movies
      - /path/to/Series:/tvshows
    ports:
      - 8096:8096
```

## Nextcloud
Es recomendable cambiar nombres de usuario y contraseña de las bases de datos. Esto es solo un ejemplo del contenedor
```
version: '2'

volumes:
  nextcloud:
  db:

services:

  db:
    image: ghcr.io/linuxserver/mariadb
    container_name: mariadb
    environment:
      - PUID=1000
      - PGID=1000
      - MYSQL_ROOT_PASSWORD=nextcloud
      - TZ=Europe/Madrid
      - MYSQL_DATABASE=nextcloud
      - MYSQL_USER=nextcloud
      - MYSQL_PASSWORD=nextcloud
    volumes:
      - /path/to/Docker/db/config:/config
    ports:
      - 3306:3306
    restart: unless-stopped

  app:
    image: nextcloud
    container_name: nextcloud
    restart: unless-stopped
    ports:
      - 8181:80
    links:
      - db
    volumes:
      - nextcloud:/var/www/html
```

## RPI Monitor
```
docker run --device=/dev/vchiq --volume=/opt/vc:/opt/vc --volume=/boot:/boot --volume=/sys:/dockerhost/sys:ro --volume=/etc:/dockerhost/etc:ro --volume=/proc:/dockerhost/proc:ro --volume=/usr/lib:/dockerhost/usr/lib:ro -p=8888:8888 --name="rpi-monitor" -d  michaelmiklis/rpi-monitor:latest
```

## Pihole
```
version: "3"

services:
  pihole:
    container_name: pihole
    image: pihole/pihole:latest
    ports:
      - "TU_IP:53:53/tcp"
      - "TU_IP:53:53/udp"
      - "67:67/udp"
      - "8383:80/tcp"
      - "1443:443/tcp"
    environment:
      TZ: 'Europe/Madrid'
      WEBPASSWORD: tecnosanvaras
    volumes:
      - /path/to/pihole/etc-pihole/:/etc/pihole/
      - /path/to/pihole/etc-dnsmasq.d/:/etc/dnsmasq.d/
    cap_add:
      - NET_ADMIN
    restart: unless-stopped
```

## Adguard
```
version: "2"
services:
  adguardhome:
    image: adguard/adguardhome
    container_name: adguardhome
    ports:
      - TU_IP:53:53/tcp
      - TU_IP:53:53/udp
      - 67:67/udp
      - 8668:68/tcp
      - 8668:68/udp
      - 853:853/tcp
      - 3000:80/tcp
    volumes:
      - /path/to/Docker/adguard/workdir:/opt/adguardhome/work
      - /path/to/Docker/adguard/confdir:/opt/adguardhome/conf
    restart: unless-stopped
```

## Qbittorrent
```
version: "2.1"
services:
  qbittorrent:
    image: linuxserver/qbittorrent
    container_name: qbittorrent
    environment:
      - PUID=1000
      - PGID=1000
      - TZ=Europe/Madrid
      - WEBUI_PORT=8585
    volumes:
      - /path/to/Docker/qbittorrent/appdata/config:/config
      - /path/to/Docker/qbittorrent/downloads:/downloads
    ports:
      - 6881:6881
      - 6881:6881/udp
      - 8585:8585
    restart: unless-stopped
```

## WatchTower
```
version: '2.1'
services:
    watchtower:
        image: containrrr/watchtower
        container_name: watchtower
        volumes:
            - /var/run/docker.sock:/var/run/docker.sock
        environment:
            - TZ=Europe/Madrid
        restart: unless-stopped
```

## Duplicati
```
version: "2.1"
services:
  duplicati:
    image: ghcr.io/linuxserver/duplicati
    container_name: duplicati
    environment:
      - PUID=1000
      - PGID=1000
      - TZ=Europe/Madrid
      - CLI_ARGS= #optional
    volumes:
      - </path/to/appdata/config>:/config
      - </path/to/backups>:/backups
      - </path/to/source>:/source
    ports:
      - 8200:8200
    restart: unless-stopped
```

## Home Assistant
Dependiendo si estais usando Raspberry pi 3 o 4 teneis que modificar la linea "image"
```
version: '3'
services:
  homeassistant:
    container_name: homeassistant
    image: homeassistant/raspberrypi4-homeassistant:stable
    volumes:
      - /PATH_TO_YOUR_CONFIG:/config
      - /etc/localtime:/etc/localtime:ro
    restart: unless-stopped
    network_mode: host
```

## WordPress
Es recomendable cambiar nombres de usuario y contraseñs de las bases de datos. Esto es solo un ejemplo del contenedor
```
version: '2.1'

services:

  wordpress:
    image: wordpress
    restart: always
    ports:
      - 84:80
    environment:
      WORDPRESS_DB_HOST: db
      WORDPRESS_DB_USER: usuario
      WORDPRESS_DB_PASSWORD: password
      WORDPRESS_DB_NAME: nombrebd
    volumes:
      - wordPress:/var/www/html
    links:
      - db:db

  db:
    image: yobasystems/alpine-mariadb:latest
    restart: always
    environment:
      MYSQL_DATABASE: exampledb
      MYSQL_USER: exampleuser
      MYSQL_PASSWORD: examplepass
      MYSQL_RANDOM_ROOT_PASSWORD: '1'
    volumes:
      - wordPress:/var/lib/mysql
```
## Wireguard
```
version: "2.1"
services:
  wireguard:
    image: ghcr.io/linuxserver/wireguard
    container_name: wireguard
    cap_add:
      - NET_ADMIN
      - SYS_MODULE
    environment:
      - PUID=1000
      - PGID=1000
      - TZ=Europe/Madrid
      - SERVERURL=wireguard.domain.com #optional
      - SERVERPORT=51820 #optional
      - PEERS=1 #optional
      - PEERDNS=auto #optional
      - INTERNAL_SUBNET=10.13.13.0 #optional
      - ALLOWEDIPS=0.0.0.0/0 #optional
    volumes:
      - /path/to/appdata/config:/config
      - /lib/modules:/lib/modules
    ports:
      - 51820:51820/udp
    sysctls:
      - net.ipv4.conf.all.src_valid_mark=1
    restart: unless-stopped
```

## NGINX Proxy Manager
Es recomendable cambiar nombres de usuario y contraseña de las bases de datos. Esto es solo un ejemplo del contenedor
```
version: '3'
services:
  app:
    image: 'jc21/nginx-proxy-manager:latest'
    ports:
      - '80:80'
      - '81:81'
      - '443:443'
    environment:
      DB_MYSQL_HOST: "db"
      DB_MYSQL_PORT: 3306
      DB_MYSQL_USER: "npm"
      DB_MYSQL_PASSWORD: "npm"
      DB_MYSQL_NAME: "npm"
    volumes:
      - ./data:/data
      - ./letsencrypt:/etc/letsencrypt
  db:
    image: 'yobasystems/alpine-mariadb:latest'
    environment:
      MYSQL_ROOT_PASSWORD: 'npm'
      MYSQL_DATABASE: 'npm'
      MYSQL_USER: 'npm'
      MYSQL_PASSWORD: 'npm'
    volumes:
      - ./data/mysql:/var/lib/mysql
```

## Taisun
```
version: "2"
services:
  taisun:
    image: linuxserver/taisun
    container_name: taisun
    network_mode: bridge
    volumes:
      - /var/run/docker.sock:/var/run/docker.sock
    ports:
      - 3000:3000
    restart: unless-stopped
```
## YouTube DL
```
version: "2"
services:
    ytdl_material:
        environment: 
            ALLOW_CONFIG_MUTATIONS: 'true'
        restart: always
        volumes:
            - /path/to/appdata:/app/appdata
            - /path/to/audio:/app/audio
            - /path/to/video:/app/video
            - /path/to/subscriptions:/app/subscriptions
            - /path/to/users:/app/users
        ports:
            - "8998:17442"
        image: tzahi12345/youtubedl-material:latest
```
## BitWarden
```
version: "2"
services:
  bitwarden:
    image: bitwardenrs/server:latest
    container_name: bitwarden
    volumes:
      - /path/to/Config/BitWarden:/data/
    ports:
      - 8686:80
    restart: unless-stopped
```
