---
title: Fcitx 5 Not Working on Electron Application
date: 2026-03-28
---


## 1. Problem Description
Fcitx 5 input does not work in Electron applications.

### Environment

| fcitx5     | 5.1.19            |
| ---------- | ----------------- |
| KDE Plasma | 6.6.3             |
| Linux      | 6.19.10-1-cachyos |

## 2. Root Cause
By default, Electron applications do not use the `text-input-v3` Wayland protocol natively.

## 3. Solution
Set the command-line flags explicitly.

### Steps
Add these lines to `~/.config/{application}-flags.conf`:
```bash
--enable-features=UseOzonePlatform
--ozone-platform=wayland
--enable-wayland-ime
```
