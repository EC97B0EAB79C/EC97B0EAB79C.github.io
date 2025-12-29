---
title: NVIDIA Driver
---
## Install
### Arch
#### 1. Enable Multilib

1. Edit `/etc/pacman.conf`:
	```
	[multilib]
	Include = /etc/pacman.d/mirrorlist
	```
2. Run:
	```bash
	sudo pacman -Sy
	```

#### 2. Install Drivers
```bash
sudo pacman -S nvidia-open nvidia-utils
```

#### 3. Enable DRM Modesetting

> Necessary for KDE

Edit `/etc/default/grub`:
```
GRUB_CMDLINE_LINUX_DEFAULT="... cryptdevice=... nvidia_drm.modeset=1"
```

Update:
```bash
sudo grub-mkconfig -o /boot/grub/grub.cfg
```

#### 4. Enable Early Loading

Edit `/etc/mkinitcpio.conf`:
```
MODULES=(nvidia nvidia_modeset nvidia_uvm nvidia_drm)
```

Regenerate:
```bash
sudo mkinitcpio -P
```

#### 5. Enable ASUS Hybrid Services
> Note: for [[Guide/Linux/ASUS-Linux|ASUS-Linux]]
```
sudo systemctl enable --now supergfxd
```