---
title: fstab Cheat Sheet
---

## Config
`/etc/fstab`:

```
# exFAT/NTFS/FAT32
UUID=YOUR_UUID_HERE /media/usb-drive auto defaults,nofail,uid=1000,gid=1000,umask=002 0 0

# Ext4
UUID=YOUR_UUID_HERE /media/usb-drive ext4 defaults,nofail 0 2
```