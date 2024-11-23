[Main menu](../../README.md)

### **`ps` Command in Linux**

The `ps` (process status) command displays information about currently running processes. It is a powerful tool for monitoring and managing processes on a Linux system.

---

### **1. Commonly Used Options**

#### **a. Output Format Options**
1. **`-e`** or **`--all`**
   - Shows all processes on the system.
   - Example:
     ```bash
     ps -e
     ```
   - Output includes all processes, not limited to the user's session.

2. **`-f`** or **`--full`**
   - Displays a full-format listing, including the process tree and additional details like the parent process ID (PPID).
   - Example:
     ```bash
     ps -f
     ```

3. **`-o`** or **`--format`**
   - Customizes the output by specifying the desired columns.
   - Example:
     ```bash
     ps -eo pid,ppid,cmd
     ```
   - Displays only process ID, parent process ID, and command.

#### **b. Filtering Options**
1. **`-u USER`**
   - Displays processes belonging to a specific user.
   - Example:
     ```bash
     ps -u root
     ```

2. **`-p PID`**
   - Shows information about a specific process by its PID.
   - Example:
     ```bash
     ps -p 1234
     ```

3. **`--ppid PPID`**
   - Lists processes with a specific parent process ID.
   - Example:
     ```bash
     ps --ppid 1
     ```

#### **c. Interactive or Repeated Display**
- For real-time monitoring, use `top` or `htop`, as `ps` is a one-time snapshot.

#### **d. BSD-Style Options**
1. **`aux`**
   - Combines the functionality of `-e`, `-f`, and additional user info.
   - Example:
     ```bash
     ps aux
     ```
   - Key fields include:
     - **USER**: The user who started the process.
     - **%CPU**: CPU usage.
     - **%MEM**: Memory usage.
     - **COMMAND**: The command used to start the process.

---

### **2. Useful Examples**

#### **View All Processes**
```bash
ps -e
```
- Lists all processes on the system.

#### **View Processes for a Specific User**
```bash
ps -u john
```
- Displays all processes owned by user `john`.

#### **Custom Output Columns**
```bash
ps -eo pid,ppid,comm,state
```
- Output includes PID, parent PID, command, and state.

#### **View a Process Tree**
```bash
ps -ef --forest
```
- Displays the hierarchy of processes in a tree format.

#### **Find Processes by Name**
```bash
ps -C apache2
```
- Lists all processes with the name `apache2`.

#### **Filter by Multiple Conditions**
```bash
ps -eo pid,user,%cpu,cmd --sort=-%cpu | head -n 10
```
- Displays the top 10 CPU-consuming processes, sorted in descending order of CPU usage.

#### **Monitor a Specific PID**
```bash
ps -p 1234 -o pid,comm,state,etime
```
- Displays PID, command name, state, and elapsed time for process 1234.

---

### **3. Explanation of Common Options**

| **Option**     | **Description**                                                                 |
|-----------------|---------------------------------------------------------------------------------|
| `-e`           | Lists all processes in the system.                                              |
| `-f`           | Full format listing, includes PPID and other details.                          |
| `-o`           | Customizable output format by specifying desired columns.                      |
| `aux`          | Displays all processes with additional user and resource usage information.     |
| `-p PID`       | Filters processes by a specific process ID.                                     |
| `--ppid PPID`  | Filters processes by a specific parent process ID.                              |
| `-C COMMAND`   | Lists processes by command name.                                                |
| `--forest`     | Displays processes in a hierarchical tree structure.                            |
| `--sort=KEY`   | Sorts the output based on the specified column, e.g., `--sort=-%cpu`.           |

---

### **4. Key Output Columns**

| **Column**      | **Description**                                                                  |
|------------------|----------------------------------------------------------------------------------|
| `PID`           | Process ID.                                                                     |
| `PPID`          | Parent Process ID.                                                              |
| `USER`          | User who owns the process.                                                      |
| `%CPU`          | Percentage of CPU being used by the process.                                    |
| `%MEM`          | Percentage of memory being used by the process.                                 |
| `VSZ`           | Virtual memory size used by the process.                                        |
| `RSS`           | Resident Set Size (physical memory) used by the process.                        |
| `STAT`          | Current state of the process (`R`, `S`, `D`, `T`, `Z`).                         |
| `COMMAND`       | The command that started the process.                                           |

---

### **5. Practical Tips**
- Use `ps` with `grep` to find specific processes:
  ```bash
  ps aux | grep nginx
  ```
- Combine with `awk` for extracting specific fields:
  ```bash
  ps aux | awk '{print $2, $11}'
  ```

[Main menu](../../README.md)