# Basic Linux Command Guide
### *For the Chinese version of this guide, please refer to **[中文版](../Tutorials/README_CN.md)**.*
---

Author: Charlene  
Version: v1.2  
Last Updated: 2025-08-28  

> This document summarizes common Linux commands, suitable for beginners to quickly look up and practice. It covers file/folder operations, file viewing, users & permissions, system monitoring, compression & decompression, networking, and package management. Appendices include a permission table, practice examples, and troubleshooting guide.

---

## Table of Contents
- [1. File and Directory Operations](#1-file-and-directory-operations)
- [2. Viewing File Contents](#2-viewing-file-contents)
- [3. Users and Permissions](#3-users-and-permissions)
- [4. System Monitoring and Process Management](#4-system-monitoring-and-process-management)
- [5. Compression and Decompression](#5-compression-and-decompression)
- [6. Networking and Connections](#6-networking-and-connections)
- [7. Software Installation and Package Management](#7-software-installation-and-package-management)
- [8. Other Useful Commands](#8-other-useful-commands)
- [Appendix A. Permission Table](#appendix-a-permission-table)
- [Appendix B. Practice Examples](#appendix-b-practice-examples)
- [Appendix C. Common Errors and Solutions](#appendix-c-common-errors-and-solutions)

---

## 1. File and Directory Operations
```bash
pwd                     # Show current directory
ls                      # List files
ls -l                   # Detailed list (permissions, size, time)
ls -lh                  # Human-readable file sizes
ls -a                   # Include hidden files
cd /path/to/dir         # Change directory
cd ..                   # Go up one level
mkdir new_folder        # Create directory
mkdir -p a/b/c          # Create nested directories
rmdir empty_folder      # Remove empty directory
rm -r folder            # Remove directory (with files)
touch file.txt          # Create empty file
cp file1 file2          # Copy file
cp -r dir1 dir2         # Copy entire directory
mv old new              # Rename or move file
rm file.txt             # Delete file
find . -name "*.txt"    # Search for all txt files in current directory
```

---

## 2. Viewing File Contents
```bash
cat file.txt            # Show full content
less file.txt           # View content with paging
head file.txt           # Show first 10 lines
head -n 20 file.txt     # Show first 20 lines
tail file.txt           # Show last 10 lines
tail -f log.txt         # Monitor log updates
grep "keyword" file.txt # Search for keyword in file
grep -r "pattern" ./    # Recursive search in directory
wc -l file.txt          # Count lines
wc -w file.txt          # Count words
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

chmod 755 file          # Change permissions (rwxr-xr-x)
chmod u+x file          # Add execute permission to owner
chown user:group file   # Change file owner
groups                  # Show groups of current user
usermod -aG sudo user1  # Add user1 to sudo group
```

---

## 4. System Monitoring and Process Management
```bash
top                     # Real-time CPU/memory/processes
htop                    # More visual top (requires install)
ps aux                  # Show all processes
kill -9 PID             # Force kill process
jobs                    # Show background jobs
fg %1                   # Bring background job 1 to foreground
df -h                   # Show disk usage
du -sh folder/          # Show directory size
free -h                 # Show memory usage
uptime                  # Show system uptime
uname -a                # Show system info
```

---

## 5. Compression and Decompression
```bash
tar -cvf files.tar file1 file2   # Create tar archive
tar -xvf files.tar               # Extract tar
tar -czvf files.tar.gz folder/   # Create compressed tar.gz
tar -xzvf files.tar.gz           # Extract tar.gz
zip files.zip file1 file2        # Create zip
unzip files.zip                  # Extract zip
gzip file.txt                    # Compress file.txt to file.txt.gz
gunzip file.txt.gz               # Decompress
```

---

## 6. Networking and Connections
```bash
ping google.com          # Test connection
curl http://example.com  # Send HTTP request
wget http://file.url     # Download file
scp file.txt user@host:/path/   # Upload file to remote host
scp user@host:/path/file .      # Download file from remote host
ssh user@host            # SSH into remote server
ifconfig                 # Show network settings (older systems)
ip a                     # Show network settings (newer systems)
```

---

## 7. Software Installation and Package Management

Linux provides many ways to install software and packages, commonly **system package managers** (apt, yum, dnf) and **language-specific managers** (pip, conda, CRAN, Bioconductor). Below are examples and common issues.

---

### 7.1 System Package Managers

#### Debian/Ubuntu (apt)
```bash
sudo apt update          # Update package list
sudo apt upgrade         # Upgrade all packages
sudo apt install pkg     # Install package
sudo apt remove pkg      # Remove package
```

#### Red Hat/CentOS (yum/dnf)
```bash
sudo yum install pkg     # Install package
sudo yum update          # Update packages
sudo yum remove pkg      # Remove package
```

> **Common Errors:**
> - `E: Unable to locate package xxx` → Package not found or repo missing (run `sudo apt update` or add repository).
> - `Permission denied` → Missing `sudo` when installing system-level package.

---

### 7.2 Python Package Management

#### pip (system vs user install)
```bash
pip install package              # Install to system path (requires sudo)
pip install --user package       # Install to user path (~/.local/lib/pythonX.X/site-packages)
```

#### conda (recommended for isolated environments)
```bash
conda create -n myenv python=3.11
conda activate myenv
conda install package
```

> **Common Issues:**
> - `ModuleNotFoundError` → Installed but not in `PYTHONPATH`.
> - Installed into `/usr/lib` → Normal users cannot use.  
>   → Fix: Use `--user` or create virtualenv/conda env.

---

### 7.3 R Package Management

#### CRAN
```R
install.packages("dplyr")                 # Install to system directory
install.packages("dplyr", lib="~/Rlib")   # Install to custom path
```

#### Bioconductor
```R
if (!require("BiocManager")) install.packages("BiocManager")
BiocManager::install("DESeq2")
```

> **Common Issues:**
> - `Error in library(xxx): there is no package called 'xxx'` → Installed but path not set.  
>   ```R
>   .libPaths()                         # Check current library paths
>   .libPaths(c("~/Rlib", .libPaths())) # Add custom path
>   ```

---

### 7.4 Package Locations and Environment Settings

Packages may be installed in different locations:
- `/usr/bin/` → System programs
- `/usr/local/bin/` → Manually compiled programs
- `~/.local/bin/` → User-installed (no root required)
- `~/anaconda3/envs/` → Conda environments

#### Check Installation Paths
```bash
which python3             # Path to executable
whereis python3           # Show related files
pip show package_name     # Show Python package location
Rscript -e '.libPaths()'  # Show R package paths
```

#### Avoid Root Restrictions
1. **Use `--user`**: Install to user path.  
2. **Modify PATH**: Ensure system finds executables in `~/.local/bin`.  
   ```bash
   echo 'export PATH=$HOME/.local/bin:$PATH' >> ~/.bashrc
   source ~/.bashrc
   ```
3. **Use Virtual Environments**: Avoid conflicts (Python venv/conda, R renv).

---

### 7.5 Common Problems Summary
- **Wrong install path** → Check with `.libPaths()` (R) or `pip show` (Python).
- **Command not found** → Installed in `~/.local/bin`, add to `PATH`.
- **Permission denied** → Use `--user` or conda env instead of root.
- **Version conflicts** → Use isolated environments (conda, venv, renv).

---

## 8. Other Useful Commands
```bash
man ls                   # Show manual page
history                  # Show command history
clear                    # Clear terminal
echo "Hello"             # Print text
date                     # Show date/time
who                      # Show logged-in users
alias ll='ls -lh'        # Create alias
```

---

## Appendix A. Permission Table

| Value | Description | Binary | Permissions (r=read, w=write, x=execute) |
|-------|-------------|--------|-------------------------------------------|
| 0     | None        | 000    | --- |
| 1     | Execute     | 001    | --x |
| 2     | Write       | 010    | -w- |
| 3     | Write+Exec  | 011    | -wx |
| 4     | Read        | 100    | r-- |
| 5     | Read+Exec   | 101    | r-x |
| 6     | Read+Write  | 110    | rw- |
| 7     | All         | 111    | rwx |

### Examples:
- `chmod 644 file.txt` → Owner read/write, group & others read-only  
- `chmod 755 script.sh` → Owner read/write/execute, others read & execute  
- `chmod 777 test.sh` → Everyone read/write/execute (⚠ not recommended)

---

## Appendix B. Practice Examples
1. Create a folder `practice` and enter it:  
   ```bash
   mkdir practice && cd practice
   ```
2. Create file `note.txt` with text:  
   ```bash
   echo "Hello Linux" > note.txt
   ```
3. View and search content:  
   ```bash
   cat note.txt
   grep "Linux" note.txt
   ```
4. Modify file permissions:  
   ```bash
   chmod 600 note.txt   # Only owner can read/write
   ls -l
   ```
5. Compress and decompress folder:  
   ```bash
   tar -czvf practice.tar.gz practice/
   tar -xzvf practice.tar.gz
   ```
6. SSH into remote server (needs account/password):  
   ```bash
   ssh user@hostname
   ```

---

## Appendix C. Common Errors and Solutions

| Error Message | Possible Cause | Solution |
|---------------|----------------|----------|
| `E: Unable to locate package xxx` | Wrong package name or repo missing | Check name, run `sudo apt update` |
| `Permission denied` | Trying to install in restricted dir | Use `sudo` or `--user` |
| `ModuleNotFoundError` (Python) | Installed but not in `PYTHONPATH` | Run `pip show`, set `PYTHONPATH` |
| `Error in library(xxx): there is no package called 'xxx'` (R) | Path not included in `.libPaths()` | Add path via `.libPaths(c("~/Rlib", .libPaths()))` |
| `command not found` | Program in `~/.local/bin` not in PATH | Add `export PATH=$HOME/.local/bin:$PATH` |
| Version conflicts | Multiple versions installed | Use conda/venv/renv for isolation |

---

✅ This document serves as a quick reference, practice manual, and troubleshooting guide.
