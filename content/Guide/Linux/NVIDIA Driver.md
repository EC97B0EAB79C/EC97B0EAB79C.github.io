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
sudo pacman -S nvidia-open-dkms nvidia-utils
```

#### 3. Enable DRM Modesetting

> KDE needs this step.

1. Edit `/etc/default/grub`:
	```
	GRUB_CMDLINE_LINUX_DEFAULT="... cryptdevice=... nvidia_drm.modeset=1"
	```

2. Update the GRUB configuration:
	```bash
	sudo grub-mkconfig -o /boot/grub/grub.cfg
	```

#### 4. Load the Modules Early

1. Edit `/etc/mkinitcpio.conf`:
	```
	MODULES=(nvidia nvidia_modeset nvidia_uvm nvidia_drm)
	```

2. Regenerate the initramfs:
	```bash
	sudo mkinitcpio -P
	```

#### 5. Enable ASUS Hybrid Services

> Note: This step is for [[Guide/Linux/Arch/ASUS-Linux|ASUS-Linux]].

```
sudo systemctl enable --now supergfxd
```