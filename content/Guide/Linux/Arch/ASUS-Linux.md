---
title: ASUS-Linux Install
---
> For details see: https://asus-linux.org/guides/arch-guide/

## Install
1. Edit `/etc/pacman.conf`:
	```
	[g14]
	Server = [https://arch.asus-linux.org](https://arch.asus-linux.org)
	```

2. Install:
	```
	pacman-key --recv-keys 8F654886F17D497FEFE3DB448B15A6B0E9A3FA35
	pacman-key --finger 8F654886F17D497FEFE3DB448B15A6B0E9A3FA35
	pacman-key --lsign-key 8F654886F17D497FEFE3DB448B15A6B0E9A3FA35
	pacman-key --finger 8F654886F17D497FEFE3DB448B15A6B0E9A3FA35
	pacman -Sy asusctl power-profiles-daemon
 rog-control-center
	```

3. Enable
```bash
systemctl enable --now power-profiles-daemon.service

```