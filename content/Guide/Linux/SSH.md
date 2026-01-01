---
title: SSH Setup
---
## Setup
### Install

```
sudo pacman -S openssh
```

#### Enable SSH Server
```bash
sudo systemctl start sshd
sudo systemctl enable sshd
```

### `ssh-agent`

1. Enable the user service
   ```bash
   systemctl --user enable --now ssh-agent
   ```
2. Add to `.bashrc`:
   ```bash
   export SSH_AUTH_SOCK="$XDG_RUNTIME_DIR/ssh-agent.socket"
   ```
3. Add to `~/.ssh/config`:
   ```bash
   AddKeysToAgent yes
   ```