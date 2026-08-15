# How To Start with *arr stack

1. [Install Docker](#1-install-dockerinstall-docker)
2. [Install Dockge](#2-install-dockge)
3. [Make the folder structure for both the containers and the media files](#3-make-the-folder-structure-for-both-the-containers-and-the-media-files)
4. [Install the arr stack](#4-install-the-arr-stack)
5. Configure it all


# 1. Install Docker

#### 1. Install necessary prerequisite tools
```bash
sudo apt update && sudo apt install -y ca-certificates curl gnupg
```
#### 2. Add Docker's official security GPG key
```bash
sudo install -m 0755 -d /etc/apt/keyrings
sudo curl -fsSL https://download.docker.com/linux/ubuntu/gpg -o /etc/apt/keyrings/docker.asc
sudo chmod a+r /etc/apt/keyrings/docker.asc
```
#### 3. Add the official Docker repository to your system sources
```bash
echo \
  "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.asc] https://download.docker.com/linux/ubuntu \
  $(. /etc/os-release && echo "$VERSION_CODENAME") stable" | \
  sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
```

#### 4. Update the package list and install Docker + the Compose plugin
```bash
sudo apt update
sudo apt install -y docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin
```

___

# 2. Install Dockge

[Dockge/github](https://github.com/louislam/dockge)

Create directories that store your stacks and stores Dockge's stack
```bash
mkdir -p /opt/stacks /opt/dockge
cd /opt/dockge
```

Create the compose file and paste the yaml below
```bash
sudo nano compose.yaml
```
ctrl+x to exit press Y to save

Start the server
```bash
docker compose up -d
```


## Compose.yaml 
```yaml
services:
  dockge:
    image: louislam/dockge:1
    restart: unless-stopped
    ports:
      # Host Port : Container Port
      - 5001:5001
    volumes:
      - /var/run/docker.sock:/var/run/docker.sock
      - ./data:/app/data
      # If you want to use private registries, you need to share the auth file with Dockge:
      # - /root/.docker/:/root/.docker

      # Stacks Directory
      # ⚠️ READ IT CAREFULLY. If you did it wrong, your data could end up writing into a WRONG PATH.
      # ⚠️ 1. FULL path only. No relative path (MUST)
      # ⚠️ 2. Left Stacks Path === Right Stacks Path (MUST)
      - /opt/stacks:/opt/stacks
    environment:
      # Tell Dockge where is your stacks directory
      - DOCKGE_STACKS_DIR=/opt/stacks
```

___

# 3. Make the folder structure for both the containers and the media files

The app's folder can be made before each install in /opt/appdata/

For media files we can use this command to make them all at once
```bash
mkdir -p /mnt/4tb/data/media/{anime,movies,movies2,movies4k,tv} /mnt/4tb/data/torrents/{anime,movies,movies4k,other,books,tv} /mnt/4tb/private
chown -R 568:568 /mnt/4tb/
```

chown gives the ownership to user 568 because that is how I run under most of my containers.

replace the "4tb" with whatever you named your hdd mount

## Folder structure for my media files follows the best practice for the *arr stack


```markdown
/mnt/4tb/
├── data
│   ├── media
│   │   ├── anime
│   │   ├── movies
│   │   ├── movies2
│   │   ├── movies4k
│   │   └── tv
│   └── torrents
│       ├── anime
│       ├── movies
│       ├── movies4k
│       ├── other
│       ├── books
│       └── tv
└── private
```

<details>
<summary> ⚠️ Click to see the /opt/ tree </summary>

```markdown
/appdata - files of most of the containers
/stacks - composer files that I run in dockge
/dockge - contains the app and it's own composer -- navigating here we can stop/restart the dockge app
/containerd - don't worry about it


/opt/
├── appdata
│   ├── adguard
│   ├── jellyfin
│   ├── seerr
│   ├── prowlarr
│   ├── qbittorrent
│   ├── radarr
│   ├── radarr4k
│   ├── recyclarr
│   ├── samba
│   ├── seerr
│   └── sonarr
├── containerd
├── dockge
│   └── data
└── stacks
    ├── ddns-updater
    ├── jellyfin
    ├── jellystat
    ├── npmplus
    ├── prowlarr
    ├── qbittorrent
    ├── radarr
    ├── radarr4k
    ├── recyclarr
    ├── samba
    ├── seerr
    ├── sonarr
    ├── sonarr2
    └── tailscale
```

</details>

___

# 4. Install the Arr stack

Main apps: Jellyfin, Radarr, Sonarr, Seerr, Prowlarr, Qbittorrent

These apps will be configured to automate the media collection.

___

Optional stuff

Jellystat - gives more data about your media files, users. 

Recyclarr - imports TRaSH guides into Sonarr/Radarr easier. [TRaSH github](https://trash-guides.info/Radarr/)

## Compose Files

| Arr Main Stack | Arr Optional | Non-Arr |
|---|---|---|
|[Radarr](/apps/arr/radarr.md)|[Recyclarr](/apps/arr/recyclarr.md)|[Samba](/apps/non-arr/samba.md)|
|[Sonarr](/apps/arr/sonarr.md)|[Jellystat](/apps/arr/jellystat.md)|[Tailscale](/apps/non-arr/tailscale.md)|
|[Seerr](/apps/arr/seerr.md)||[NPMPlus](/apps/non-arr/npmplus.md)|
|[Qbittorrent](/apps/arr/qbittorrent.md)| |
|[Prowlarr](/apps/arr/prowlarr.md)|||
