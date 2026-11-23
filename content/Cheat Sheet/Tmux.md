---
title: tmux Cheat Sheet
tags:
  - CheatSheet
---

| Command                            | Description                                                |
|:---------------------------------- |:---------------------------------------------------------- |
| `tmux new -s SessionName`          | Create a new session with this name.                       |
| `tmux ls`                          | List all active sessions.                                  |
| `tmux a -t SessionName`            | Attach to an existing session by its name.                 |
| `tmux kill-session -t SessionName` | Stop a session by its name.                                |
| `Ctrl+B D`                         | Detach from the current session.                           |
| `Ctrl+B C`                         | Create a new window in the current session.                |
| `Ctrl+B N` / `Ctrl+B P`            | Go to the next or the previous window.                     |
| `Ctrl+B 0, 1, 2, ...`              | Go to a window by its number.                              |
| `Ctrl+B %`                         | Split the current window horizontally into panes.          |
| `Ctrl+B "`                         | Split the current window vertically into panes.            |
| `Ctrl+B Arrow Key`                 | Switch between panes.                                      |
| `Ctrl+B X`                         | Close the current pane.                                    |
| `Ctrl+B :`                         | Enter command mode to run advanced tmux commands.          |
| `Ctrl+B ?`                         | Show a list of all available keybindings.                  |
