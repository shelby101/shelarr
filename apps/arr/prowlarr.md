# Prowlarr

Prowlarr is an indexer manager/proxy built on the popular *arr .net/reactjs base stack to integrate with your various PVR apps. Prowlarr supports management of both Torrent Trackers and Usenet Indexers. It integrates seamlessly with Lidarr, Mylar3, Radarr, Readarr, and Sonarr offering complete management of your indexers with no per app Indexer setup required (we do it all).

[Github](https://github.com/Prowlarr/Prowlarr)

___

### compose.yaml
services:
  prowlarr:
    image: lscr.io/linuxserver/prowlarr:latest
    container_name: prowlarr
    environment:
      - PUID=568
      - PGID=568
      - TZ=Etc/UTC
    volumes:
      - /opt/appdata/prowlarr:/config
    ports:
      - 9696:9696
    restart: unless-stopped
```
