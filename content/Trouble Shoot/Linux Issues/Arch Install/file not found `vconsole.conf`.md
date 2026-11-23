---
title: file not found `vconsole.conf`
date: 2026-01-18
---


## 1. Problem Description

### Details
This error appears when you install the packages from the install ISO:
```bash
file not found: /etc/vconsole.conf
```

## 2. Root Cause
- The file `/etc/vconsole.conf` is missing.

## 3. Solution
```bash
echo "KEYMAP=us" > /mnt/etc/vconsole.conf
```
