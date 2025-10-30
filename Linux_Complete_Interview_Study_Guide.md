
# 🧠 LINUX COMPLETE STUDY GUIDE (Interview + Practical Reference)

This README is your **complete Linux interview and practical reference guide** — designed to ensure you can **answer 90%+ Linux questions** asked in DevOps, Cloud, or SysAdmin interviews.

---

## 🟩 1. Linux Basics

### 🔹 What is Linux?
Linux is an **open-source operating system kernel** used in servers, embedded systems, and DevOps environments.

### 🔹 Why Linux in DevOps?
- Most cloud servers run on Linux
- Command-line automation
- Open-source flexibility and control

---

## 🟨 2. Linux Architecture

| Layer | Description |
|--------|--------------|
| Hardware | Physical devices (CPU, RAM, Disk) |
| Kernel | Core of OS — interacts with hardware |
| Shell | Interface between user and kernel |
| Applications | Programs and utilities (e.g., vim, bash, top) |

---

## 🟦 3. File System Hierarchy

| Directory | Description |
|------------|-------------|
| `/` | Root directory |
| `/home` | User home directories |
| `/etc` | Configuration files |
| `/var` | Logs and variable data |
| `/bin` | Essential binaries |
| `/usr` | User programs |
| `/tmp` | Temporary files |
| `/opt` | Optional software |

---

## 🟪 4. Basic Commands

### Navigation
```bash
pwd                 # Print working directory
ls -l               # List files with details
cd /path/to/dir     # Change directory
```

### File Management
```bash
touch file.txt
mkdir new_folder
cp file1 file2
mv old.txt new.txt
rm file.txt
rmdir empty_dir
```

### Viewing Files
```bash
cat file.txt
less file.txt
head -n 5 file.txt
tail -n 10 file.txt
```

---

## 🟧 5. File Permissions

### Check Permissions
```bash
ls -l
```

**Example Output:**
```
-rwxr-xr-- 1 user group 1234 Oct 29 file.txt
```

| Symbol | Meaning |
|---------|----------|
| r | Read |
| w | Write |
| x | Execute |

### Change Permissions
```bash
chmod 755 file.sh
chmod u+x file.sh
```

### Change Ownership
```bash
chown user:group file.txt
```

---

## 🟥 6. Process Management

### View Running Processes
```bash
ps aux
top
htop
```

### Kill a Process
```bash
kill <pid>
kill -9 <pid>       # Force kill
```

### Background Jobs
```bash
sleep 100 &
jobs
fg %1
bg %1
```

---

## 🟩 7. System Monitoring

### Disk and Memory Usage
```bash
df -h       # Disk usage
du -sh *    # Directory usage
free -h     # Memory
uptime      # System load
```

### CPU and Network
```bash
top
vmstat 1
iostat
netstat -tulnp
ss -tuln
```

---

## 🟨 8. User Management

### Create and Manage Users
```bash
sudo adduser sohel
sudo passwd sohel
sudo usermod -aG sudo sohel
```

### Check Current User and Groups
```bash
whoami
id
groups
```

### Switch Users
```bash
su - username
sudo -i
```

---

## 🟦 9. Package Management

### Debian/Ubuntu (APT)
```bash
sudo apt update
sudo apt install nginx
sudo apt remove nginx
```

### RHEL/CentOS (YUM/DNF)
```bash
sudo yum install httpd
sudo dnf update
```

---

## 🟪 10. System Services (systemctl)

### Manage Services
```bash
sudo systemctl start nginx
sudo systemctl stop nginx
sudo systemctl restart nginx
sudo systemctl enable nginx
sudo systemctl status nginx
```

---

## 🟧 11. Networking Commands

```bash
ifconfig
ip addr show
ping google.com
traceroute google.com
nslookup example.com
curl -I example.com
wget https://example.com
```

---

## 🟥 12. Disk & File Operations

```bash
lsblk
df -h
mount /dev/sdb1 /mnt
umount /mnt
fdisk -l
```

### Find and Search
```bash
find /home -name "*.log"
grep "error" logfile.txt
grep -r "keyword" /var/log/
```

---

## 🟩 13. Shell Scripting Basics

### Example Script
```bash
#!/bin/bash
echo "Hello, $USER"
date
df -h
```

### Run Script
```bash
chmod +x script.sh
./script.sh
```

---

## 🟨 14. Scheduling Jobs (cron)

### Edit Crontab
```bash
crontab -e
```

### Example:
Run every day at midnight:
```
0 0 * * * /home/user/backup.sh
```

### List and Remove Jobs
```bash
crontab -l
crontab -r
```

---

## 🟦 15. Log Management

```bash
cd /var/log
cat syslog
tail -f /var/log/auth.log
journalctl -xe
```

---

## 🟪 16. SSH and Remote Access

### Connect to Remote Server
```bash
ssh user@ip
```

### Copy Files Securely
```bash
scp file.txt user@ip:/home/user/
```

### Generate SSH Key
```bash
ssh-keygen -t rsa
ssh-copy-id user@ip
```

---

## 🟧 17. Compression and Archiving

```bash
tar -cvf archive.tar folder/
tar -xvf archive.tar
gzip file.txt
gunzip file.txt.gz
zip -r archive.zip folder/
unzip archive.zip
```

---

## 🟥 18. Environment Variables

```bash
echo $PATH
export NAME=sohel
printenv
unset NAME
```

To make permanent → add to `~/.bashrc`.

---

## 🟩 19. System Information

```bash
uname -a
hostname
lsb_release -a
cat /etc/os-release
```

---

## 🟨 20. Interview Quick Recap

✅ **Core Topics**
- Linux architecture and directories  
- File permissions and ownership  
- System monitoring commands  
- Package management (apt, yum)  
- Service management (`systemctl`)  
- Network troubleshooting  
- Cron jobs and shell scripting  
- SSH and file transfer  
- Disk management and logging  

✅ **Common Interview Questions**
1. What are runlevels in Linux?
2. Difference between hard link and soft link?
3. How do you check CPU and memory usage?
4. How do you schedule a job in Linux?
5. Explain how permissions work in Linux.
6. What is the difference between `su` and `sudo`?
7. How to check which process is using a port?
8. How to kill a zombie process?
9. What is SELinux and how do you disable it?
10. How do you secure SSH access?

---

## 🧠 21. Quick Troubleshooting

| Problem | Command |
|----------|----------|
| Disk full | `df -h`, `du -sh *` |
| High CPU | `top`, `ps aux --sort=-%cpu` |
| Service down | `systemctl status <service>` |
| Port check | `ss -tuln` |
| DNS issue | `dig`, `nslookup` |

---

## 🟫 22. Best Practices

✅ Regularly update packages  
✅ Avoid running as root unnecessarily  
✅ Monitor `/var/log` for issues  
✅ Automate with shell scripts  
✅ Use SSH keys instead of passwords  
✅ Always check permissions before execution  

---

**Author:** Sohel Mohammed  
**Goal:** Master Linux for DevOps and Cloud Interviews  
**Confidence:** 90%+ coverage of Linux practical and interview questions

---
