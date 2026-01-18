---
title: file not found `vconsole.conf`
date: 2026-01-18
---


## Problem Description

### Details
Error when installing packages from install ISO
```bash
file not found: /etc/vconsole.conf
```

## 2. Root Cause
- `/etc/vconsole.conf` missing

## 3. Solution
```bash
echo "KEYMAP=us" > /mnt/etc/vconsole.conf
```
