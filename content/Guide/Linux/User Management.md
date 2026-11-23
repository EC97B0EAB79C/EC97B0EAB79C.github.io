---
title: Linux User Management
---
## Add user
```bash
useradd -m -d /path/to/home/directory username
```

- `useradd`: The command to add a new user.
- `-m`: This option makes `useradd` create the home directory if it does not exist.
- `-d /path/to/home/directory`: This option sets the home directory of the new user.
- `username`: The name of the new user.

### Set the Password
```bash
sudo passwd username
```

### Add User to Group
```bash
sudo usermod -aG groupname username
groups username
```

#### Give Sudo Rights
```bash
sudo usermod -aG sudo username
```

- `usermod` is the command that changes the attributes of a user.
- `-aG sudo` adds the user to the `sudo` group.
- `username` is the name of the user.

### Set Permissions
```bash
setfacl -m u:username:rx /path/to/directory
```

### Set the Shell to Bash
```shell
sudo chsh -s /bin/bash username
```

## Delete User
```
sudo deluser username
```