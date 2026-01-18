---
title: Fcitx5 Setup
---
## Setup
### Install

1. Install packages
   ```bash
	sudo pacman -S fcitx5-im kcm-fcitx5 fcitx5-mozc fcitx5-hangul
	```
2. Add to `/etc/environment` or `~/.pam_environment`:
	```bash
	GTK_IM_MODULE=fcitx
	QT_IM_MODULE=fcitx
	XMODIFIERS=@im=fcitx
   ```
3. Configure Mozc:
   ```bash
   fcitx5-configtool
   ```
