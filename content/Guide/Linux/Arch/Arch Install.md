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

### 2.1 Create partition
#### `fdisk`

1. Open drive
```bash
fdisk /dev/nvme0n1
```
2. Create a new GPT (`g`)
3. Create EFI partition
	1. New partition (`n`)
	2. Id: `[default]`
	3. First sector: `[default]`
	4. Last sector: `+1G`
	5. Change Type to EFI: `t`, `1`
4. Create Root partition
	1. New partition (`n`)
	2. First sector: `[default]`
	3. Last sector: `[default]`
5. Write changes (`w`)

### 2.2 (Optional) Creating LUKS encryption

[[Guide/Linux/LUKS|LUKS]]

1. Format the partition
	```bash
	cryptsetup luksFormat /dev/nvme0n1p2
	```
2. Open encrypted partition
	```bash
	cryptsetup open /dev/nvme0n1p2 cryptroot
	```

### 2.3 Format Partitions

1. Format EFI partition
	```bash
	mkfs.fat -F 32 /dev/nvme0n1p1
	```
2. Format encrypted root
	```bash
	mkfs.ext4 /dev/mapper/cryptroot
	```
### 2.4 Mount Partitions
```bash
mount /dev/root_partition /mnt
mount --mkdir /dev/efi_system_partition /mnt/boot
```

## 3. Installing essential packages
```bash
# Use 'intel-ucode' for Intel CPU
pacstrap /mnt base base-devel linux linux-firmware linux-headers vim git networkmanager amd-ucode
arch-chroot /mnt
```

> If error `file not found: /etc/vconsole.conf`, check [[Trouble Shoot/Linux Issues/Arch Install/file not found `vconsole.conf`|here]]

## 4. Configuration
### 4.1 File system
```bash
genfstab -U /mnt >> /mnt/etc/fstab
```

#### 4.2 Change root to new system
```bash
arch-chroot /mnt
```

### 4.3 Set time and localization
```bash
ln -sf /usr/share/zoneinfo/Area/Location /etc/localtime
hwclock --systohc
locale-gen
echo LANG=en_US.UTF-8 >> /etc/locale.conf
```

### 4.4 `mkinitcpio`

1. Edit `/etc/mkinitcpio.conf`:
	```
	HOOKS=(base udev autodetect modconf kms keyboard keymap consolefont block encrypt filesystems fsck)
 	#HOOKS=(base udev autodetect microcode modconf kms keyboard keymap sd-vconsole block encrypt filesystems fsck)
	```
	> Note: `encrypt` is necessary when encrypting partition
2. Regenerate:
	```bash
	mkinitcpio -P
	```

### 4.5 Root password
```bash
passwd
```
### Boot loader
#### `systemd-boot`
> Installing `systemd-boot` as recommended by `asus-linux`

1. Install:
	```bash
	bootctl install
	```
2. Edit `/boot/loader/loader.conf`:
	```TOML
	default	arch.conf
 	timeout	3
 	console-mode max
 	editor	no
	```
 3. Edit `/boot/loader/entries/arch.conf`:
```TOML
title   Arch Linux
linux   /vmlinuz-linux
initrd /amd-ucode.img
initrd  /initramfs-linux.img
options cryptdevice=UUID=YOUR-UUID-HERE:cryptroot root=/dev/mapper/cryptroot rw
```

## 5. Setup System
### 5.1 User

```bash
useradd -m -G wheel -s /bin/bash your_user
passwd your_user
passwd
```

### 5.2 Sudo

Edit `EDITOR=vim visudo`:
```
%wheel ALL=(ALL:ALL) ALL
```

### 5.3 Network
```bash
systemctl enable NetworkManager
```

### 5.4 ASUS-Linux
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
