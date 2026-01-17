---
title: Arch Install
---

> For details check [ArchWiki](https://wiki.archlinux.org/title/Installation_guide)

## 1. Boot & Connect
```bash
iwctl --passphrase "YOUR_PASSWORD" station wlan0 connect "YOUR_SSID"
timedatectl set-ntp true
```

## 2. Partition

TODO

### Mount Partitions
```bash
mount /dev/root_partition /mnt
mount --mkdir /dev/efi_system_partition /mnt/boot
```

## 3. Installation
```bash
# Use 'intel-ucode' for Intel CPU
pacstrap /mnt base base-devel linux linux-firmware vim git networkmanager amd-ucode
arch-chroot /mnt
```

> If error TODO

## 4. Configuration
### File system
```bash
genfstab -U /mnt >> /mnt/etc/fstab
```

#### Change root to new system
```bash
arch-chroot /mnt
```

### Set time and localization
```bash
ln -sf /usr/share/zoneinfo/Area/Location /etc/localtime
hwclock --systohc
locale-gen
echo LANG=en_US.UTF-8 >> /etc/locale.conf
```

### Mkinitcpio

1. Edit `/etc/mkinitcpio.conf`:
	```
	HOOKS=(base udev autodetect modconf kms keyboard keymap consolefont block encrypt filesystems fsck)
 	#HOOKS=(base udev autodetect microcode modconf kms keyboard keymap sd-vconsole block encrypt filesystems fsck)
	```
2. Regenerate:
	```bash
	mkinitcpio -P
	```

### Boot loader
#### `systemd-boot`
> Installing `systemd-boot` as recommended by `asus-linux`

1. Install:
	```bash
	bootctl install
	```
2. Edit `/boot/loader/loader.conf`:
	```
	default	arch.conf
 	timeout	3
 	console-mode max
 	editor	no
	```
 TODO

## 5. Setup System
### User

```bash
useradd -m -G wheel -s /bin/bash your_user
passwd your_user
passwd
```

### Sudo

Edit `EDITOR=vim visudo`:
```
wheel ALL=(ALL:ALL) ALL
```

### Network
```bash
systemctl enable NetworkManager
```

### ASUS-Linux
Install [[Guide/Linux/Arch/ASUS-Linux|ASUS-Linux]]

## 6. Setup Desktop (KDE)

```bash
pacman -S plasma-meta sddm konsole dolphin
systemctl enable sddm
```

## 7. Finish

```bash
exit
umount -R /mnt
reboot
```

## Next Steps
### NVIDIA Driver
[[Guide/Linux/NVIDIA Driver#Arch|Install]]

### Packages Consider Installing
```
sudo pacman -S \
	noto-fonts noto-fonts-emoji noto-fonts-cjk \
	net-tools openssh \
	ntfs-3g
```

#### `bash-completion`
1. Install
	```bash
	sudo pacman -S bash-completion
	```
2. Edit `~/.bashrc`:
	```bash
	[[ $PS1 && -f /usr/share/bash-completion/bash_completion ]] && \
	    . /usr/share/bash-completion/bash_completion
	```

### `.bashrc`
```bash
#  
# ~/.bashrc  
#  
  
# If not running interactively, don't do anything  
[[ $- != *i* ]] && return  
  
  
alias ls='ls --color=auto'  
alias grep='grep --color=auto'  
alias diff='diff --color=auto'  
alias ip='ip -color=auto'  
alias ll='ls -l --color=auto'  
alias la='ls -la --color=auto'  
  
export GCC_COLORS='error=01;31:warning=01;35:note=01;36:caret=01;32:locus=01:quote=01'  
  
#PS1='[\u@\h \W]\$ '  
PS1='\[\033[01;32m\]\u@\h\[\033[00m\]:\[\033[01;34m\]\W\[\033[00m\]\$ '
```
