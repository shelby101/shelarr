# My arr stack

## Index
- [How To Start](How%20to%20start.md)
- [Linux](./linux-commands.md)
- [Compose files](./How%20to%20start.md#4-install-the-arr-stack)




## How I run my apps

All the apps I have currently run as a docker container.

If the app doesn't require root they all run as 568:568.

The composer yamls and app files are in /opt/

Before I use a composer file in Dockge I first create the folder in appdata using:

```bash
sudo mkdir /opt/appdata/app-name
chown -R 568:568 /opt/appdata/app-name
```
Unless it requires to run under root then I don't use chown

## Compose files

Click the link above or browse the [apps](apps) folder.


