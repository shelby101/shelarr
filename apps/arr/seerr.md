# Seerr 
## Used to request media

#### compose.yaml
```yaml
services:
  seerr:
    image: ghcr.io/seerr-team/seerr:latest
    container_name: seerr
    init: true
    user: 568:568
    ports:
      - 5055:5055
    environment:
      - TZ=Etc/UTC
      - LOG_LEVEL=debug
    volumes:
      - /opt/appdata/seerr:/app/config
    restart: unless-stopped
```

