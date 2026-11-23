---
title: 7-Zip Cheat Sheet
tags:
  - CheatSheet
---


## Commands

**Create an Encrypted Archive**
```bash
7z a -p -mhe=on -t7z archive.7z /path/to/files/
```
- `a`: Add files to the archive.
- `-p`: Ask for a password.
- `-mhe=on`: Turn on header encryption.
- `-t7z`: Set the archive type to 7z.