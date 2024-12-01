[Main menu](../../README.md)

### **Configuring the `sudoers` File in Linux**

The `sudoers` file controls how users or groups gain administrative (root) privileges through the `sudo` command. Proper configuration ensures secure and controlled privilege escalation.

---

### **Key Guidelines**
1. **Edit the File Safely**:
   - Always use `visudo` to edit the `sudoers` file.
   - `visudo` checks the file for syntax errors before saving.

   **Command**:
   ```bash
   sudo visudo
   ```

2. **Backup the File**:
   - Before making changes, create a backup:
     ```bash
     sudo cp /etc/sudoers /etc/sudoers.bak
     ```

3. **Default Location**:
   - The main `sudoers` file is located at:
     ```
     /etc/sudoers
     ```

4. **File Permissions**:
   - Ensure `sudoers` file permissions are set correctly:
     ```bash
     ls -l /etc/sudoers
     # Output: -r--r----- 1 root root 755
     ```

---

### **Syntax of a Sudoers Entry**
```
user ALL=(ALL:ALL) ALL
```

- **`user`**: The username being granted privileges.
- **`ALL`**: 
  - First `ALL`: The hosts on which the rule applies.
  - Second `ALL`: The user who can be impersonated (default is all users).
  - Third `ALL`: The groups whose permissions are affected.
- **Final `ALL`**: The commands the user can execute as root.

---

### **Common Configuration Examples**

#### **1. Grant Full Root Privileges**
To give a user full `sudo` rights:
```bash
john ALL=(ALL:ALL) ALL
```
- User `john` can run all commands as any user or group on all hosts.

---

#### **2. Grant Root Access Without Password**
To allow a user to execute commands without entering a password:
```bash
john ALL=(ALL:ALL) NOPASSWD: ALL
```
- Add this for specific commands (e.g., `systemctl`):
  ```bash
  john ALL=(ALL) NOPASSWD: /bin/systemctl
  ```

---

#### **3. Restrict User to Specific Commands**
Allow a user to execute only specific commands:
```bash
john ALL=(ALL) /bin/systemctl restart nginx, /usr/bin/tail /var/log/nginx/access.log
```
- User `john` can only restart Nginx or view the access log.

---

#### **4. Grant Sudo Access to a Group**
To allow all members of a group to use `sudo`:
```bash
%developers ALL=(ALL:ALL) ALL
```
- The `%` prefix specifies a group.
- All users in the `developers` group can run any command as root.

---

#### **5. Restrict Sudo Access to Specific Users**
Deny `sudo` access for specific users:
```bash
Defaults:jane !authenticate
```
- User `jane` will be denied `sudo` access entirely.

---

#### **6. Limit User to Run Commands as Specific User**
Allow a user to execute commands only as a specific user (not root):
```bash
john ALL=(alice) /bin/cp
```
- User `john` can run the `cp` command as user `alice`.

---

### **Additional Options in `sudoers`**

#### **Defaults**
Set global or user-specific policies.

1. **Disable Password Requirement Globally**:
   ```bash
   Defaults exempt_group=sudoers
   ```

2. **Set Timeout for Sudo Sessions**:
   ```bash
   Defaults timestamp_timeout=5
   ```
   - Sudo permissions will expire after 5 minutes of inactivity.

3. **Record Commands in a Log**:
   ```bash
   Defaults log_input, log_output
   ```

---

### **Include External Configuration**
For better organization, include external configuration files:
- In the `sudoers` file:
  ```bash
  # Includedir directive
  # Add custom rules to /etc/sudoers.d/
  ```
- Create a new rule in `/etc/sudoers.d/john`:
  ```bash
  john ALL=(ALL:ALL) NOPASSWD: ALL
  ```

---

### **Testing Sudoers Configuration**
1. Check syntax with `visudo`:
   ```bash
   sudo visudo
   ```
   Any syntax error will prevent saving.

2. Test with a user:
   ```bash
   sudo -l
   ```
   Lists the commands the user can execute.

---

### **Practical Example**

#### Scenario:
- User `john`:
  - Can restart Nginx without a password.
  - Can view logs but not modify them.
- Developers group:
  - Full `sudo` access.

#### Configuration:
```bash
john ALL=(ALL) NOPASSWD: /bin/systemctl restart nginx, /usr/bin/tail /var/log/nginx/access.log
%developers ALL=(ALL:ALL) ALL
```

---

[Main menu](../../README.md)