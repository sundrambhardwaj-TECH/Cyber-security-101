# 🐧 Linux Fundamentals - Complete Admin & Hacker Guide

Welcome to the ultimate Linux guide! These notes deeply cover Linux system administration, networking, file management, and process automation. These commands form the backbone for TryHackMe (THM) labs and real-world server management.

---

## 📑 Table of Contents
1. Text Editors (Nano & Vim)
2. Downloading Files (Wget & Curl)
3. Remote Management (SSH & SCP)
4. Serving Files (Python Web Server)
5. Finding Files (Find & Locate)
6. Process Management (The Task Manager)
7. Job Control (Backgrounding)
8. Managing Services (Systemctl)
9. Automation with Crontab
10. Package Management (APT)
11. System Logging (/var/log)

---

## 📝 1. Text Editors: Nano & Vim
We use text editors to create and modify files directly within the Linux terminal.

### GNU Nano (The Simple Editor)
* Open/Create a file: `nano filename.txt`
* Save File: `Ctrl + O`, then press `Enter`
* Exit: `Ctrl + X`

### Vim (The Power Editor)
Vim is highly advanced and operates entirely on keyboard shortcuts without a mouse. It uses different **Modes**:
* **Command Mode (Default):** When you open a file, you cannot type text immediately. You can only copy, paste, delete, or navigate.
* **Insert Mode (For Typing):** Press `i` to enter Insert Mode and start typing normally.
* **Escape:** Press `Esc` to stop typing and return to Command Mode.

**Essential Vim Shortcuts (in Command Mode):**
* `dd` $\rightarrow$ Delete an entire line.
* `yy` $\rightarrow$ Copy an entire line.
* `p` $\rightarrow$ Paste the copied line.
* `x` $\rightarrow$ Delete a single character.

**How to Exit Vim (The famous question):**
While in Command Mode, press `:` (colon) and type:
* `:w` $\rightarrow$ Save (write) the file.
* `:q` $\rightarrow$ Quit (if no changes were made).
* `:wq` $\rightarrow$ Save and quit.
* `:q!` $\rightarrow$ Force quit without saving.

---

## 🌐 2. Downloading Files: wget vs curl
Tools used to download files from the internet directly to your server.

### wget (Web Get)
Best used strictly for downloading files. It supports automatic resuming for interrupted downloads.
wget https://example.com/file.zip
wget -O new_name.zip https://example.com/file.zip  # Save with a new name

### curl (Client URL)
Best for data transfer and interacting with APIs.
curl -O https://example.com/photo.jpg  # Save with the original name
curl -o image.jpg https://example.com/photo.jpg  # Save with a new name

> FAQ: Where do I get the download link in the terminal?
> Right-click on any download button or image in your web browser
> -> select "Copy link address", and paste it into the terminal.

---

## 🔐 3. Remote Management: SSH & SCP

### SSH (Secure Shell)
Used to gain secure terminal control over a remote server:
ssh username@remote_host_ip

### SCP (Secure Copy Protocol)
Used to securely transfer files between your local machine and a remote server.
> SCP Direction Rule: `scp [SOURCE] [DESTINATION]` (The part containing @ and : is the server path).

* Send from Local to Server:
  scp resume.pdf ubuntu@192.168.1.50:/home/ubuntu/

* Bring from Server to Local:
  scp ubuntu@192.168.1.50:/home/ubuntu/backup.zip .

* Transfer an entire folder: Use the `-r` (recursive) flag.

---

## 🌐 4. Serving Files (Python Web Server)
The easiest way to share files from your host machine to devices on your local network.

* Start Web Server: Run this command inside the folder you want to share:
  python3 -m http.server 8000

* Access Files: On another device's browser, type http://<your-ip>:8000
* Stop Server: Press Ctrl + C.

> Security Warning: Never run this on a Public Wi-Fi (like a cafe or airport). It is 100% safe and recommended for TryHackMe / VPN Labs.

---

## 🔍 5. Finding Files: Find & Locate

### The find Command (Live Deep Search)
Used for real-time, exhaustive searching.
sudo find / -name "flag.txt"
sudo find / -iname "flag.txt"  # Case-insensitive
sudo find / -name "*flag*"     # Wildcard search

> No Root (Sudo) Privilege? No Problem!
> To hide annoying permission errors, append 2>/dev/null (this sends all errors to a digital black hole):
> find / -name "flag.txt" 2>/dev/null

### The locate Command (Instant Search)
Searches incredibly fast using a pre-built system database. For newly created files, you must update the database first by running `sudo updatedb`.
locate flag.txt

---

## ⚙️ 6. Process Management (The Task Manager)

* View Active Processes: `ps aux` (Lists processes for all users on the server)
* Live Dynamic View: `top` or `htop`
* Filter Process: `ps aux | grep "apache"`

### Killing Processes (Signals)
* kill <PID>: (SIGTERM) A polite exit, giving the program time to save data and close safely.
* kill -9 <PID>: (SIGKILL) Force kill, terminates the process instantly if it's frozen.
* kill -SIGSTOP <PID>: Pauses/freezes the process temporarily.

---

## 🔀 7. Job Control (Backgrounding)
Tricks for multitasking and keeping your terminal free for other commands.

* Start in Background: Add an & at the end of the command.
  ./heavy_script.sh &

* Pause Task: Ctrl + Z
* View Jobs: jobs
* Resume in Background: bg %1
* Bring to Foreground: fg %1

---

## ⚙️ 8. Managing Services (systemctl)
Used to manage background processes (Daemons) that start when the system boots up.

* Check Status: systemctl status apache2
* Start/Stop: sudo systemctl start apache2 | sudo systemctl stop apache2
* Restart: sudo systemctl restart apache2
* Auto-Start on Boot (Enable/Disable): 
  sudo systemctl enable apache2
  sudo systemctl disable apache2

---

## ⏰ 9. Automation with Crontab (Cron Jobs)
Used to schedule scripts or commands to run automatically at specific times.

Syntax (M-H-DOM-M-DOW):
Minute | Hour | Day of Month | Month | Day of Week
.---------------- minute (0 - 59)
|  .------------- hour (0 - 23)
|  |  .---------- day of month (1 - 31)
|  |  |  .------- month (1 - 12)
|  |  |  |  .---- day of week (0 - 6) (Sunday=0 or 7)
|  |  |  |  |
*  *  *  *  *  /path/to/command
              
* Edit Jobs: crontab -e
* List Jobs: crontab -l
* Remove All Jobs: crontab -r

Example (Run every Monday at 5:00 AM):
0 5 * * 1 /home/user/script.sh

---

## 📦 10. Package Management (apt)
The "App Store" of Linux. Packages are stored in remote vaults called Repositories.

* Update App Registry: sudo apt update
* Install Software: sudo apt install sublime-text
* Remove Software: sudo apt remove sublime-text

> Note: To add third-party repositories, you must first add their GPG Keys to verify the software's security and integrity. New repositories are saved in /etc/apt/sources.list.d/.

---

## 📋 11.  System Logging (/var/log)
The system's CCTV camera. All activities, authentications, and errors are recorded here. (To save storage space, Linux automatically zips older logs—a process known as Log Rotation).

### Critical Logs:
* Apache2 (Web Server): /var/log/apache2/access.log (Tracks website visitors) and error.log.
* Fail2Ban: /var/log/fail2ban.log (Tracks brute-force attacks and banned IPs).
* UFW (Firewall): /var/log/ufw.log (Tracks blocked and allowed network traffic).
* Auth Logs: /var/log/auth.log (Tracks logins and sudo command usage).

> Pro-Tip: How to read large Log Files?
> Never use `cat` for logs (it can flood and hang your terminal). Always use the `less` command. It opens the file page-by-page and can natively read compressed (.gz) files without needing to unzip them first.
> To watch live logs: tail -f /var/log/apache2/access.log


