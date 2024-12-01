[Main menu](../../README.md)

### **User Limits in Linux**

User limits in Linux control system resource usage for individual users and processes. These limits ensure fair resource allocation, protect against resource exhaustion, and maintain system stability.

Linux uses **PAM (Pluggable Authentication Modules)** and the shell's `ulimit` command to enforce these limits.

---

### **Types of Limits**
1. **Soft Limits**:
   - A threshold that users or processes can temporarily exceed.
   - Users can increase the soft limit up to the corresponding hard limit within a session.

2. **Hard Limits**:
   - The maximum value for a resource that users or processes cannot exceed unless they have root privileges.
   - Hard limits act as an upper ceiling for the soft limits.

---

### **Where Limits Are Defined**
1. **Global configuration**: `/etc/security/limits.conf` or files under `/etc/security/limits.d/`
2. **Current session**: Modified using the `ulimit` command or within shell initialization files (e.g., `.bashrc`).

---

### **Resource Types for Limits**
Common resources managed by user limits include:
- **CPU time**: Maximum CPU time in seconds a process can consume.
- **File size**: Maximum size of files that can be created.
- **Memory**: Maximum memory a process can allocate.
- **Open files**: Maximum number of open file descriptors.
- **Processes**: Maximum number of processes a user can create.
- **Locked memory**: Maximum amount of memory that can be locked into RAM.

---

### **Viewing Limits**

#### **Using `ulimit` Command**
- Show all limits:
  ```bash
  ulimit -a
  ```
  Example output:
  ```
  core file size          (blocks, -c) 0
  data seg size           (kbytes, -d) unlimited
  scheduling priority     (-e) 0
  file size               (blocks, -f) unlimited
  pending signals         (-i) 15402
  max locked memory       (kbytes, -l) 64
  max memory size         (kbytes, -m) unlimited
  open files              (-n) 1024
  ```

#### **Using `ulimit` Options**
- Display a specific limit:
  ```bash
  ulimit -n   # Open files
  ulimit -u   # Max user processes
  ```

#### **Viewing Hard and Soft Limits**
- Soft limit:
  ```bash
  ulimit -Sn
  ```
- Hard limit:
  ```bash
  ulimit -Hn
  ```

---

### **Setting Limits**

#### **Temporary Session Limits**
Set soft or hard limits for the current session using `ulimit`:
- Set soft limit for open files:
  ```bash
  ulimit -Sn 2048
  ```
- Set hard limit for open files:
  ```bash
  ulimit -Hn 4096
  ```

---

#### **Permanent Limits (Per User)**
1. **Edit `/etc/security/limits.conf`** or create a file in `/etc/security/limits.d/`:
   ```
   username   soft   nofile   2048
   username   hard   nofile   4096
   username   soft   nproc    1000
   username   hard   nproc    2000
   ```

2. **Restart the session** for changes to take effect.

---

### **Practical Examples**

#### **Example 1: Limiting Open Files**
1. Check current open file limit:
   ```bash
   ulimit -n
   # Output: 1024
   ```

2. Temporarily increase the limit:
   ```bash
   ulimit -n 2048
   ```

3. Set permanent limits for user `john`:
   - Add to `/etc/security/limits.conf`:
     ```
     john   soft   nofile   2048
     john   hard   nofile   4096
     ```

---

#### **Example 2: Limiting Processes**
1. Temporarily limit processes to 500:
   ```bash
   ulimit -u 500
   ```

2. Set permanent limits:
   - Add to `/etc/security/limits.conf`:
     ```
     john   soft   nproc   500
     john   hard   nproc   1000
     ```

---

### **Notes**
- Hard limits require root privileges to modify.
- PAM's `pam_limits.so` must be enabled in `/etc/pam.d/common-session` and `/etc/pam.d/common-session-noninteractive` for limits in `limits.conf` to work:
  ```
  session required pam_limits.so
  ```

---

### **Example Scenarios**

#### **Preventing Resource Exhaustion by a Single User**
- Limit `nproc` to prevent a user from starting too many processes and overwhelming the system:
  ```
  user1   soft   nproc   100
  user1   hard   nproc   200
  ```

#### **Restricting File Creation Sizes**
- Limit file sizes created by a user:
  ```
  user2   soft   fsize   1048576   # 1GB
  ```

[Main menu](../../README.md)