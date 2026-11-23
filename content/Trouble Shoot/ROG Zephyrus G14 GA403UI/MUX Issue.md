---
title: ROG Zephyrus G14 GA403UI MUX Problem
date: 2025-12-23
---
> Note: This fix is temporary. An OS reinstall repaired the problem.

## 1. Problem Description
### Environment
| Device | ASUS Zephyrus G14 (GA403UI) |
| ------ | --------------------------- |
| OS     | Fedora Linux (KDE Plasma)   |
### Details

The laptop boots normally, but the internal main display fails to start after the BIOS stage.
- The ASUS manufacturer logo (white) appears on the internal screen
- Immediately after the logo, the internal screen goes black and stays off
- The external monitor works and shows the OS login screen/desktop
- Fedora Display Configuration does not detect the internal panel at all

## 2. Root Cause

The MUX switch stayed in a state that stopped the OS from sending video to the internal panel.
## 3. Solution

To repair the problem, force the GPU mode back to `hybrid` with the `supergfxctl` CLI tool.

### Steps

1. Check the current status of the graphics switch:
	```bash
	supergfxctl -s
	```

2. Force the mode to Hybrid:
	```bash
	supergfxctl -m Hybrid
	```

3. Restart the computer.