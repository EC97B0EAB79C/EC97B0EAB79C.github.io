---
title: Tmux Cheat Sheet
tags:
  - CheatSheet
---

| Command                            | Description                                                |
|:---------------------------------- |:---------------------------------------------------------- |
| `tmux new -s SessionName`          | Create a new session with the specified name.              |
| `tmux ls`                          | List all active sessions.                                  |
| `tmux a -t SessionName`            | Attach to an existing session by name.                     |
| `tmux kill-session -t SessionName` | Kill a specific session by name.                           |
| `Ctrl+B D`                         | Detach from the current session.                           |
| `Ctrl+B C`                         | Create a new window in the current session.                |
| `Ctrl+B N` / `Ctrl+B P`            | Navigate to the next or previous window.                   |
| `Ctrl+B 0, 1, 2, ...`              | Jump directly to a window by its number.                   |
| `Ctrl+B %`                         | Split the current window horizontally into panes.          |
| `Ctrl+B "`                         | Split the current window vertically into panes.            |
| `Ctrl+B Arrow Key`                 | Switch between panes.                                      |
| `Ctrl+B X`                         | Close the current pane.                                    |
| `Ctrl+B :`                         | Enter command mode to execute more advanced tmux commands. |
| `Ctrl+B ?`                         | Display a list of all available keybindings.               |
