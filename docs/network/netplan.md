[Main menu](../../README.md)

### **Configuring Netplan in Ubuntu**

Netplan is the default network configuration tool used in Ubuntu (from version 17.10). It uses YAML configuration files to define network settings and applies them via backends like **NetworkManager** or **systemd-networkd**.

---

### **Key Features**
1. YAML-based configuration files.
2. Works with **NetworkManager** (desktop) or **systemd-networkd** (server).
3. Supports static IPs, DHCP, VLANs, bridges, bonds, and more.

---

### **Configuration Files**
Netplan configurations are stored in `/etc/netplan/`. Common file names include:
- `/etc/netplan/01-netcfg.yaml`
- `/etc/netplan/50-cloud-init.yaml`

---

### **Netplan Commands**
1. **`netplan apply`**:
   - Applies the current configuration immediately.
   - Example:
     ```bash
     sudo netplan apply
     ```

2. **`netplan generate`**:
   - Generates backend-specific configuration files for `NetworkManager` or `systemd-networkd`.
   - Example:
     ```bash
     sudo netplan generate
     ```

3. **`netplan try`**:
   - Tests configuration changes temporarily. Reverts if unconfirmed within 120 seconds.
   - Example:
     ```bash
     sudo netplan try
     ```

4. **`netplan info`**:
   - Displays backend information (`NetworkManager` or `systemd-networkd`).
   - Example:
     ```bash
     netplan info
     ```

---

### **Basic Syntax for YAML Files**

Netplan YAML files follow this structure:
```yaml
network:
  version: 2
  renderer: <backend>  # networkd or NetworkManager
  ethernets:
    <interface_name>:
      dhcp4: <true|false>
      addresses:
        - <IP_address/subnet>
      gateway4: <gateway_IP>
      nameservers:
        addresses:
          - <DNS_IP>
          - <DNS_IP>
```

---

### **Examples**

#### **1. Basic DHCP Configuration**
If your network uses DHCP for IP assignment:
```yaml
network:
  version: 2
  renderer: networkd
  ethernets:
    ens33:
      dhcp4: true
```

- Apply the configuration:
  ```bash
  sudo netplan apply
  ```

---

#### **2. Static IP Configuration**
To set a static IP:
```yaml
network:
  version: 2
  renderer: networkd
  ethernets:
    ens33:
      dhcp4: false
      addresses:
        - 192.168.1.100/24
      gateway4: 192.168.1.1
      nameservers:
        addresses:
          - 8.8.8.8
          - 8.8.4.4
```

- Apply the configuration:
  ```bash
  sudo netplan apply
  ```

---

#### **3. Configure Multiple Interfaces**
Example for two interfaces, one using DHCP and another with a static IP:
```yaml
network:
  version: 2
  renderer: networkd
  ethernets:
    ens33:
      dhcp4: true
    ens34:
      dhcp4: false
      addresses:
        - 192.168.2.10/24
      gateway4: 192.168.2.1
      nameservers:
        addresses:
          - 8.8.8.8
```

---

#### **4. Bridge Interface**
Useful for virtualization or bonding interfaces:
```yaml
network:
  version: 2
  renderer: networkd
  bridges:
    br0:
      dhcp4: true
      interfaces:
        - ens33
```

---

#### **5. VLAN Configuration**
For VLAN tagging on an interface:
```yaml
network:
  version: 2
  renderer: networkd
  vlans:
    vlan10:
      id: 10
      link: ens33
      addresses:
        - 192.168.10.100/24
      nameservers:
        addresses:
          - 8.8.8.8
```

---

#### **6. Disable an Interface**
To disable an interface:
```yaml
network:
  version: 2
  renderer: networkd
  ethernets:
    ens33:
      dhcp4: false
      optional: true
```

---

### **Testing and Debugging**

1. **Testing Configuration**:
   Use `netplan try` to test changes temporarily:
   ```bash
   sudo netplan try
   ```
   If the configuration works, confirm it. Otherwise, wait, and it will revert.

2. **Check Logs**:
   If issues arise, check system logs:
   ```bash
   journalctl -u systemd-networkd
   ```

3. **Debugging**:
   Use `netplan generate` to view the backend-specific configuration files:
   ```bash
   sudo netplan generate
   cat /run/systemd/network/*.network
   ```

---

### **Troubleshooting**

1. **Configuration Errors**:
   If `sudo netplan apply` fails, check the syntax in the YAML file:
   ```bash
   sudo netplan --debug apply
   ```

2. **Interface Names**:
   Use `ip link` or `ifconfig` to list available network interfaces.

3. **DNS Issues**:
   Ensure correct DNS servers are specified under `nameservers`.

---

### **Useful Commands for Network Troubleshooting**

- **Check Network Status**:
  ```bash
  ip a
  ```

- **Ping a Host**:
  ```bash
  ping 8.8.8.8
  ```

- **Display Routing Table**:
  ```bash
  ip route
  ```

- **Check System Logs**:
  ```bash
  journalctl -xe
  ```

[Main menu](../../README.md)