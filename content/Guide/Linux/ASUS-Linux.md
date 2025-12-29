---
title: ASUS-Linux Install
---
> For details see: https://asus-linux.org/guides/arch-guide/

## Install
Edit `/etc/pacman.conf`:
```
[g14]
Server = [https://arch.asus-linux.org](https://arch.asus-linux.org)
```

Install:
```
pacman-key --recv-keys 8F654886F17D497FEFE3DB448B15A6B0E9A3FA35
pacman-key --finger 8F654886F17D497FEFE3DB448B15A6B0E9A3FA35
pacman-key --lsign-key 8F654886F17D497FEFE3DB448B15A6B0E9A3FA35
pacman -Sy asusctl supergfxctl rog-control-center
```