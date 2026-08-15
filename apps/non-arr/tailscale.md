# Tailscale

VPN 

### compose.yaml
```yaml
services:
  tailscale:
    image: tailscale/tailscale:stable
    container_name: tailscale
    hostname: nas_name
    network_mode: host
    environment:
      - TS_AUTHKEY=${TS_AUTHKEY}
      - TS_STATE_DIR=/var/lib/tailscale
      - TS_USERSPACE=false
    volumes:
      - ./state:/var/lib/tailscale
    cap_add:
      - NET_ADMIN
      - NET_RAW
    devices:
      - /dev/net/tun:/dev/net/tun
    restart: unless-stopped
```
