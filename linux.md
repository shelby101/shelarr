#### Makes a folder

```bash
sudo mkdir /opt/appdata/app
```

#### Gives ownership to a user. -R stands for recursive so it applies to the folder, subfolders, files
```bash
sudo chown -R 568:568 /opt/appdata/app
```

___


## Mounting the HDD (example)

```bash
# 1. Create your custom 4tb storage folder
sudo mkdir -p /mnt/4tb

# 2. Mount your hard drive partition directly to the new 4tb folder
sudo mount /dev/sda1 /mnt/4tb

# 3. Pass full folder ownership over to your 'apps' user and group (ID 568)
sudo chown -R apps:apps /mnt/4tb
sudo chmod -R 775 /mnt/4tb

# 4. Stamp the friendly name '4tb' onto the drive's file system layout
sudo e2label /dev/sda1 4tb

# 5. Automatically append the permanent UUID rule to your system boot file
echo "UUID=7ad056ac-1708-4abc-a190-5b156af07873 /mnt/4tb ext4 defaults 0 2" | sudo tee -a /etc/fstab

# 6. Refresh all system mounts to test your work and confirm zero errors
sudo mount -a
lsblk -o NAME,LABEL,SIZE,MOUNTPOINTS
```
