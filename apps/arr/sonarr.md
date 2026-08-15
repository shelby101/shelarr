# Sonarr

[Wiki](https://wiki.servarr.com/)
[Github](https://github.com/Sonarr/Sonarr)


## TV SHOWS

```yaml
services:
  sonarr:
    image: lscr.io/linuxserver/sonarr:latest
    container_name: sonarr
    environment:
      - PUID=568
      - PGID=568
      - TZ=Etc/UTC
    volumes:
      - /opt/appdata/sonarr:/config
      - /mnt/4tb/data:/data
    ports:
      - 8989:8989
    restart: unless-stopped
```

## Anime

```yaml
services:
  sonarr2:
    image: lscr.io/linuxserver/sonarr:latest
    container_name: sonarr2
    environment:
      - PUID=568
      - PGID=568
      - TZ=Europe/Bucharest
    volumes:
      - /apps/sonarr2/config:/config
      - /mnt/4tb/data:/data
    ports:
      - 8990:8989
    restart: unless-stopped
networks: {}
```