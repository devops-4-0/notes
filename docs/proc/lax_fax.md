[Main menu](../../README.md)

### **Understanding `ps fax` and `ps lax`**

The `ps` command with `fax` and `lax` options provides specific information about processes in different formats. These options use a combination of **BSD-style options** and **Linux-standard flags** to modify the output.

---

### **1. `ps fax`: Hierarchical Process Display**

#### **Description**
- The `f` option displays processes in a **hierarchical tree format**, showing parent-child relationships (useful for visualizing process trees).
- The `a` option lists processes associated with all users' terminals.
- The `x` option includes processes without a controlling terminal (e.g., background or daemon processes).

#### **Command**:
```bash
ps fax
```

#### **Example Output**:
```
  PID TTY      STAT   TIME COMMAND
    1 ?        Ss     0:01 /sbin/init
   85 ?        Ss     0:00  \_ /lib/systemd/systemd-journald
  230 ?        Ss     0:00  \_ /lib/systemd/systemd-udevd
  345 tty1     S      0:00  \_ /bin/login --    
  400 tty1     S+     0:01      \_ /bin/bash
  450 tty1     R+     0:00          \_ htop
```

#### **Key Points**:
- **Tree Structure**: Processes are shown hierarchically, with child processes indented and connected to their parent using `_`.
- **TTY**: Includes terminal-based processes and those without a controlling terminal (`?` under `TTY`).

#### **Use Case**:
- Ideal for debugging **process relationships** (e.g., which processes a parent process has spawned).

---

### **2. `ps lax`: Detailed Information with State Codes**

#### **Description**
- The `l` option displays processes in a **long format**, showing more details such as priority, process group, and session ID.
- The `a` option lists processes associated with all users' terminals.
- The `x` option includes processes without a controlling terminal.

#### **Command**:
```bash
ps lax
```

#### **Example Output**:
```
 F   UID   PID  PPID PRI  NI   VSZ  RSS  WCHAN  STAT TTY    TIME COMMAND
 4     0     1     0  20   0  4892  368  ep_pol Ss   ?      0:01 /sbin/init
 1     0    85     1  20   0  6204 1100  ep_pol Ss   ?      0:00 /lib/systemd/systemd-journald
 1     0   230     1  20   0 10500  820  ep_pol Ss   ?      0:00 /lib/systemd/systemd-udevd
 5  1000   345     1  20   0  6044 1032  ep_pol Ss   tty1   0:00 /bin/login --
 5  1000   400   345  20   0  9800 1700  ep_pol S+   tty1   0:01 /bin/bash
 5  1000   450   400  20   0 15560 2576  -      R+   tty1   0:00 htop
```

#### **Field Descriptions**:
| **Field**  | **Description**                                                                 |
|------------|---------------------------------------------------------------------------------|
| `F`        | Flags related to the process (`4` = superuser process).                        |
| `UID`      | User ID of the process owner.                                                  |
| `PID`      | Process ID.                                                                    |
| `PPID`     | Parent process ID.                                                             |
| `PRI`      | Priority (lower is higher priority).                                           |
| `NI`       | Nice value (affects process priority).                                         |
| `VSZ`      | Virtual memory size in KB.                                                    |
| `RSS`      | Resident Set Size (physical memory usage in KB).                               |
| `WCHAN`    | Kernel function where the process is waiting (e.g., `ep_pol`).                |
| `STAT`     | Current state of the process (e.g., `R`, `S`, `Z`, `D`).                      |
| `TTY`      | Terminal associated with the process (if any).                                |
| `TIME`     | Total CPU time used by the process.                                            |
| `COMMAND`  | Command that started the process.                                              |

#### **Use Case**:
- Ideal for in-depth analysis of process **resource usage**, **priority**, and **scheduling**.

---

### **Key Differences Between `ps fax` and `ps lax`**

| **Feature**       | **`ps fax`**                              | **`ps lax`**                              |
|--------------------|-------------------------------------------|-------------------------------------------|
| **Hierarchy**      | Displays processes in a tree structure.  | Does not show process hierarchy.          |
| **Output Format**  | Simplified format focusing on hierarchy. | Long, detailed output with technical info.|
| **Use Case**       | Debugging parent-child relationships.    | Resource usage, priority, and scheduling. |

---

### **Practical Scenarios**

#### **Monitor System Services Hierarchically**
```bash
ps fax | grep systemd
```
- View how `systemd` services and daemons are structured.

#### **Analyze Process Priorities**
```bash
ps lax | sort -nk5 | head
```
- Sort processes by priority (field `PRI`) to find the most prioritized ones.

#### **Investigate Zombie Processes**
```bash
ps lax | grep Z
```
- List all zombie processes (state `Z` in `STAT`).

---

[Main menu](../../README.md)