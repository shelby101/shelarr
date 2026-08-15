# Recyclarr

Imports TRaSH guides into sonarr or radarr easier

[Website](https://recyclarr.dev/guide/guide-configs/)

[TRaSH](https://trash-guides.info/Radarr/)

### compose.yaml
```yaml
services:
  recyclarr:
    image: ghcr.io/recyclarr/recyclarr:8
    container_name: recyclarr
    user: 568:568
    environment:
      - TZ=Etc/UTC
      - CRON_SCHEDULE=@daily
    volumes:
      - /opt/appdata/recyclarr:/config
    restart: unless-stopped
```

___

## My configs

### recyclarr.yaml

```yaml
radarr:
  movies:
    base_url: http://192.168.88.162:7878
    api_key: YOUR_RADARR_API_KEY

    # Automatically imports TRaSH Guides custom file size recommendations
    quality_definition:
      type: movie

    # Injects the exact official Remux + WEB 1080p profile
    quality_profiles:
      - trash_id: 9ca12ea80aa55ef916e3751f4b874151
        reset_unmatched_scores:
          enabled: true

  movies4k:
    base_url: http://192.168.88.162:7879
    api_key: YOUR_RADARR_API_KEY #the other instance of radarr

    quality_definition:
      type: movie

    quality_profiles:
      - trash_id: fd161a61e3ab826d3a22d53f935696dd  # Remux + WEB 2160p
        reset_unmatched_scores:
          enabled: true

sonarr:
  tv:
    base_url: http://192.168.88.162:8989
    api_key: YOUR_SONARR_API_KEY

    # Automatically imports TRaSH Guides custom show size recommendations
    quality_definition:
      type: series

    # Injects the exact official WEB-1080p profile
    quality_profiles:
      - trash_id: 72dae194fc92bf828f32cde7744e51a1
        reset_unmatched_scores:
          enabled: true

      - trash_id: d1498e7d189fbe6c7110ceaabb7473e6  # WEB-2160p
        reset_unmatched_scores:
          enabled: true
```