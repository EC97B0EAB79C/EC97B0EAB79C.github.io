---
title: ROG Zephyrus G14 GA403UI MUX Issue
date: 2025-12-23
---
## 1. Problem Description
### Environment
| Device | ASUS Zephyrus G14 (GA403UI) |
| ------ | --------------------------- |
| OS     | Fedora Linux (KDE Plasma)   |
### Details
The laptop boots normally, but the internal main display fails to initialize after the BIOS stage.
- The ASUS manufacturer logo (white) appears on the internal screen
- Immediately after the logo, the internal screen goes black and stays off
- The external monitor works and shows the OS login screen/desktop
- In Fedora Display Configuration, the internal panel is not detected at all

## 2. Root Cause
MUX switch became stuck in a state that prevented the OS from routing video to the internal panel
## 3. Solution
The issue was resolved forcibly switching the GPU mode back to `hybrid` using the `supergfxctl` CLI tool.

### Steps
1. Check the current status of the graphics switch:
	```bash
	supergfxctl -s
	```

2. Force the mode to Hybrid
	```bash
	supergfxctl -m Hybrid
	```

3. Reboot