[Main menu](../../README.md)

# About TMUX

### **General Information About TMUX**

**tmux** (Terminal Multiplexer) is a powerful command-line tool used in Unix-like operating systems to manage multiple terminal sessions within a single terminal window. It is commonly used by system administrators, developers, and power users for multitasking in a terminal environment.

---

### **Key Features of TMUX**

1. **Session Management**:
   - tmux allows you to create multiple independent sessions. Each session can hold multiple windows and panes.
   - Sessions persist even if the terminal window is closed or the user is disconnected (e.g., SSH disconnection).

2. **Window and Pane Management**:
   - You can split windows into panes horizontally or vertically and navigate between them easily.
   - Each pane can run a separate terminal session.

3. **Customizable and Scriptable**:
   - tmux is highly configurable via its configuration file (`~/.tmux.conf`).
   - Users can define key bindings, appearance, and behavior.

4. **Remote Workflows**:
   - tmux is widely used in remote workflows via SSH, as it enables sessions to persist even when the connection is lost.

5. **Copy and Paste**:
   - tmux provides a built-in mechanism to scroll through terminal output, select text, and copy/paste across panes and sessions.

6. **Mouse Support**:
   - It supports mouse interaction for scrolling, resizing panes, and selecting text.

---

### **Common Use Cases**
- **Long-Running Tasks**:
  Run tasks in a tmux session, detach from it, and reattach later to check progress without losing the terminal session.
  
- **Multitasking**:
  Split a terminal into multiple panes/windows for tasks like monitoring logs, editing files, and running commands simultaneously.

- **Remote Work**:
  Run tmux on remote servers over SSH to maintain persistent sessions that survive disconnections.

- **Development and Debugging**:
  Use tmux for organizing different terminals needed for development (e.g., running a server, database, and editor in separate panes).

---

### **Key Concepts**

1. **Sessions**:
   A tmux session is a container for managing terminal windows and panes. Sessions can be named and detached, allowing for reattachment later.

2. **Windows**:
   A window is a virtual terminal within a tmux session. You can create multiple windows and switch between them.

3. **Panes**:
   Panes are subdivisions of a window. You can split a window horizontally or vertically into multiple panes.

---

### **Key Benefits**
- **Efficiency**: Save time and increase productivity by managing multiple terminal sessions in a single window.
- **Persistence**: Keep tasks running even if the terminal is closed or disconnected.
- **Organization**: Organize terminal workflows by separating tasks into different panes and windows.
- **Cross-Terminal Workflow**: Easily switch between sessions across different machines.

---

### **How TMUX Works**
When you start tmux, it creates a **server process** that runs in the background and manages sessions, windows, and panes. This server persists even if you close your terminal, allowing you to reattach to the session later.

---

### **Installation**

1. **On Debian/Ubuntu**:
   ```bash
   sudo apt update
   sudo apt install tmux
   ```

2. **On CentOS/RHEL**:
   ```bash
   sudo yum install tmux
   ```

3. **On macOS**:
   ```bash
   brew install tmux
   ```

4. **From Source**:
   - Download and compile the latest version from the [tmux GitHub repository](https://github.com/tmux/tmux).

---

### **Configuration File**

The configuration file is located at:
```bash
~/.tmux.conf
```

Here’s an example `.tmux.conf` file:
```bash
# Set prefix key to Ctrl-a
unbind C-b
set-option -g prefix C-a
bind-key C-a send-prefix

# Enable mouse support
set -g mouse on

# Set status bar style
set -g status-bg black
set -g status-fg green
set -g status-left "Session: #S"
```

Reload the configuration:
```bash
tmux source-file ~/.tmux.conf
```

---

### **Comparison with Alternatives**
- **tmux vs screen**:
  - `tmux` is considered more modern and customizable than `screen`.
  - tmux has better support for window splitting and scripting.

- **tmux vs Byobu**:
  - `Byobu` is a wrapper around tmux or screen, providing a more user-friendly interface.

---

### **tmux Limitations**
1. **Learning Curve**:
   - Beginners may find it challenging to get started due to its powerful and complex features.
   
2. **No Native GUI**:
   - It’s strictly a command-line tool, which might be less appealing to users who prefer graphical interfaces.

---


[Main menu](../../README.md)