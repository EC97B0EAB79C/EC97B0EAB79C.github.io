---
title: ADB Cheat Sheet
tags:
  - CheatSheet
---
## Commands
### APK

**Install an APK**
```bash
adb install path/to/your_app.apk
```

**Run an APK**
```bash
adb shell am start -n com.yourpackage/.YourMainActivity
```

**Stop an APK**
```bash
adb shell am force-stop package_name
```