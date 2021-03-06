title: Docker useful Containers
description: Docker useful Containers

# Docker Containers

## Watchtower - Automating Docker Updates Container

```docker
docker run \
-d \
--restart always \
--name watchtower \
-h watchtower \
-v /var/run/docker.sock:/var/run/docker.sock \
-e TZ=Asia/Jerusalem \
containrrr/watchtower:latest --cleanup --debug
```

## cloudflare-ddns

```docker
docker run \
-d \
--restart always \
--name=cloudflare-ddns \
-h cloudflare-ddns \
-v /volume1/docker/cloudflare-ddns/config.yaml:/app/config.yaml \
-e TZ=Asia/Jerusalem \
-e PUID=1000 \
-e PGID=1000 \
joshava/cloudflare-ddns:latest
```

config.yaml example:

```config
auth:
  scopedToken: E8AAPoDE_Ukt7soafzZ4JcizLoUQ8YtAhXR3xE3
domains:
  - name: sub.example.com
    type: A
    proxied: false
    create: false
    zoneId: 88d455fbf3685db55fbe6855fb13de44fb3a8
```

## Ubiquiti Unifi Controller On Synology NAS

```docker
docker run \
-d \
--restart always \
--name=unifi-controller \
-h unifi-controller \
-e MEM_LIMIT=1024M  \
-v /volume1/docker/unifi:/config \
-p 8080:8080/tcp \
-p 8081:8081/tcp \
-p 11503:8443/tcp \
-p 8843:8843/tcp \
-p 8880:8880/tcp \
-p 3478:3478/udp \
-p 10001:10001/udp \
-p 6789:6789 \
-e TZ=Asia/Jerusalem \
-e PUID=1000 \
-e PGID=1000 \
linuxserver/unifi-controller:latest
```

## iperf3 Server Container

```docker
docker run \
-d \
--restart always \
--name=iperf3-server \
-h iperf3-server \
-p 5201:5201 \
-e TZ=Asia/Jerusalem \
-e PUID=1000 \
-e PGID=1000 \
networkstatic/iperf3:latest -s
```

## Calibre-Web

```docker
docker run \
-d \
--restart always \
--name=calibre-web \
-h calibre-web \
-v /volume1/docker/calibre/config:/config \
-v /volume1/docker/calibre/books:/books \
-e DOCKER_MODS=linuxserver/calibre-web:calibre \
-e TZ=Asia/Jerusalem \
-e PUID=1000 \
-e PGID=1000 \
linuxserver/calibre-web:latest
```

## HomeBridge

```docker
docker run \
-d \
--restart always \
--net=host \
--name=homebridge \
-e TZ=Asia/Jerusalem \
-e PUID=1000 \
-e PGID=1000 \
-e HOMEBRIDGE_CONFIG_UI=1 \
-e HOMEBRIDGE_CONFIG_UI_PORT=11507 \
-e HOMEBRIDGE_INSECURE=1 \
-v /volume1/docker/homebridge:/homebridge \
oznu/homebridge
```

## Sonarr - Container to Auto Download TV Shows

```docker
docker run \
-d \
--restart always \
--name sonarr \
-h sonarr \
-e TZ=Asia/Jerusalem \
-p 11504:8989 \
-v /volume1/docker/sonarr:/config \
-v /volume1/activeShare/Media/TV\ Showes/:/tv \
-v /volume1/activeShare/DownloadStation/:/downloads \
-e TZ=Asia/Jerusalem \
-e PUID=1000 \
-e PGID=1000 \
linuxserver/sonarr:latest
```

## Radarr - Container to Auto Download Movies

```docker
docker run \
-d \
--restart always \
--name=radarr \
-h radarr \
-p 11505:7878 \
-v /volume1/docker/radarr:/config \
-v /volume1/activeShare/Media/Movies:/movies \
-v /volume1/activeShare/DownloadStation:/downloads \
-e TZ=Asia/Jerusalem \
-e PUID=1000 \
-e PGID=1000 \
linuxserver/radarr:latest
```

## Jackett - Container for Indexers for Radarr & Sonarr

```docker
docker run \
-d \
--restart always \
--name=jackett \
-h jackett \
-p 11501:9117 \
-v /volume1/docker/jackett:/config \
-v /volume1/activeShare/DownloadStation:/downloads \
-e TZ=Asia/Jerusalem \
-e PUID=1000 \
-e PGID=1000 \
linuxserver/jackett:latest
```

Import Jackett Indexer In Sonarr

Add Custom Tornzab with API Path of:

```bash
/torznab/all/api
```

Import Jackett Indexer In Radarr

Add Custom Tornzab with URL of:

```bash
<ADDRESS>:<PORT>/torznab/all/
```

## Bazarr - Container for Subtitles Auto Download

```docker
docker run \
-d \
--restart always \
--name=bazarr \
-h bazarr \
-v /volume1/docker/bazarr:/config \
-v /volume1/activeShare/Media/Movies:/movies \
-v /volume1/activeShare/Media/TV\ Showes/:/tv \
-e TZ=Asia/Jerusalem \
-e PUID=1000 \
-e PGID=1000 \
linuxserver/bazarr:latest
```

## Ombi - Container for Requesting Movies & TV Shows Integrated with Sonarr & Radarr

```docker
docker run \
-d \
-h ombi \
--restart always \
--name=ombi \
-v /volume1/docker/ombi:/config \
-e TZ=Asia/Jerusalem \
-e PUID=1000 \
-e PGID=1000 \
linuxserver/ombi:latest
```

## Joal - Torrent Fake Seedings

```docker
docker run \
-d \
--name="joal" \
--restart always \
-h joal \
-p 11506:9000 \
-v /volume1/docker/joal:/data \
-e TZ=Asia/Jerusalem \
-e PUID=1000 \
-e PGID=1000 \
anthonyraymond/joal:latest \
--joal-conf="/data" \
--spring.main.web-environment=true \
--server.port="9000" \
--joal.ui.path.prefix="joal" \
--joal.ui.secret-token="joal"
```

## Zabbix Monitoring Container

```docker
docker run \
-d \
--name zabbix-appliance \
--restart always \
-h zabbix \
-p 10051:10051 \
-p 11502:80 \
-v /volume1/docker/zabbix:/var/lib/zabbix \
-v /volume1/docker/zabbix/mysql:/var/lib/mysql \
-v /volume1/docker/zabbix/nginx:/etc/ssl/nginx \
-e ZBX_SERVER_NAME=zabbix.3os.re \
-e TZ=Asia/Jerusalem \
-e PHP_TZ=Asia/Jerusalem \
-e TZ=Asia/Jerusalem \
-e PUID=1000 \
-e PGID=1000 \
zabbix/zabbix-appliance:latest
```

## Traefik - Revers proxy with Let's Encrypt and Cloudflare DNS Challenge

```docker
docker run \
-d \
--restart always \
--name=traefik \
-h traefik \
-v /volume1/docker/traefik.3os.re:/etc/traefik/ \
-v /var/run/docker.sock:/var/run/docker.sock \
-p 80:80 \
-p 443:443 \
-e TZ=Asia/Jerusalem \
-e CLOUDFLARE_EMAIL=cloudflare@email.org \
-e CLOUDFLARE_API_KEY=de1782bd0e8d05245f6648d03e1e6e17c \
traefik:latest
```
