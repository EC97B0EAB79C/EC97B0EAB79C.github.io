---
title: KWin and Fcitx 5 Wayland Integration
date: 2026-03-28
---


## Problem Description
[[#Details|Pop up]] showing when logging in.

### Environment

| fcitx5     | 5.1.19            |
| ---------- | ----------------- |
| KDE Plasma | 6.6.3             |
| Linux      | 6.19.10-1-cachyos |

### Details

```bash
Fcitx should be launched by KWin under KDE Wayland in order to use Wayland input method frontend. This can improve the experience when using Fcitx on Wayland. To configure this, you need to go to "System Settings" -> "Virtual keyboard" and select "Fcitx 5" from it. You may also need to disable tools that launches input method, such as imsettings on Fedora, or im-config on Debian/Ubuntu. For more details see https://fcitx-im.org/wiki/Using_Fcitx_5_on_Wayland#KDE_Plasma
```


## 2. Root Cause
Input method initialisation issue

## 3. Solution
Modify environment variables

### Steps

In `.bashrc` or `.zshrc` or `.xprofile` or `.pam_environment` or `/etc/environment`

```bash
XMODIFIERS=@im=fcitx
```
- Remove `GTK_IM_MODULE` and `QT_IM_MODULE`

