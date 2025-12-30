---
title: "`uplatex` Japanese Compile Error"
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
mktexfmt: mktexfmt is using the following fmtutil.cnf files (in precedence order): mktexfmt: /etc/texmf/web2c/fmtutil.cnf mktexfmt: mktexfmt is using the following fmtutil.cnf file for writing changes: mktexfmt: /home/c/.texlive/texmf-config/web2c/fmtutil.cnf
mktexfmt [INFO]: writing formats under /home/c/.texlive/texmf-var/web2c
mktexfmt [INFO]: Did not find entry for byfmt=uplatex skipped mktexfmt [INFO]: disabled formats: 1 mktexfmt [INFO]: not selected formats: 38 mktexfmt [INFO]: total formats: 39 mktexfmt [INFO]: exiting with status 0
Process exited with error(s)
```

## 2. Root Cause

- Configuration missing

## 3. Solution

Install `texlive-langjapanese` package

### Steps
1. Install:
	```bash
	sudo pacman -S texlive-langjapanese
	```
2. Rebuild the formats
	```bash
	sudo fmtutil-sys --all
	```

