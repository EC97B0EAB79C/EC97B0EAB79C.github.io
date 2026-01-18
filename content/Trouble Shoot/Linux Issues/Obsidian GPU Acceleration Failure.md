---
title: Obsidian GPU Acceleration Failure
date: 2026-01-18
---


## Problem Description
### Environment

| OS       | Linux arch-linux 6.18.5-arch1-1 |
| -------- | ------------------------------- |
| Obsidian | 1.11.4                          |

### Details
```bash
$ obsidian
2026-01-18 04:29:50 Loading main app package /usr/lib/obsidian/obsidian.asar
Ignored: Error: ENOENT: no such file or directory, open 'redacted'
2026-01-18 04:29:50 Checking for update using Github
2026-01-18 04:29:51 Success.
2026-01-18 04:29:51 Latest version is 1.11.4
2026-01-18 04:29:51 App is up to date.
Xlib:  extension "DRI2" missing on display ":1".
libva error: vaGetDriverNames() failed with operation failed
[9869:0118/132951.112089:ERROR:media/gpu/vaapi/vaapi_wrapper.cc:1631] vaInitialize failed: operation failed
[9869:0118/132951.114004:ERROR:components/viz/service/main/viz_main_impl.cc:189] Exiting GPU process due to errors d
uring initialization
Xlib:  extension "DRI2" missing on display ":1".
libva error: vaGetDriverNames() failed with operation failed
[9934:0118/132951.286934:ERROR:media/gpu/vaapi/vaapi_wrapper.cc:1631] vaInitialize failed: operation failed
```

## 2. Root Cause
- GPU acceleration failure

## 3. Solution
### Temporary Fix
```bash
obsidian --disable-gpu
```

### Modify desktop entry
#### Steps
1. Copy desktop file
	```bash
	cp /usr/share/applications/obsidian.desktop ~/.local/share/applications/
	```
2. Edit `~/.local/share/applications/obsidian.desktop`
	```bash
	Exec=/usr/bin/obsidian --disable-gpu %U
	```
