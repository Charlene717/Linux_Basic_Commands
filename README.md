# Basic Linux Commands Guide
### *For the Chinese version of this guide, please see the **[中文版本](./Tutorials/README_CN.md)**.*
---

Author: Charlene  
Version: v1.1  
Last Updated: 2025-08-24  

> This document summarizes common Linux commands, useful for beginners as a quick reference and practice guide. It covers file/directory operations, file viewing, user and permission management, system monitoring, compression/extraction, networking, and package management. Appendices include a permission table and practical examples.

---

## Table of Contents
- [1. File and Directory Operations](#1-file-and-directory-operations)
- [2. Viewing File Contents](#2-viewing-file-contents)
- [3. Users and Permissions](#3-users-and-permissions)
- [4. System Monitoring and Process Management](#4-system-monitoring-and-process-management)
- [5. Compression and Extraction](#5-compression-and-extraction)
- [6. Networking and Connections](#6-networking-and-connections)
- [7. Software Installation and Package Management](#7-software-installation-and-package-management)
- [8. Other Useful Commands](#8-other-useful-commands)
- [Appendix A. Permission Settings Table](#appendix-a-permission-settings-table)
- [Appendix B. Common Practice Examples](#appendix-b-common-practice-examples)

---

## 1. File and Directory Operations
```bash
pwd                     # Show current directory
ls                      # List files
ls -l                   # Detailed list (permissions, size, date)
ls -lh                  # Human-readable file sizes
ls -a                   # Include hidden files
cd /path/to/dir         # Change directory
cd ..                   # Go up one level
mkdir new_folder        # Create a directory
mkdir -p a/b/c          # Create nested directories
rmdir empty_folder      # Remove empty directory
rm -r folder            # Remove directory with files
touch file.txt          # Create an empty file
cp file1 file2          # Copy file
cp -r dir1 dir2         # Copy directory
mv old new              # Rename or move file
rm file.txt             # Remove file
find . -name "*.txt"    # Find all txt files in current path
```

---

## 2. Viewing File Contents
```bash
cat file.txt            # Display file contents
less file.txt           # View file page by page
head file.txt           # Show first 10 lines
head -n 20 file.txt     # Show first 20 lines
tail file.txt           # Show last 10 lines
tail -f log.txt         # Continuously watch a log file
grep "keyword" file.txt # Search for keyword in file
grep -r "pattern" ./    # Recursively search in directory
wc -l file.txt          # Count lines in file
wc -w file.txt          # Count words in file
```

---

## 3. Users and Permissions
```bash
whoami                  # Show current user
id                      # Show UID and groups
adduser user1           # Add new user
passwd user1            # Set password
su user1                # Switch user
sudo command            # Run command as administrator

chmod 755 file          # Change permission (rwxr-xr-x)
chmod u+x file          # Give owner execute permission
chown user:group file   # Change file ownership
groups                  # Show current user's groups
usermod -aG sudo user1  # Add user1 to sudo group
```

---

## 4. System Monitoring and Process Management
```bash
top                     # Real-time CPU / memory / processes
htop                    # User-friendly top (requires install)
ps aux                  # Show all processes
kill -9 PID             # Kill process by PID
jobs                    # Show background jobs
fg %1                   # Bring job 1 to foreground
df -h                   # Disk usage
du -sh folder/          # Folder size
free -h                 # Memory usage
uptime                  # Show system uptime
uname -a                # System information
```

---

## 5. Compression and Extraction
```bash
tar -cvf files.tar file1 file2   # Create tar archive
tar -xvf files.tar               # Extract tar archive
tar -czvf files.tar.gz folder/   # Create compressed archive
tar -xzvf files.tar.gz           # Extract compressed archive
zip files.zip file1 file2        # Create zip
unzip files.zip                  # Extract zip
gzip file.txt                    # Compress into file.txt.gz
gunzip file.txt.gz               # Decompress
```

---

## 6. Networking and Connections
```bash
ping google.com          # Test connectivity
curl http://example.com  # Send HTTP request
wget http://file.url     # Download file
scp file.txt user@host:/path/   # Copy file to remote
scp user@host:/path/file .      # Download file from remote
ssh user@host            # SSH connect to remote server
ifconfig                 # Show network settings (older)
ip a                     # Show network settings (newer)
```

---

## 7. Software Installation and Package Management
### Debian/Ubuntu (apt)
```bash
sudo apt update          # Update package list
sudo apt upgrade         # Upgrade installed packages
sudo apt install pkg     # Install package
sudo apt remove pkg      # Remove package
```

### Red Hat/CentOS (yum/dnf)
```bash
sudo yum install pkg     # Install package
sudo yum update          # Update packages
sudo yum remove pkg      # Remove package
```

### Useful tools
```bash
which python3            # Find program path
whereis python3          # Show locations related to program
```

---

## 8. Other Useful Commands
```bash
man ls                   # Show manual for command
history                  # Show command history
clear                    # Clear terminal screen
echo "Hello"             # Print text
date                     # Show date/time
who                      # Show logged-in users
alias ll='ls -lh'        # Create command shortcut
```

---

## Appendix A. Permission Settings Table

| Value | Meaning | Binary | Permission (r=read, w=write, x=execute) |
|-------|---------|--------|------------------------------------------|
| 0     | No perm | 000    | --- |
| 1     | Execute | 001    | --x |
| 2     | Write   | 010    | -w- |
| 3     | W+Exec  | 011    | -wx |
| 4     | Read    | 100    | r-- |
| 5     | R+Exec  | 101    | r-x |
| 6     | R+Write | 110    | rw- |
| 7     | All     | 111    | rwx |

### Examples:
- `chmod 644 file.txt` → Owner read/write, group/others read only  
- `chmod 755 script.sh` → Owner full, group/others read+execute  
- `chmod 777 test.sh` → Everyone full (⚠ Not recommended)  

---

## Appendix B. Common Practice Examples
1. Create folder `practice` and enter it:  
   ```bash
   mkdir practice && cd practice
   ```
2. Create `note.txt` and write text:  
   ```bash
   echo "Hello Linux" > note.txt
   ```
3. View and search file:  
   ```bash
   cat note.txt
   grep "Linux" note.txt
   ```
4. Change file permission:  
   ```bash
   chmod 600 note.txt   # Only owner read/write
   ls -l
   ```
5. Compress and extract:  
   ```bash
   tar -czvf practice.tar.gz practice/
   tar -xzvf practice.tar.gz
   ```
6. Connect to remote via SSH:  
   ```bash
   ssh user@hostname
   ```

---

✅ This document can be used as a quick reference and practice guide.
