# Samba

This is used to navigate the NAS folders on Windows

I'm running this in a container as well.


### compose.yaml

```yaml
services:
  samba:
    image: crazymax/samba:latest
    container_name: samba
    network_mode: host
    environment:
      - TZ=Etc/UTC
      - SAMBA_LOG_LEVEL=1
    volumes:
      # The container's system config directory mapped to our appdata folder
      - /opt/appdata/samba:/data
      # Your real 4TB drive mapped to the share location we defined in config.yml
      - /mnt/4tb/data:/mnt/media
      - /mnt/4tb/private:/mnt/private
    restart: unless-stopped
networks: {}
```

### config.yml 

```yaml
auth:
  - user: mediauser
    group: mediauser
    uid: 568
    gid: 568
    password: mediapassword

  - user: privateuser
    group: mediauser
    uid: 569
    gid: 568
    password: privatepassword

#global:
#  - "force user = mediauser"
#  - "force group = mediauser"

share:
  - name: data
    path: /mnt/media
    forceuser: mediauser
    forcegroup: mediauser
    browsable: yes
    readonly: no
    guestok: no
    validusers: mediauser

  - name: private
    path: /mnt/private
    forceuser: privateuser
    forcegroup: mediauser
    browsable: yes
    readonly: no
    guestok: no
    validusers: privateuser
```

## Windows NAS paths

To be able to log in with 2 different users in the same windows session, we must edit the /etc/hosts file and add this 2 lines

```yaml
# Copyright (c) 1993-2009 Microsoft Corp.
#
# This is a sample HOSTS file used by Microsoft TCP/IP for Windows.
#
# This file contains the mappings of IP addresses to host names. Each
# entry should be kept on an individual line. The IP address should
# be placed in the first column followed by the corresponding host name.
# The IP address and the host name should be separated by at least one
# space.
#
# Additionally, comments (such as these) may be inserted on individual
# lines or following the machine name denoted by a '#' symbol.
#
# For example:
#
#      102.54.94.97     rhino.acme.com          # source server
#       38.25.63.10     x.acme.com              # x client host

# localhost name resolution is handled within DNS itself.
#	127.0.0.1       localhost
#	::1             localhost

192.168.88.162   nas
192.168.88.162   nas-private
```