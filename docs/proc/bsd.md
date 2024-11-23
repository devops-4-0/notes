[Main menu](../../README.md)

### **BSD Options in the `ps` Command**

BSD options are commonly used with the `ps` command for a simpler, compact, and versatile display format. Unlike standard UNIX options, BSD-style options do not require a leading dash (`-`).

---

### **1. Common BSD Options and Their Usage**

| **Option** | **Description**                                                                 |
|------------|---------------------------------------------------------------------------------|
| `a`        | Lists processes associated with all terminals (not limited to the current user). |
| `u`        | Displays user-oriented output, including owner, CPU, memory usage, and process. |
| `x`        | Lists processes without a controlling terminal (e.g., daemon processes).        |
| `aux`      | A combination of `a`, `u`, and `x` to display all processes in a user-friendly format. |

---

### **2. Detailed Examples**

#### **a. `ps a`**
- **Description**: Shows processes with associated terminals for the current user.
- **Command**:
  ```bash
  ps a
  ```
- **Output**:
  ```
    PID TTY      STAT   TIME COMMAND
   1234 pts/0    R+     0:00 bash
   5678 pts/1    S+     0:02 vim
  ```
- Includes `PID`, terminal (`TTY`), process state (`STAT`), and command.

---

#### **b. `ps u`**
- **Description**: Displays user-oriented information about processes, including user, CPU, and memory usage.
- **Command**:
  ```bash
  ps u
  ```
- **Output**:
  ```
  USER       PID %CPU %MEM    VSZ   RSS TTY      STAT START   TIME COMMAND
  root       123  0.0  0.1  48200  3924 tty1     Ss   10:00   0:00 /sbin/init
  john      2345  0.2  1.0 134820 10240 pts/0    R+   10:15   0:05 /usr/bin/python3 script.py
  ```
- **Fields Explained**:
  - **USER**: Owner of the process.
  - **%CPU**: CPU usage percentage.
  - **%MEM**: Memory usage percentage.
  - **VSZ**: Virtual memory size in KB.
  - **RSS**: Resident Set Size (physical memory in KB).
  - **STAT**: Process state.

---

#### **c. `ps x`**
- **Description**: Lists all processes, including those without a controlling terminal (like background or daemon processes).
- **Command**:
  ```bash
  ps x
  ```
- **Output**:
  ```
    PID TTY      STAT   TIME COMMAND
   3456 ?        Ss     0:01 /usr/sbin/cron
   4567 ?        Sl     0:02 /usr/bin/dbus-daemon
   5678 ?        S      0:00 /usr/bin/ssh-agent
  ```
- Processes with a `?` under the `TTY` column indicate they lack a controlling terminal.

---

#### **d. `ps aux`**
- **Description**: Combines `a`, `u`, and `x` to show all processes with detailed user information and includes processes without a terminal.
- **Command**:
  ```bash
  ps aux
  ```
- **Output**:
  ```
  USER       PID %CPU %MEM    VSZ   RSS TTY      STAT START   TIME COMMAND
  root         1  0.0  0.1  48200  3924 ?        Ss   10:00   0:00 /sbin/init
  john      2345  0.2  1.0 134820 10240 pts/0    R+   10:15   0:05 /usr/bin/python3 script.py
  root       1234  0.1  0.5  92040  5032 ?        Ss   10:05   0:02 /usr/bin/apache2 -k start
  ```
- **Benefits**:
  - Combines user info, CPU/memory usage, and terminal status.
  - Useful for system-wide process monitoring.

---

#### **e. Sorting with BSD Options**
- Sort processes by resource usage.
- Example: Sort by CPU usage:
  ```bash
  ps aux --sort=-%cpu
  ```
- Example: Sort by memory usage:
  ```bash
  ps aux --sort=-%mem
  ```

---

### **3. Combining BSD Options**

You can combine BSD options for more tailored outputs:
- **View all processes, showing only user-oriented information**:
  ```bash
  ps axu
  ```
- **Display processes with specific columns and sort**:
  ```bash
  ps aux | head -n 10
  ```
- **Filter for a specific user**:
  ```bash
  ps aux | grep john
  ```

---

### **4. Key Takeaways**
- BSD options are compact and often used for quick, system-wide process monitoring.
- The `ps aux` combination is the most common for admins to view all processes.
- Combine with `grep` or `awk` for refined outputs.

[Main menu](../../README.md)