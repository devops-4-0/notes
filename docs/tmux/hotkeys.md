[Main menu](../../README.md)

# TMUX CHEAT SHEET
---

Here's a **tmux cheat sheet** covering the most common commands and shortcuts for managing terminal multiplexing:

---

### **Getting Started**
- **Start a new session**:
  ```bash
  tmux
  ```
- **Start a named session**:
  ```bash
  tmux new -s session_name
  ```
- **Attach to a session**:
  ```bash
  tmux attach -t session_name
  ```
- **List sessions**:
  ```bash
  tmux ls
  ```
- **Detach from a session**:
  Press `Ctrl-b` then `d`.

---

### **Prefix Key**
The **default prefix key** is:
- **`Ctrl-b`**
- All tmux shortcuts are triggered after pressing the prefix key.

You can customize it (e.g., change to `Ctrl-a`) in `.tmux.conf`:
```bash
unbind C-b
set-option -g prefix C-a
bind-key C-a send-prefix
```

---

### **Window Management**
- **Create a new window**:
  `Ctrl-b c`
- **List all windows**:
  `Ctrl-b w`
- **Switch to the next window**:
  `Ctrl-b n`
- **Switch to the previous window**:
  `Ctrl-b p`
- **Select a specific window**:
  `Ctrl-b <window_number>`
- **Rename the current window**:
  `Ctrl-b ,`
- **Kill the current window**:
  `Ctrl-b &`

---

### **Pane Management**
- **Split window horizontally**:
  `Ctrl-b "`
- **Split window vertically**:
  `Ctrl-b %`
- **Switch between panes**:
  `Ctrl-b o`
- **Move to the next pane**:
  `Ctrl-b ;`
- **Resize panes**:
  - `Ctrl-b <arrow_keys>`: Resize in the direction of the arrow.
- **Swap panes**:
  `Ctrl-b {` (move pane left)  
  `Ctrl-b }` (move pane right)
- **Kill the current pane**:
  `Ctrl-b x`

---

### **Session Management**
- **Detach from a session**:
  `Ctrl-b d`
- **Kill a session**:
  ```bash
  tmux kill-session -t session_name
  ```
- **Switch between sessions**:
  ```bash
  tmux switch -t session_name
  ```

---

### **Copy and Paste Mode**
- **Enter copy mode**:
  `Ctrl-b [`
- **Scroll up/down**:
  Use arrow keys or `PageUp`/`PageDown`.
- **Start selection**:
  Press `Space`.
- **Copy selection**:
  Press `Enter`.
- **Paste buffer**:
  `Ctrl-b ]`

---

### **Customize Status Bar**
- **Reload tmux configuration**:
  ```bash
  tmux source-file ~/.tmux.conf
  ```
- **Show time in status bar**:
  Add to `.tmux.conf`:
  ```bash
  set -g status-right "%H:%M:%S"
  ```

---

### **Common Commands**
Run these commands in a terminal or after pressing `Ctrl-b :`:

| Command                           | Description                                      |
|-----------------------------------|--------------------------------------------------|
| `tmux new -s session_name`        | Create a new session with a name.               |
| `tmux kill-session -t session_name` | Kill a specific session.                       |
| `tmux kill-server`                | Kill the tmux server and all sessions.          |
| `tmux rename-session new_name`    | Rename the current session.                     |
| `tmux list-keys`                  | List all key bindings.                          |
| `tmux list-panes`                 | Show information about panes in the current window. |
| `tmux list-windows`               | List all windows in the current session.        |

---

### **Other Useful Shortcuts**
- **Reload configuration**:
  `Ctrl-b :` then type `source-file ~/.tmux.conf`
- **Switch last active window**:
  `Ctrl-b l`
- **Show tmux command prompt**:
  `Ctrl-b :`

---

[Main menu](../../README.md)