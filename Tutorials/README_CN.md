# 基本 Linux 指令教學
### *若需本指南的英文版本，請參閱 **[English version](../README.md)**.*
---

作者：Charlene  
版本：v1.1  
最後更新：2025-08-24  

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
### Debian/Ubuntu (apt)
```bash
sudo apt update          # 更新套件列表
sudo apt upgrade         # 升級所有已安裝套件
sudo apt install pkg     # 安裝套件
sudo apt remove pkg      # 移除套件
```

### Red Hat/CentOS (yum/dnf)
```bash
sudo yum install pkg     # 安裝套件
sudo yum update          # 更新套件
sudo yum remove pkg      # 移除套件
```

### 常見工具
```bash
which python3            # 查看程式路徑
whereis python3          # 顯示程式相關檔案位置
```

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

✅ 本文件可作為快速查詢手冊與練習手冊使用。
