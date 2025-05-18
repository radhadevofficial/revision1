---

### 🔹 PRIORITY AREAS TO MASTER (Be *strong* in these)

These are directly relevant and **high-impact** areas where your knowledge must be confident and demonstrable:

#### 1. **Linux and Windows Server Administration**

* Installation, configuration, and troubleshooting of servers.
* Service management (e.g., Apache, Samba, systemd).
* Log management (`/var/log`, `eventvwr`).
* SSH, remote desktop, user and permission management.

#### 2. **RAID and Storage**

* RAID levels (RAID 0, 1, 5, 10): understand the purpose, pros/cons, and how to configure.
* Basic LVM (which you’ve mentioned in resume) – ensure you can explain and show CLI examples.
* Storage troubleshooting (disk failures, mount issues, etc.)

#### 3. **Virtualization**

* **VMware**: Basic understanding of ESXi, vCenter, VM creation, snapshots.
* **Proxmox**: Since you used it in freelance, know how to relate it to VMware concepts.

#### 4. **Active Directory, DNS, DHCP, GPO**

* Structure and purpose of AD.
* DNS/DHCP roles in AD setup.
* Creating and linking GPOs.
* Troubleshooting domain join issues.

#### 5. **Backup and Restore**

* Basics of **Veritas or Veeam** (even theory if no direct experience).
* Describe how you’d set up regular backups and restore data.

#### 6. **Troubleshooting and Preventive Maintenance**

* How you check system health (disk usage, RAM, CPU).
* How you would handle a sudden outage or performance degradation.
* Use of monitoring tools or basic scripting for health checks.

---

### 🔹 SECONDARY AREAS (Know **basics**, able to discuss)

You should be able to talk about these but deep expertise is not expected for 6-months experience:

#### 1. **NAS & Enterprise Storage**

* QNAP/Synology basics – how they’re used, protocols (SMB, NFS).
* What is SAN vs NAS – use case and architecture.

#### 2. **Cloud Integration (AWS)**

* You’ve done cloud projects – be ready to briefly explain EC2, S3, and how you deployed web apps or managed infra.

#### 3. **Security**

* Describe basic hardening steps: disabling unused ports, configuring firewall (`ufw`, `iptables`, Windows firewall).
* VPNs and access control – even at a basic level.

#### 4. **Automation & Scripting**

* Bash: cron jobs, file backup scripts.
* PowerShell: simple scripts to manage users, services.
* Explain a script you’ve written for automating a real task.

---

### 🔹 EXTRAS THAT ADD VALUE

These can be discussed to stand out:

* CI/CD and GitHub Actions (as mentioned in your resume).
* Your RHCE certification – highlight the training, not just the cert.
* Any real support incidents you handled (even in freelance) – what the issue was, how you solved it.

---

### ⚠️ Topics You Can Be Light On

It’s okay to have limited hands-on but basic understanding is good:

* VMware vCenter advanced features.
* Veritas/Veeam actual console usage (mention theory and workflow).
* SAN zoning or enterprise EMC/NetApp if not experienced.

---

### ✅ Summary Table

| Area                     | Importance | Depth Needed     | Your Resume Match |
| ------------------------ | ---------- | ---------------- | ----------------- |
| Linux Server Admin       | ★★★★★      | Strong hands-on  | ✅ Strong          |
| Windows Server + AD/DNS  | ★★★★★      | Strong hands-on  | ✅ Moderate        |
| RAID & Storage           | ★★★★☆      | Medium to Strong | ✅ Basic to mid    |
| VMware/Proxmox           | ★★★★☆      | Medium           | ✅ Basic           |
| NAS & Backup             | ★★★☆☆      | Basic to Medium  | 🟡 Mention only   |
| Cloud (AWS)              | ★★★☆☆      | Basic to Medium  | ✅ Basic           |
| GPO/Policy Management    | ★★★☆☆      | Basic to Medium  | 🟡 Limited        |
| Security & Firewall      | ★★★☆☆      | Basic            | ✅ Basic           |
| Automation (Bash/Python) | ★★★☆☆      | Basic to Medium  | ✅ Good            |

---

### Final Tip

In the **interview**, showcase:

* **Real tasks/projects** you’ve done (even as a freelancer).
* **Confident troubleshooting mindset**.
* Eagerness to learn and grow into the role.
---
# Areas Begin
---

# ✅ **Area 1: Linux & Windows Server Administration**

---

## 🔹 **Key Topics to Cover**

| Topic                        | Description                                                                            |
| ---------------------------- | -------------------------------------------------------------------------------------- |
| OS Installation & Config     | Installing Linux (Ubuntu, RHEL) and Windows Server with partitions, hostname, IP, etc. |
| User & Permission Management | Add/delete users, groups, set file/folder permissions                                  |
| Service Management           | Start, stop, restart services, check status                                            |
| Firewall & Security Settings | Configure `ufw`, `iptables`, Windows Firewall, restrict SSH                            |
| System Monitoring & Logs     | Tools: `top`, `htop`, `vmstat`, Event Viewer                                           |
| SSH & Remote Management      | Configure and secure SSH in Linux, RDP in Windows                                      |
| Troubleshooting Boot/Disks   | Use `fsck`, recovery mode, disk management tools                                       |

---

## 🔸 **Linux Server Admin – Interview Questions & Answers**

### 🔹 Beginner to Intermediate

---

**Q: How do you check system resource usage (CPU, memory, disk)?**

**A:**

```bash
top          # Live CPU & memory usage
htop         # Enhanced version of top
free -h      # Memory usage in human-readable format
df -h        # Disk space usage
lsblk        # Show block devices and mount points
```

---

**Q: What are the runlevels in Linux? Difference between runlevel 3 and 5?**

**A:**
Runlevels define what system services are running.

* **Runlevel 3**: Multi-user, command line only
* **Runlevel 5**: Multi-user with GUI

On `systemd` distros:

```bash
systemctl get-default         # Shows default target
```

* Runlevel 3 → `multi-user.target`
* Runlevel 5 → `graphical.target`

---

**Q: How do you check which services are running and control them?**

**A:**

```bash
systemctl status sshd          # Check status
systemctl start sshd           # Start service
systemctl stop sshd            # Stop service
systemctl restart sshd         # Restart service
systemctl enable sshd          # Enable at boot
```

---

**Q: What’s the difference between hard and soft links?**

**A:**

* **Hard Link**: Actual duplicate pointing to same inode. Even if original is deleted, the link works.
* **Soft Link (symlink)**: Just a shortcut. Breaks if original file is deleted.

```bash
ln file1 file1_hard
ln -s file1 file1_soft
```

---

**Q: Explain chmod 755.**

**A:**

* `7` = read(4) + write(2) + execute(1) → Owner
* `5` = read(4) + execute(1) → Group
* `5` = read(4) + execute(1) → Others

```bash
chmod 755 filename
```

Owner: full access, others: read + execute

---

**Q: What is LVM? How to create a logical volume?**

**A:**
LVM = Logical Volume Manager, allows flexible disk management.

Steps:

```bash
pvcreate /dev/sdb
vgcreate my_vg /dev/sdb
lvcreate -L 5G -n my_lv my_vg
mkfs.ext4 /dev/my_vg/my_lv
mount /dev/my_vg/my_lv /mnt
```

---

**Q: What is crontab? How do you schedule a backup?**

**A:**
Crontab runs scheduled jobs.

```bash
crontab -e
```

Example:

```bash
0 2 * * * tar -czf /backup/backup.tar.gz /etc
```

(Backs up `/etc` every day at 2 AM)

---

**Q: How do you check logs for troubleshooting in Linux?**

**A:**

```bash
journalctl -xe               # systemd logs
tail -f /var/log/syslog      # general log
cat /var/log/auth.log        # auth/SSH login attempts
```

---

**Q: How do you configure a static IP on Linux?**

For Netplan (Ubuntu):

```bash
sudo nano /etc/netplan/01-netcfg.yaml
```

```yaml
network:
  version: 2
  ethernets:
    eth0:
      dhcp4: no
      addresses: [192.168.1.100/24]
      gateway4: 192.168.1.1
      nameservers:
        addresses: [8.8.8.8, 1.1.1.1]
```

```bash
sudo netplan apply
```

---

**Q: What is SELinux/AppArmor?**

**A:**
Security modules for Linux:

* **SELinux**: Mandatory Access Control, very strict

  * Modes: Enforcing, Permissive, Disabled
  * `sestatus`, `setenforce 0`
* **AppArmor**: Profile-based protection, easier than SELinux

---

**Q: How to configure firewall in Linux (iptables/ufw)?**

**UFW (simpler):**

```bash
ufw allow 22/tcp
ufw enable
ufw status
```

**iptables (manual):**

```bash
iptables -A INPUT -p tcp --dport 22 -j ACCEPT
iptables -L
```

---

### 🔹 Slightly Advanced

---

**Q: How to troubleshoot if a Linux server doesn't boot?**

**A:**

* Use **recovery mode**
* Check **/etc/fstab** errors
* Run `fsck /dev/sdX` for file system repair
* Check logs via `journalctl -xb`
* Undo last software/config change

---

**Q: How do you secure SSH access?**

**A:**

```bash
# In /etc/ssh/sshd_config:
Port 2222
PermitRootLogin no
PasswordAuthentication no
AllowUsers adminuser

# Reload:
systemctl restart sshd
```

Also install `fail2ban` to prevent brute force.

---

**Q: top vs htop vs iotop**

| Tool    | Purpose              |
| ------- | -------------------- |
| `top`   | Basic process info   |
| `htop`  | Visual + interactive |
| `iotop` | Shows disk I/O usage |

---

**Q: How to mount NFS or remote share?**

```bash
sudo apt install nfs-common
sudo mount 192.168.1.100:/shared /mnt
```

To persist:

```
192.168.1.100:/shared /mnt nfs defaults 0 0
```

---

## 🔸 **Windows Server Admin – Interview Questions & Answers**

### 🔹 Beginner to Intermediate

---

**Q: How do you install Windows Server and set static IP?**

* Boot from ISO → Install
* Use `Server Manager` to add roles
* Static IP:

  * Go to **Network Connections**
  * Right-click Adapter → IPv4 → Set IP, Subnet, Gateway

---

**Q: What is Active Directory? Main components?**

**A:**
AD is a directory service that manages users, groups, and policies in a domain.

* **Domain**
* **OU (Organizational Unit)**
* **Group**
* **User**
* **Group Policy**
* **Domain Controller**

---

**Q: What are GPOs? Example?**

Group Policy Objects let you enforce settings.
Example:

* Auto-lock screen after 5 mins:
  `User Config > Policies > Admin Templates > Control Panel > Display`

---

**Q: Difference: Domain vs Workgroup vs Forest**

| Feature         | Domain     | Workgroup | Forest             |
| --------------- | ---------- | --------- | ------------------ |
| Central Control | Yes        | No        | Yes (multi-domain) |
| Scalability     | Enterprise | Small LAN | Cross-domain       |

---

**Q: How to create/manage AD users?**

Use `dsa.msc` or PowerShell:

```powershell
New-ADUser -Name "John Doe" -AccountPassword (ConvertTo-SecureString "P@ssw0rd" -AsPlainText -Force)
```

---

**Q: How to check Event Logs?**

Open **Event Viewer**, check:

* System
* Application
* Security

For login issues, check **Security** logs.

---

**Q: How to restart a Windows service (GUI & CLI)?**

**GUI**:

* `services.msc` → right-click → restart

**CLI**:

```powershell
Get-Service wuauserv | Restart-Service
```

---

**Q: Local vs Domain user**

* **Local user**: Exists only on one PC
* **Domain user**: Exists in Active Directory and can log into any domain-joined system

---

**Q: Create network share and assign permissions**

1. Right-click folder → Properties → Sharing tab
2. Share → Permissions → Add users/groups
3. Advanced → NTFS security permissions

---

**Q: Tools to monitor performance**

* **Task Manager**
* **Resource Monitor**
* **Performance Monitor (`perfmon`)**
* **Event Viewer**

---

### 🔹 Slightly Advanced

---

**Q: NTFS vs ReFS**

| Feature      | NTFS                        | ReFS                             |
| ------------ | --------------------------- | -------------------------------- |
| Feature-rich | ✅ (permissions, encryption) | ❌ (no quotas, no compression)    |
| Resilience   | Less than ReFS              | Auto healing, better for storage |

---

**Q: Join PC to domain**

1. Right-click **This PC → Properties → Change settings**
2. Click **Change** → enter domain name
3. Provide credentials → restart

---

**Q: Use of `gpupdate /force` and `rsop.msc`**

* `gpupdate /force`: Reapplies all group policies
* `rsop.msc`: Shows Resultant Set of Policy (what GPOs are active on system)

---

**Q: Troubleshoot login failure (domain)**

* Check network/DNS connectivity to DC
* Ensure account is not locked/expired
* Check **event logs**
* Use `nltest /dsgetdc:domainname` to check DC availability

---
---

## 🔹 Area 2: RAID & Storage (Interview Focus)

RAID is used to improve **performance**, **redundancy**, or **both** in server storage systems. You’ll often deal with it while configuring **HP, Dell, IBM servers** or during **disk failure recovery**.

---

### ✅ Topics to Be Strong In

| Concept               | What You Should Know                                                        |
| --------------------- | --------------------------------------------------------------------------- |
| RAID Levels           | Purpose, benefits, and trade-offs of each level                             |
| RAID Types            | Software RAID (mdadm), Hardware RAID (BIOS/Controller)                      |
| Storage Terms         | JBOD, Hot Spare, Striping, Mirroring, Parity                                |
| Disk Tools            | `lsblk`, `fdisk`, `parted`, `df`, `du`, `smartctl`                          |
| Basic Troubleshooting | Disk failure symptoms, SMART errors, `dmesg`, logs                          |
| Storage Configuration | RAID setup steps (theory), common vendor tools (HP Array Config, Dell OMSA) |

---

## 🔸 RAID Levels (Must Know)

| RAID | Type                  | Disks (Min) | Fault Tolerance          | Use Case                               |
| ---- | --------------------- | ----------- | ------------------------ | -------------------------------------- |
| 0    | Striping              | 2           | ❌ None                   | Speed, not reliable                    |
| 1    | Mirroring             | 2           | ✅ 1 disk                 | High availability, slower write        |
| 5    | Striping + Parity     | 3           | ✅ 1 disk                 | Balanced performance + redundancy      |
| 10   | Mirror + Stripe       | 4           | ✅ 2 disks (1 per mirror) | High performance + fault tolerant      |
| JBOD | Just a Bunch of Disks | 1+          | ❌ None                   | Simple, not recommended for production |

---

### 🔸 Sample Interview Questions with Suggested Answers

---

### **Q1. What is RAID and why is it used?**

**A**:
RAID (Redundant Array of Independent Disks) is a technology to combine multiple disks into one logical unit to improve performance, increase storage capacity, or provide redundancy in case of disk failure.

---

### **Q2. What is the difference between Hardware and Software RAID?**

**A**:

* **Hardware RAID**: Managed by RAID controller card or motherboard BIOS.
* **Software RAID**: Managed by the operating system using tools like `mdadm` in Linux.
* Hardware RAID has better performance and is OS-independent.

---

### **Q3. Explain RAID 0, 1, 5, and 10.**

You should summarize like this:

* **RAID 0**: No redundancy, just performance. If one disk fails, data is lost.
* **RAID 1**: Mirror. Same data written to 2 disks. High reliability.
* **RAID 5**: Striping + Parity. Need at least 3 disks. Can tolerate 1 disk failure.
* **RAID 10**: Combination of RAID 1 and 0. Needs 4 disks. High performance + redundancy.

🧠 Tip: Draw a quick diagram if allowed in whiteboard rounds!

---

### **Q4. Have you configured RAID manually? How?**

If not done practically:

> I’ve studied and observed RAID setup during my RHCE/college project. For example, using `mdadm` in Linux:

```bash
mdadm --create /dev/md0 --level=5 --raid-devices=3 /dev/sdb /dev/sdc /dev/sdd
```

Then format and mount:

```bash
mkfs.ext4 /dev/md0
mount /dev/md0 /mnt/raid
```

---

### **Q5. What happens when one disk in RAID 5 fails?**

**A**:

* RAID 5 can continue to function with **1 disk failure** using parity data.
* However, performance decreases.
* If a second disk fails before rebuild, data is lost.

---

### **Q6. How do you monitor disk health in Linux?**

**A**:

* `smartctl -a /dev/sdX` – SMART disk health
* `dmesg` – check kernel disk errors
* `cat /proc/mdstat` – if using software RAID
* `lsblk`, `df -h` – for mounted partitions
* Third-party tools: Zabbix, Nagios

---

### 🔧 Bonus: Commands to Remember

```bash
# View all disks and partitions
lsblk

# Disk space usage
df -h
du -sh /folder

# Create partition
fdisk /dev/sdb

# Check RAID status (software)
cat /proc/mdstat

# View SMART status
smartctl -a /dev/sda
```

---
---

## 🔹 Area 3: AD, DNS, DHCP & GPO

These services are part of **Windows Server infrastructure**, and interviewers expect you to understand how they work together to manage users, computers, policies, and network settings in a domain environment.

---

### ✅ Topics You Need to Know

| Component                 | Key Focus                                  |
| ------------------------- | ------------------------------------------ |
| **Active Directory (AD)** | User/computer management, domain structure |
| **DNS**                   | Resolving names inside the domain          |
| **DHCP**                  | Assigning IPs to devices                   |
| **GPO (Group Policy)**    | Automating settings and enforcing security |

---

### 🔸 Sample Interview Questions & Good Answers

---

### **Q1. What is Active Directory and what is it used for?**

**A**:
Active Directory (AD) is a directory service developed by Microsoft. It stores information about users, computers, and other resources in a domain and helps administrators manage access and security centrally.

* AD is used for **authentication (login)** and **authorization (permissions)**.
* AD stores data in a structured hierarchy (domain → OU → objects).

---

### **Q2. What are the main components of Active Directory?**

**A**:

* **Domain**: Logical group of objects (users, computers).
* **OU (Organizational Unit)**: Subdivision of a domain used to organize objects.
* **Domain Controller (DC)**: Server that hosts AD services.
* **Forest & Tree**: Top-level logical structure that can contain multiple domains.

---

### **Q3. What is DNS and why is it important for Active Directory?**

**A**:

* DNS (Domain Name System) translates domain names (e.g., `server01.domain.com`) to IP addresses.
* **AD requires DNS** to locate domain controllers and for login, replication, and services to work.

🧠 AD creates special DNS records (SRV) during domain setup.

---

### **Q4. What is DHCP and how does it work?**

**A**:
DHCP (Dynamic Host Configuration Protocol) automatically assigns IP addresses and other network settings to devices.

* The server maintains a **DHCP scope** (IP pool).
* Clients send a **DHCP Discover**, server replies with **Offer → Request → Acknowledge** (DORA process).

---

### **Q5. What is Group Policy and how is it used?**

**A**:
Group Policy is a feature that allows administrators to define settings and rules for users or computers.

* GPOs (Group Policy Objects) are applied to **OUs** to enforce:

  * Security settings (password policy, screen lock)
  * Software deployment
  * Network configurations (drive mapping, firewall)

🧠 Tools:

* `gpedit.msc` – Local Group Policy Editor
* `gpmc.msc` – Group Policy Management Console

---

### **Q6. How do you create and apply a GPO?**

1. Open **Group Policy Management Console** (`gpmc.msc`)
2. Right-click OU → “Create a GPO”
3. Edit the GPO to configure settings
4. It automatically applies to all objects in the OU

---

### **Q7. How do you troubleshoot GPO issues?**

**A**:

* Run `gpresult /h gp.html` or `gpresult /R` to check applied policies
* Use `rsop.msc` to simulate Resultant Set of Policy
* Use Event Viewer under **System or GroupPolicy** logs

---

### **Q8. What is the difference between OU and Group?**

* **OU** is used to organize objects (like a folder) – GPOs apply here.
* **Group** is used to grant permissions to users (e.g., read-only access to a folder).

---

### **Q9. What are the types of groups in Active Directory?**

**A**:

* **Security Group**: Used to assign permissions
* **Distribution Group**: Used for email (not for security)
* Scope:

  * **Global**: Members from same domain
  * **Domain Local**: Permissions in local domain
  * **Universal**: Members and permissions across domains

---

### 🔧 Must-Know Commands & Tools

| Tool / Command           | Purpose                            |
| ------------------------ | ---------------------------------- |
| `dsa.msc`                | Active Directory Users & Computers |
| `gpmc.msc`               | Group Policy Management            |
| `gpresult /R`            | View applied GPOs                  |
| `gpupdate /force`        | Force GPO refresh                  |
| `netsh dhcp show server` | Check DHCP server settings         |
| `nslookup`               | Test DNS resolution                |

---

### ✅ Summary of Concepts to Review

* How to join a computer to a domain
* How to reset a domain user’s password
* What happens when DNS or AD is misconfigured
* How GPOs flow (Local > Site > Domain > OU)
* How to delegate control in AD

---
---

## 🔹 Area 4: Virtualization & Cloud (VMware, Proxmox, AWS Basics)

You'll be expected to show knowledge in managing **virtual machines (VMs)** and basic understanding of **cloud platforms like AWS**.

---

### ✅ Topics to Be Strong In

| Sub-Area       | Key Concepts                                                  |
| -------------- | ------------------------------------------------------------- |
| **VMware**     | ESXi, vSphere, VM creation, snapshot, resource allocation     |
| **Proxmox VE** | Node, VM/CT setup, backup, console, ISO upload, storage types |
| **AWS Basics** | EC2, S3, IAM, Security Group, Launch instance, SSH keypair    |

---

### 🔸 Interview Questions & Answers

---

### **Q1. What is virtualization and why is it used?**

**A**:
Virtualization allows multiple virtual machines to run on a single physical server using a hypervisor. It improves **hardware utilization**, **isolation**, and **scalability**.

🧠 Hypervisors:

* Type 1: Bare-metal (e.g., VMware ESXi, Proxmox)
* Type 2: Hosted (e.g., VirtualBox, VMware Workstation)

---

### **Q2. What is VMware ESXi and how do you manage it?**

**A**:

* VMware ESXi is a Type-1 hypervisor installed directly on physical servers.
* Managed via:

  * **vSphere Client/Web** (GUI)
  * **vCenter** (for multiple ESXi hosts)
  * CLI tools (`esxcli`)

Common Tasks:

* Create VM
* Allocate CPU/RAM
* Configure storage/network
* Take snapshots before major changes

---

### **Q3. What are snapshots in VMware and when should you use them?**

**A**:
Snapshots are point-in-time states of a VM, used for **backup before changes** (like OS patching). They are not replacements for full backups and can affect performance if left for long.

---

### **Q4. What is Proxmox VE and how is it different from VMware?**

**A**:

* Open-source virtualization platform using **KVM (VMs)** and **LXC (containers)**.
* Web interface + CLI.
* Allows backup, snapshot, ISO upload, clustering (multiple nodes), storage types (local, NFS, Ceph).

---

### **Q5. How do you create a VM in Proxmox?**

1. Upload ISO (Debian, Ubuntu, etc.)
2. Click **Create VM**, choose name, OS, ISO
3. Set disk size, CPU, RAM
4. Configure network bridge (vmbr0)
5. Start and open console

---

### **Q6. What is EC2 in AWS and how do you launch an instance?**

**A**:

* **EC2** is a virtual server in AWS cloud.
* Steps:

  1. Select AMI (Ubuntu, Amazon Linux, etc.)
  2. Choose instance type (t2.micro etc.)
  3. Configure network and storage
  4. Add SSH keypair (PEM file)
  5. Launch and connect using:

     ```bash
     ssh -i key.pem ec2-user@<public-ip>
     ```

---

### **Q7. What is an AWS Security Group?**

**A**:
A security group is like a virtual firewall that controls inbound and outbound traffic to EC2 instances.

Example rules:

* Allow TCP 22 from your IP (for SSH)
* Allow TCP 80/443 for HTTP/HTTPS

---

### **Q8. What is S3 and how do you use it?**

**A**:

* S3 (Simple Storage Service) is object storage used for backups, file hosting, logs, static websites.
* You can create buckets, set public/private permissions, and upload/download files via web or AWS CLI.

---

### 🔧 Useful Commands & Tools

| Tool/Command        | Description            |
| ------------------- | ---------------------- |
| `qm list` (Proxmox) | List VMs               |
| `pvecm status`      | Proxmox cluster status |
| `esxcli`            | VMware CLI             |
| `aws configure`     | Setup AWS CLI          |
| `aws s3 ls`         | List S3 buckets        |
| `ssh -i key.pem`    | Connect to EC2         |

---

### ✅ Summary of What to Review

* VMware snapshot, VM create, console access
* Proxmox dashboard: creating VM, container, backups
* AWS: Launch EC2, security group, connect using key
* Basic billing awareness: free tier, instance limits

---
---

## 🔹 **Area 5: Backup, Recovery & NAS Storage (For Server Admin Interview)**

---

### ✅ **1. Backup Concepts**

* **Backup** is a copy of data to restore after accidental deletion, corruption, or system failure.
* **Types of backups**:

  * **Full** – complete copy of all selected files.
  * **Incremental** – only changes since the last backup (faster, smaller).
  * **Differential** – changes since the last **full** backup (larger, but faster to restore).

🧠 **3-2-1 Rule**:

> Keep **3 copies** of your data, on **2 different media**, with **1 copy offsite**.

---

### ✅ **2. Backup Tools (Server Admin Should Know)**

#### 🔹 For Linux:

* `rsync`: Efficient backup/sync tool.

  ```bash
  rsync -avh /source /backup
  ```
* `tar`: Archive and compress backup.

  ```bash
  tar -czvf etc_backup.tar.gz /etc
  ```

#### 🔹 For Windows:

* **Windows Server Backup** (GUI tool).
* **`wbadmin`**: Command-line tool.

  ```cmd
  wbadmin start backup -backupTarget:D: -include:C: -allCritical -quiet
  ```

#### 🔹 Enterprise Tools (Theory is enough if you haven't used):

* **Veeam** – Great for virtual machine backups (VMware/Hyper-V).
* **Veritas NetBackup** – Powerful enterprise backup solution.

---

### ✅ **3. Restore Basics**

* Use `tar -xzvf backup.tar.gz` in Linux.
* Use `wbadmin start recovery` in Windows (or via GUI).
* Always **test backups** by performing restore operations.

---

### ✅ **4. Disaster Recovery (DR) Basics**

* A **DR plan** is your response after critical failure (hardware failure, ransomware, natural disaster).
* Key points:

  * Backup frequency
  * Offsite/cloud storage
  * Restore time objective (RTO) and restore point objective (RPO)
  * Regular testing of recovery steps

---

### ✅ **5. NAS (Network Attached Storage)**

* A NAS is a storage device (like Synology or QNAP) connected to the LAN.
* Used for shared folders, backups, and media/file storage.

🧠 Protocols:

* **SMB/CIFS** – Used by Windows for file shares.
* **NFS** – Used by Linux/Unix systems.
* **FTP** – For file transfer over the network.

---

### ✅ **6. NAS Admin Basics**

* Access web UI (e.g., `http://192.168.1.100`) to configure.
* Setup:

  * Volumes and shared folders
  * Users and permissions
  * Enable SMB/NFS/FTP as needed
  * Optional: configure RAID in the NAS

🛠 Good practice:

* Schedule NAS to **auto-backup to cloud** (like Google Drive or AWS S3).
* Use NAS **snapshots** + remote sync for critical folders.

---

### ✅ **7. Snapshot vs Backup**

| Feature  | Snapshot                      | Backup                        |
| -------- | ----------------------------- | ----------------------------- |
| Location | Same storage                  | External/cloud/secondary disk |
| Speed    | Instant                       | Slower (copy entire data)     |
| Use case | Rollback quickly (short-term) | Disaster recovery (long-term) |
| Risk     | If main storage fails, gone   | Survives if external          |

---
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
