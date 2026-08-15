# NPMplus

Reverse proxy
[Github](https://github.com/ZoeyVid/NPMplus)

```yaml
services:
  app:
    image: zoeyvid/npmplus:latest
    restart: unless-stopped
    network_mode: host
    volumes:
      - ./data:/data
    environment:
      DB_MYSQL_HOST: 127.0.0.1
      DB_MYSQL_PORT: 3306
      DB_MYSQL_USER: npm_admin
      DB_MYSQL_PASSWORD: npm_admin_password
      DB_MYSQL_NAME: npm
      TZ: Europe/Bucharest
      LOGROTATE: "true"
      LOGROTATIONS: "7"
    depends_on:
      db:
        condition: service_started
  db:
    image: mariadb:10.8
    restart: unless-stopped
    network_mode: host
    environment:
      MYSQL_ROOT_PASSWORD: mysql_root_password
      MYSQL_DATABASE: npm
      MYSQL_USER: npm_admin
      MYSQL_PASSWORD: npm_admin_password
    volumes:
      - ./db:/var/lib/mysql
networks: {}
```
