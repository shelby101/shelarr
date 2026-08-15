# Qbittorrent

[qbit/github](https://github.com/qbittorrent/qBittorrent/)

### compose.yaml
```yaml
services:
  qbittorrent:
    image: lscr.io/linuxserver/qbittorrent:latest
    container_name: qbittorrent
    environment:
      - PUID=568
      - PGID=568
      - TZ=Etc/UTC
      - WEBUI_PORT=8090
      - TORRENTING_PORT=45676
#      - DOCKER_MODS=ghcr.io/vuetorrent/vuetorrent-lsio-mod:latest
    volumes:
      - /opt/appdata/qbittorrent:/config
      - /mnt/4tb/data:/data
    ports:
      - 8090:8090
      - 45676:45676
      - 45676:45676/udp
    restart: unless-stopped
networks: {}
```