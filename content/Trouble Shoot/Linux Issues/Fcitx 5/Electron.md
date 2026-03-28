---
title: Fcitx 5 Not Working on Electron Application
date: 2026-03-28
---


## Problem Description
Fcitx 5 Input not working no Electron applications

### Environment

| fcitx5     | 5.1.19            |
| ---------- | ----------------- |
| KDE Plasma | 6.6.3             |
| Linux      | 6.19.10-1-cachyos |

## 2. Root Cause
Electron application do not natively hook into the `text-input-v3` Wayland protocol by default.

## 3. Solution
Set explicit command-line flags.

### Steps
In `~/.config/{application}-flags.conf`:
```bash
--enable-features=UseOzonePlatform
--ozone-platform=wayland
--enable-wayland-ime
```
