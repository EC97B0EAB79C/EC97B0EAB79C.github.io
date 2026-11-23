---
title: Linux Unified Key Setup
---

## Steps
1. Identify the device:
	```bash
	lsblk
	```

2. Create the LUKS container:
	```bash
	sudo cryptsetup luksFormat /dev/sda
	```

3. Map the encrypted volume to `/dev/mapper/encrpt`:
	```bash
	sudo cryptsetup open /dev/sda encrpt
	```

4. Create the filesystem:
	```bash
	sudo mkfs.ext4 /dev/mapper/encrpt
	```

## Usage
### Unlock and Mount
```bash
sudo cryptsetup open /dev/sda encrpt
sudo mkdir -p /mnt/secure_data
sudo mount /dev/mapper/encrpt /mnt/secure_data
```

### Unmount and Lock
```bash
sudo umount /mnt/secure_data
sudo cryptsetup close encrpt
```