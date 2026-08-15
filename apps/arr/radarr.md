
# Radarr

[Github](https://github.com/Radarr/Radarr)

[Website](https://radarr.video/)

I use 2 instances because I want to be able to have in Jellyfin both a HD and UHD version, otherwise if I request a 4K version the FHD will be replaced. Tags can be used but this is easier.

### HD

```yaml
services:
  radarr:
    image: lscr.io/linuxserver/radarr:latest
    container_name: radarr
    environment:
      - PUID=568
      - PGID=568
      - TZ=Etc/UTC
    volumes:
      - /opt/appdata/radarr:/config
      - /mnt/4tb/data:/data
    ports:
      - 7878:7878
    restart: unless-stopped
networks: {}
```

### UHD

```yaml
services:
  radarr4k:
    image: lscr.io/linuxserver/radarr:latest
    container_name: radarr4k
    environment:
      - PUID=568
      - PGID=568
      - TZ=Etc/UTC
    volumes:
      - /opt/appdata/radarr4k:/config
      - /mnt/4tb/data:/data
    ports:
      - 7879:7878
    restart: unless-stopped
```

