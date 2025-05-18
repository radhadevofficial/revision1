---
## 🔹 **Area 6: Security & Firewall (Linux + Windows)**

---

### ✅ **1. Firewall Basics (Concept)**

A **firewall** controls incoming and outgoing network traffic based on predefined rules. It's like a gatekeeper for your server.

Types:

* **Host-based** (local to OS): `iptables`, `ufw`, Windows Defender Firewall
* **Network-based**: Fortinet, Sophos, Cisco ASA (covered in job JD)

---

### ✅ **2. Linux Firewall: UFW & iptables**

#### 🔹 UFW (Uncomplicated Firewall – for Ubuntu)

```bash
ufw status
ufw allow 22/tcp       # Allow SSH
ufw deny 23/tcp        # Block Telnet
ufw enable
ufw disable
```

#### 🔹 iptables (More powerful, but complex)

```bash
iptables -L                       # List all rules
iptables -A INPUT -p tcp --dport 80 -j ACCEPT
iptables -A INPUT -p tcp --dport 23 -j DROP
iptables-save > /etc/iptables.rules
```

🧠 Remember:

* Ports: 22 (SSH), 80 (HTTP), 443 (HTTPS), 3306 (MySQL), 21 (FTP)

---

### ✅ **3. Windows Firewall Essentials**

#### GUI:

* Go to `Control Panel > Windows Defender Firewall > Advanced Settings`

#### CLI (PowerShell / CMD):

```powershell
netsh advfirewall firewall show rule name=all
netsh advfirewall firewall add rule name="Allow SSH" dir=in action=allow protocol=TCP localport=22
```

🧠 Block outbound traffic for suspicious apps or open ports only as needed.

---

### ✅ **4. SSH Hardening (Linux)**

1. Edit `/etc/ssh/sshd_config`

   ```bash
   Port 2222                   # Change default SSH port
   PermitRootLogin no          # Block root login
   PasswordAuthentication no   # Use key-based login
   AllowUsers devuser sysadmin
   ```

2. Restart SSH:

   ```bash
   systemctl restart sshd
   ```

3. Use **fail2ban** to block brute force:

   ```bash
   apt install fail2ban
   ```

---

### ✅ **5. Antivirus Tools**

* **Linux**: ClamAV

  ```bash
  clamscan -r /home
  ```
* **Windows**: Windows Defender or third-party (Bitdefender, Kaspersky)

---

### ✅ **6. System Hardening Tips**

| Platform | Tips                                                              |
| -------- | ----------------------------------------------------------------- |
| Linux    | Disable unused services, patch regularly, file permission hygiene |
| Windows  | Enable firewall, disable guest account, auto-updates, BitLocker   |
| Both     | Strong passwords, disable USB ports, keep logs monitored          |

---

### ✅ **7. Security Best Practices**

* Use **sudo**, never work as root/admin directly
* Enable **multi-factor authentication (MFA)** wherever possible
* Set up **logging and alerts** for login attempts and failures
* Keep OS and packages **updated**
* Audit users & remove unused accounts

---

### ✅ **8. Bonus: Check for Open Ports**

* **Linux**:

  ```bash
  ss -tuln       # Shows listening ports
  netstat -tuln  # Older alternative
  ```
* **Windows**:

  ```cmd
  netstat -an | find "LISTEN"
  ```

---

### 💡 Good to Know

* **NAT and Port Forwarding**: Used in firewalls to route external traffic to internal machines.
* **IDS/IPS**: Tools like Snort can detect/prevent attacks.
* **Security Logs**:

  * Linux: `/var/log/auth.log`, `/var/log/syslog`
  * Windows: Event Viewer → Security

---
---

## 🔹 **Area 7: Troubleshooting & Preventive Maintenance**

---

### ✅ **1. What is Preventive Maintenance (PM)?**

Preventive Maintenance is **routine checking and servicing** of systems to avoid unexpected failures.

Tasks include:

* Checking disk space and health
* Monitoring resource usage (CPU, RAM, I/O)
* Applying OS updates and patches
* Checking logs and clearing old ones
* Testing backups and restore jobs
* Verifying RAID/Storage health
* Monitoring temperature and hardware conditions

🧠 Most companies expect **weekly/monthly checklists**.

---

### ✅ **2. Basic Troubleshooting Workflow (Any OS)**

| Step | Action                                          |
| ---- | ----------------------------------------------- |
| 1️⃣  | Identify the problem (ask user, logs, symptoms) |
| 2️⃣  | Reproduce the issue, isolate hardware/software  |
| 3️⃣  | Check logs (auth, syslog, dmesg, Event Viewer)  |
| 4️⃣  | Restart relevant service or process             |
| 5️⃣  | Apply known fix or escalate if needed           |
| 6️⃣  | Document the solution for future                |

---

### ✅ **3. Linux Common Issues & Solutions**

| Issue                      | Command/Action                                     |
| -------------------------- | -------------------------------------------------- |
| High CPU/Memory            | `top`, `htop`, `ps aux --sort=-%mem`               |
| Disk full                  | `df -h`, `du -sh *`, `journalctl --vacuum-time=1d` |
| Network unreachable        | `ping`, `ip a`, `nmcli`, `netplan apply`           |
| Service failed             | `systemctl status nginx`, `journalctl -xe`         |
| Boot failure (fstab, init) | Boot into recovery, fix `/etc/fstab`, use `fsck`   |
| User can't login           | Check `/etc/passwd`, lock status, permissions      |

---

### ✅ **4. Windows Common Issues & Solutions**

| Issue                | Tool or Fix                                   |
| -------------------- | --------------------------------------------- |
| Slow performance     | Task Manager, disable startup apps            |
| Cannot login         | Reset password in AD or local user            |
| Service not starting | Check Event Viewer → Services                 |
| Disk issue           | `chkdsk`, Disk Management                     |
| Driver issue         | Device Manager                                |
| Network not working  | `ipconfig /release` & `/renew`, check adapter |

---

### ✅ **5. Tools for Monitoring & Alerts**

#### Linux:

* `top`, `vmstat`, `iotop`, `dmesg`, `journalctl`
* Tools: **Zabbix**, **Nagios**, **Glances**

#### Windows:

* Event Viewer (logs)
* Performance Monitor (`perfmon`)
* Task Scheduler
* Disk Cleanup, Disk Management

---

### ✅ **6. Routine Tasks You Should Know**

* Check system uptime:

  * `uptime` (Linux), `systeminfo | find "System Boot"` (Windows)
* Reboot logs:

  * `last reboot` (Linux)
* Schedule jobs:

  * `crontab -e` (Linux), Task Scheduler (Windows)
* View last login:

  * `last` or `who` (Linux), Event Viewer (Windows)

---

### ✅ **7. Proactive Monitoring Checklist**

* ✅ Disk space > 20% free
* ✅ Backup jobs completed
* ✅ RAID status = healthy
* ✅ No failed services
* ✅ No critical logs in last 24h
* ✅ CPU load within normal
* ✅ External access (web server, SSH) confirmed

---
