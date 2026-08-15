# Jellystat

more info about users, media files
[github](https://github.com/CyferShepard/Jellystat)
___

### compose.yaml

```yaml
services:
  jellystat-db:
    image: postgres:15.2
    container_name: jellystat-db
    restart: unless-stopped
    shm_size: 1gb
    environment:
      POSTGRES_USER: postgres
      POSTGRES_PASSWORD: mypassword
      POSTGRES_DB: jellystat
    volumes:
      - ./postgres-data:/var/lib/postgresql/data
  jellystat:
    image: cyfershepard/jellystat:latest
    container_name: jellystat
    restart: unless-stopped
    ports:
      - 3001:3000
    environment:
      POSTGRES_USER: postgres
      POSTGRES_PASSWORD: mypassword
      POSTGRES_IP: jellystat-db
      POSTGRES_PORT: 5432
      JWT_SECRET: my-secret-jwt-key
      TZ: Europe/Bucharest
    depends_on:
      - jellystat-db
    volumes:
      - ./jellystat-backup-data:/app/backend/backup-data
```
