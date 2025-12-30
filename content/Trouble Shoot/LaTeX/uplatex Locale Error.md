---
title: "`uplatex` Locale Error"
date: 2025-12-25
---


## Problem Description
### Environment

| OS       | Linux arch-asus 6.18.2-arch2-1      |
| -------- | ----------------------------------- |
| e-upTeX  | 3.141592653-p4.1.2-u2.00-250202-2.6 |
| kpathsea | 6.4.2/dev                           |
| ptexenc  | 1.5.2/dev                           |

### Details

Following warning displays when compiling
```bash
Process started: uplatex -synctex=1 -interaction=nonstopmode "main".tex

kpathsea: Running mktexfmt uplatex.fmt
perl: warning: Setting locale failed. perl: warning: Please check that your locale settings: LANGUAGE = (unset), LC_ALL = (unset), LC_CTYPE = (unset), LC_NUMERIC = (unset), LC_COLLATE = (unset), LC_TIME = (unset), LC_MESSAGES = (unset), LC_MONETARY = (unset), LC_ADDRESS = (unset), LC_IDENTIFICATION = (unset), LC_MEASUREMENT = (unset), LC_PAPER = (unset), LC_TELEPHONE = (unset), LC_NAME = (unset), LANG = "en_US.UTF-8" are supported and installed on your system. perl: warning: Falling back to the standard locale ("C").
```

## 2. Root Cause

- System's locale settings are defined in environment variables
- But have not been generated on the system

## 3. Solution

Generate missing locales

### Steps

1. Edit `/etc/locale.gen` (sudo):
	```
	en_US.UTF-8 UTF-8
	```
2. Generate
	```bash
	sudo locale-gen
	```
3. Verify
	```bash
	cat /etc/locale.conf | grep LANG=en_US.UTF-8
	```
4. Apply changes
	```bash
	source /etc/profile
	```