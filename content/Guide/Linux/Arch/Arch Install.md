---
title: Arch Install
---
## 1. Boot & Connect
```bash
iwctl --passphrase "YOUR_PASSWORD" station wlan0 connect "YOUR_SSID"
timedatectl set-ntp true
```

## 2. Partition
### Identify Disks

```bash
lsblk
```

### Partition

```bash
cfdisk /dev/nvme0n1
```
- Type: Linux filesystem

### Encrypt

```bash
cryptsetup luksFormat /dev/nvme0n1p5
cryptsetup open /dev/nvme0n1p5 cryptroot
```

### Format
```bash
mkfs.ext4 /dev/mapper/cryptroot
```

### Mount
```bash
#Root
mount /dev/mapper/cryptroot /mnt
# EFI
mkdir /mnt/efi
mount /dev/nvme0n1p1 /mnt/efi
```

> Note: Because `/dev/nvme0n1p1` has not enough space, mounting to `/mnt/efi`

## 3. Installation
```bash
# Use 'intel-ucode' for Intel CPU
pacstrap /mnt base base-devel linux linux-firmware vim git networkmanager amd-ucode
genfstab -U /mnt >> /mnt/etc/fstab
arch-chroot /mnt
```

## 4. Configuration
### Mkinitcpio

1. Edit `/etc/mkinitcpio.conf`:
	```
	HOOKS=(base udev autodetect modconf kms keyboard keymap consolefont block encrypt filesystems fsck)
	```
2. Regenerate:
	```bash
	mkinitcpio -P
	```

### GRUB

1. Install tools:
	```bash
	pacman -S grub efibootmgr os-prober
	```
2. Get UUID:
	```bash
	blkid | grep crypto_LUKS
	```
3. Edit `/etc/default/grub`:
	```
	GRUB_ENABLE_CRYPTODISK=y
	GRUB_CMDLINE_LINUX_DEFAULT="loglevel=3 quiet cryptdevice=UUID=PASTE_UUID_HERE:cryptroot root=/dev/mapper/cryptroot"
	GRUB_DISABLE_OS_PROBER=false
	```
4. Install Bootloader:
	```bash
	grub-install --target=x86_64-efi --efi-directory=/efi --bootloader-id=GRUB
	```
5. Generate menu:
	```bash
	grub-mkconfig -o /boot/grub/grub.cfg
	```

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
	net-tools openssh
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