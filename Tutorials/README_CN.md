# 基本 Linux 指令教學
### *若需本指南的英文版本，請參閱 **[English version](../README.md)**.*
---

作者：Charlene  
版本：v1.2  
最後更新：2025-08-28  

> 本文件整理了常見的 Linux 指令，適合初學者快速查找與練習。涵蓋檔案/資料夾操作、檔案檢視、使用者與權限、系統監控、壓縮解壓縮、網路操作與套件管理。附錄提供權限設定表與實用範例。

---

## 目錄
- [1. 檔案與資料夾操作](#1-檔案與資料夾操作)
- [2. 檔案內容檢視](#2-檔案內容檢視)
- [3. 使用者與權限](#3-使用者與權限)
- [4. 系統監控與程序管理](#4-系統監控與程序管理)
- [5. 壓縮與解壓縮](#5-壓縮與解壓縮)
- [6. 網路與連線](#6-網路與連線)
- [7. 軟體安裝與套件管理](#7-軟體安裝與套件管理)
- [8. 其他常用指令](#8-其他常用指令)
- [附錄 A. 權限設定對照表](#附錄-a-權限設定對照表)
- [附錄 B. 常用範例練習](#附錄-b-常用範例練習)
- [附錄 C. 常見錯誤與解決方案](#附錄-c-常見錯誤與解決方案)

---

## 1. 檔案與資料夾操作
```bash
pwd                     # 顯示當前目錄
ls                      # 列出檔案
ls -l                   # 詳細列表（含權限、大小、時間）
ls -lh                  # 以人類可讀單位顯示檔案大小
ls -a                   # 包含隱藏檔
cd /path/to/dir         # 切換資料夾
cd ..                   # 回到上一層
mkdir new_folder        # 建立資料夾
mkdir -p a/b/c          # 一次建立多層資料夾
rmdir empty_folder      # 刪除空資料夾
rm -r folder            # 刪除資料夾（含檔案）
touch file.txt          # 建立空檔案
cp file1 file2          # 複製檔案
cp -r dir1 dir2         # 複製整個資料夾
mv old new              # 重新命名或移動檔案
rm file.txt             # 刪除檔案
find . -name "*.txt"    # 搜尋當前目錄下所有 txt 檔
```

---

## 2. 檔案內容檢視
```bash
cat file.txt            # 顯示檔案全部內容
less file.txt           # 分頁查看檔案內容（上下翻頁）
head file.txt           # 顯示前 10 行
head -n 20 file.txt     # 顯示前 20 行
tail file.txt           # 顯示最後 10 行
tail -f log.txt         # 動態顯示最新內容（監看 log）
grep "keyword" file.txt # 搜尋檔案內含 keyword 的行
grep -r "pattern" ./    # 在資料夾內遞迴搜尋
wc -l file.txt          # 統計檔案行數
wc -w file.txt          # 統計檔案字數
```

---

## 3. 使用者與權限
```bash
whoami                  # 顯示當前使用者
id                      # 顯示 UID 與群組
adduser user1           # 新增使用者
passwd user1            # 設定密碼
su user1                # 切換使用者
sudo command            # 以管理員身份執行

chmod 755 file          # 修改權限 (rwxr-xr-x)
chmod u+x file          # 給檔案擁有者增加執行權限
chown user:group file   # 修改檔案擁有者
groups                  # 查看當前使用者所屬群組
usermod -aG sudo user1  # 將 user1 加入 sudo 群組
```

---

## 4. 系統監控與程序管理
```bash
top                     # 即時顯示 CPU / 記憶體 / 程序
htop                    # 更直觀的 top（需安裝）
ps aux                  # 顯示所有程序
kill -9 PID             # 強制終止程序
jobs                    # 顯示背景工作
fg %1                   # 將第 1 個背景工作切回前景
df -h                   # 顯示磁碟使用量
du -sh folder/          # 顯示資料夾大小
free -h                 # 顯示記憶體狀況
uptime                  # 顯示系統執行時間
uname -a                # 顯示系統資訊
```

---

## 5. 壓縮與解壓縮
```bash
tar -cvf files.tar file1 file2   # 建立 tar 包
tar -xvf files.tar               # 解壓 tar
tar -czvf files.tar.gz folder/   # 建立壓縮檔
tar -xzvf files.tar.gz           # 解壓 tar.gz
zip files.zip file1 file2        # 建立 zip
unzip files.zip                  # 解壓 zip
gzip file.txt                    # 壓縮成 file.txt.gz
gunzip file.txt.gz               # 解壓縮
```

---

## 6. 網路與連線
```bash
ping google.com          # 測試連線
curl http://example.com  # 傳送 HTTP 請求
wget http://file.url     # 下載檔案
scp file.txt user@host:/path/   # 從本機傳送檔案到遠端
scp user@host:/path/file .      # 從遠端下載檔案
ssh user@host            # SSH 連線到遠端伺服器
ifconfig                 # 顯示網路設定（舊版系統）
ip a                     # 顯示網路設定（較新系統）
```

---

## 7. 軟體安裝與套件管理

在 Linux 中，軟體與套件的安裝方式很多，常見的有 **系統套件管理工具**（apt, yum, dnf）、**語言專屬套件管理器**（pip, conda, CRAN, Bioconductor）等。以下整理安裝方式與常見錯誤。

---

### 7.1 系統套件管理工具

#### Debian/Ubuntu (apt)
```bash
sudo apt update          # 更新套件列表
sudo apt upgrade         # 升級所有已安裝套件
sudo apt install pkg     # 安裝套件
sudo apt remove pkg      # 移除套件
```

#### Red Hat/CentOS (yum/dnf)
```bash
sudo yum install pkg     # 安裝套件
sudo yum update          # 更新套件
sudo yum remove pkg      # 移除套件
```

> **常見錯誤與原因：**
> - `E: Unable to locate package xxx` → 套件名稱錯誤或缺少套件源（需 `sudo apt update` 或新增 repository）。
> - `Permission denied` → 未使用 `sudo` 嘗試安裝系統層級套件。

---

### 7.2 Python 套件管理

#### pip (安裝到系統或使用者目錄)
```bash
pip install package              # 預設安裝到系統路徑（需 sudo）
pip install --user package       # 安裝到使用者目錄 (~/.local/lib/pythonX.X/site-packages)
```

#### conda (推薦用於隔離環境)
```bash
conda create -n myenv python=3.11
conda activate myenv
conda install package
```

> **常見錯誤與解法：**
> - `ModuleNotFoundError`：套件已安裝，但安裝位置不在 `PYTHONPATH`。
> - `pip install` 安裝到 root `/usr/lib` 時，非 sudo 用戶無法使用。  
>   → 解法：加上 `--user` 或建立 `virtualenv/conda env`。

---

### 7.3 R 套件管理

#### CRAN
```R
install.packages("dplyr")                 # 預設安裝到系統資料夾
install.packages("dplyr", lib="~/Rlib")   # 安裝到自訂路徑
```

#### Bioconductor
```R
if (!require("BiocManager")) install.packages("BiocManager")
BiocManager::install("DESeq2")
```

> **常見錯誤與解法：**
> - `library(xxx) 中錯誤：找不到套件` → 已安裝但 lib 路徑未設定。
>   ```R
>   .libPaths()                         # 檢查目前的 R 套件路徑
>   .libPaths(c("~/Rlib", .libPaths())) # 加入自訂路徑
>   ```

---

### 7.4 套件位置與環境設定

Linux 的程式與套件可能安裝在不同資料夾，例如：
- `/usr/bin/` → 系統主要程式
- `/usr/local/bin/` → 手動編譯安裝的程式
- `~/.local/bin/` → 使用者安裝的程式（無 root 權限時）
- `~/anaconda3/envs/` → conda 環境專用

#### 如何確認套件位置
```bash
which python3             # 查看執行檔路徑
whereis python3           # 顯示相關檔案位置
pip show package_name     # 顯示 Python 套件安裝位置
Rscript -e '.libPaths()'  # 查看 R 套件安裝路徑
```

#### 避免安裝受限於 root 權限的方法
1. **使用 `--user`**：安裝到使用者目錄。
2. **修改環境變數 PATH**：確保系統能找到安裝在 `~/.local/bin` 的可執行檔。
   ```bash
   echo 'export PATH=$HOME/.local/bin:$PATH' >> ~/.bashrc
   source ~/.bashrc
   ```
3. **使用虛擬環境**：避免與系統套件衝突（如 Python 的 `venv` / conda）。

### 範例：fastp 安裝後無法直接執行

假設我們使用 `conda` 或 `pip install --user fastp` 安裝，程式可能會被放在：
```
~/.local/bin/fastp
```

此時若直接輸入：
```bash
fastp -h
```
會出現：
```
bash: fastp: command not found
```

原因是 `~/.local/bin` 不在 `PATH` 裡。

**解決方式：將其加入 PATH**
```bash
echo 'export PATH=$HOME/.local/bin:$PATH' >> ~/.bashrc
source ~/.bashrc
```

再確認：
```bash
which fastp
# 輸出應該會是 /home/username/.local/bin/fastp
```

這樣就能直接執行 `fastp`，不用每次輸入完整路徑。


---

### 7.5 常見問題整理
- **安裝到錯誤目錄** → 使用 `.libPaths()` (R) 或 `pip show` (Python) 檢查。
- **找不到指令** → 套件安裝在 `~/.local/bin`，需加到 `PATH`。
- **權限不足** → 避免用 root，建議用 `--user` 或 conda 虛擬環境。
- **不同版本衝突** → 建議在隔離環境安裝（conda, venv, renv）。

---

## 8. 其他常用指令
```bash
man ls                   # 顯示指令說明 (manual)
history                  # 查看歷史指令
clear                    # 清空終端畫面
echo "Hello"             # 輸出文字
date                     # 顯示日期時間
who                      # 顯示登入使用者
alias ll='ls -lh'        # 建立快捷指令
```

---

## 附錄 A. 權限設定對照表

| 權限值 | 說明 | 二進位 | 對應權限 (r=讀, w=寫, x=執行) |
|--------|------|--------|-------------------------------|
| 0      | 無權限 | 000 | --- |
| 1      | 執行  | 001 | --x |
| 2      | 寫入  | 010 | -w- |
| 3      | 寫+執 | 011 | -wx |
| 4      | 讀取  | 100 | r-- |
| 5      | 讀+執 | 101 | r-x |
| 6      | 讀+寫 | 110 | rw- |
| 7      | 全部  | 111 | rwx |

### 範例：
- `chmod 644 file.txt` → 擁有者可讀寫，群組與其他人僅可讀  
- `chmod 755 script.sh` → 擁有者可讀寫執行，其他人可讀與執行  
- `chmod 777 test.sh` → 所有人皆有讀寫執行權限（⚠ 不建議）

---

## 附錄 B. 常用範例練習
1. 建立一個資料夾 `practice` 並進入：  
   ```bash
   mkdir practice && cd practice
   ```
2. 建立檔案 `note.txt` 並寫入一些文字：  
   ```bash
   echo "Hello Linux" > note.txt
   ```
3. 檢視與搜尋內容：  
   ```bash
   cat note.txt
   grep "Linux" note.txt
   ```
4. 修改檔案權限：  
   ```bash
   chmod 600 note.txt   # 只有自己可讀寫
   ls -l
   ```
5. 將資料夾壓縮與解壓縮：  
   ```bash
   tar -czvf practice.tar.gz practice/
   tar -xzvf practice.tar.gz
   ```
6. 使用 SSH 登入遠端伺服器（需帳號密碼）：  
   ```bash
   ssh user@hostname
   ```

---

## 附錄 C. 常見錯誤與解決方案

| 錯誤訊息 | 可能原因 | 解決方案 |
|----------|----------|----------|
| `E: Unable to locate package xxx` | 套件名稱錯誤或缺少來源 | 確認套件名稱，或執行 `sudo apt update` 更新來源 |
| `Permission denied` | 嘗試在無權限目錄安裝 | 使用 `sudo` 或改用 `--user` 安裝到使用者目錄 |
| `ModuleNotFoundError` (Python) | 套件已安裝但不在 `PYTHONPATH` | 使用 `pip show` 找位置，或設定 `export PYTHONPATH` |
| `library(xxx) 中錯誤：找不到套件` (R) | 安裝路徑不在 `.libPaths()` | 在 R 中執行 `.libPaths(c("~/Rlib", .libPaths()))` |
| `command not found` | 程式安裝在 `~/.local/bin`，未加入 PATH | 在 `~/.bashrc` 加入 `export PATH=$HOME/.local/bin:$PATH` |
| 套件版本衝突 | 同時存在多版本 | 建立 conda/venv 隔離環境，或用 R 的 renv 管理 |

---

✅ 本文件可作為快速查詢手冊、練習手冊與錯誤排查工具。
