---
title: Linux User Management
---
## Add user
```bash
useradd -m -d /path/to/home/directory username
```

- `useradd`: The command to add a new user.
- `-m`: This option tells `useradd` to create the home directory if it doesn't exist.
- `-d /path/to/home/directory`: This specifies the new user's home directory.
- `username`: The name of the new user.

### Set Passwd
```bash
sudo passwd username
```

### Add User to Group
```bash
sudo usermod -aG groupname username
groups username
```

#### Add su
```bash
sudo usermod -aG sudo username
```

- `usermod` is the command to modify a user's attributes.
- `-aG sudo` adds the user to the `sudo` group.
- `username` is the name of the user.

### Permission
```bash
setfacl -m u:username:rx /path/to/directory
```

### Set shell to Bash
```shell
sudo chsh -s /bin/bash username
```

## Delete User
```
sudo deluser username
```