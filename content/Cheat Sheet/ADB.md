---
title: ADB Cheat Sheet
---
## Commands
### APK

**Install APK**
```bash
adb install path/to/your_app.apk
```

**Run APK**
```bash
adb shell am start -n com.yourpackage/.YourMainActivity
```

**Stop APK**
```bash
adb shell am force-stop package_name
```