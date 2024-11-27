Scrolling in a tmux terminal is done using **copy mode**. Here's how you can do it:

# Mouse Scrolling in TMUX

---

### **Enable Copy Mode for Scrolling**
1. **Enter Copy Mode**:
   Press `Ctrl-b [`  
   This switches the current pane into copy mode, allowing you to scroll.

2. **Scroll in Copy Mode**:
   - Use the **arrow keys** (`↑`/`↓`) to scroll line by line.
   - Use `PageUp` and `PageDown` for faster navigation.
   - You can also use **Vim-style keys**:
     - `k`: Scroll up one line.
     - `j`: Scroll down one line.
     - `Ctrl-u`: Scroll up half a page.
     - `Ctrl-d`: Scroll down half a page.

3. **Exit Copy Mode**:
   Press `q` to return to normal terminal interaction.

---

### **Enable Mouse Scrolling**
If you prefer to scroll using the mouse, enable mouse support in your `.tmux.conf`:

#### **Enable Mouse Support**:
1. Edit your `.tmux.conf` file:
   ```bash
   nano ~/.tmux.conf
   ```
2. Add the following line:
   ```bash
   set -g mouse on
   ```
3. Reload the configuration:
   ```bash
   tmux source-file ~/.tmux.conf
   ```

Now you can use your mouse wheel to scroll within tmux.

---

### **Copying Text While Scrolling**
If you want to copy text while scrolling:
1. Enter copy mode: `Ctrl-b [`.
2. Use the arrow keys or mouse to navigate to the desired text.
3. Press `Space` to start selecting text.
4. Navigate to the end of the selection and press `Enter` to copy it.
5. Paste the copied text by pressing `Ctrl-b ]`.

---

### **Troubleshooting Mouse Scrolling**
If mouse scrolling doesn't work:
1. Ensure the terminal emulator supports mouse events (e.g., `xterm`, `gnome-terminal`, or `tmux` in an SSH session).
2. Check that `set -g mouse on` is active.
3. Verify terminal multiplexer settings don't interfere with tmux.

