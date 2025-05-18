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
