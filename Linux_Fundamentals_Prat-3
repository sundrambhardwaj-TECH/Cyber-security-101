# 🐧 Linux Fundamentals - The Complete Admin & Hacker Guide

Welcome to the ultimate detailed Linux guide! These notes deeply cover Linux system administration, networking, file management, and process automation. These concepts form the backbone for TryHackMe (THM) labs and real-world server management.

---

## 📑 Table of Contents
1. [Text Editors (Nano & Vim)](#1-text-editors-nano--vim)
2. [Downloading Files (Wget & Curl)](#2-downloading-files-wget--curl)
3. [Remote Management (SSH & SCP)](#3-remote-management-ssh--scp)
4. [Serving Files (Python Web Server)](#4-serving-files-python-web-server)
5. [Finding Files (Find & Locate)](#5-finding-files-find--locate)
6. [Process Management (The Task Manager)](#6-process-management-the-task-manager)
7. [Job Control (Backgrounding)](#7-job-control-backgrounding)
8. [Managing Services (Systemctl)](#8-managing-services-systemctl)
9. [Automation with Crontab](#9-automation-with-crontab)
10. [Package Management (APT)](#10-package-management-apt)
11. [System Logging (/var/log)](#11-system-logging-varlog)

---

## 📝 1. Text Editors: Nano & Vim
When you are working on a remote server, you don't have a GUI (Graphical User Interface) like Notepad or Word. You must edit files directly inside the terminal.

### GNU Nano (The Simple Editor)
Nano is straightforward and beginner-friendly. All keyboard shortcuts are always visible at the bottom of the screen.
* **Open/Create a file:** `nano filename.txt`
* **Save File:** Press `Ctrl + O` (WriteOut), then press `Enter`.
* **Exit:** Press `Ctrl + X`.

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
When you are managing a cloud server (like AWS), there is no Chrome browser to right-click and "Save As". You must use terminal commands to download software or scripts.

### `wget` (Web Get)
Designed specifically for downloading files. If a network drops, it can automatically resume the download.
```bash
wget [https://example.com/file.zip](https://example.com/file.zip)
wget -O my_new_name.zip [https://example.com/file.zip](https://example.com/file.zip)  # Save with a custom name
curl (Client URL)More powerful than wget; it is used for data transfer and interacting with APIs. By default, it prints the file's content directly to the terminal instead of saving it.Bashcurl -O [https://example.com/photo.jpg](https://example.com/photo.jpg)  # Save file with its original name
curl -o image.jpg [https://example.com/photo.jpg](https://example.com/photo.jpg)  # Save file with a custom name
🔍 FAQ: Where do I get the download link if I don't have a browser on the server?You use your personal laptop's browser! Right-click any download button or image, select "Copy link address", and then paste that link into your remote terminal alongside the wget command.🔐 3. Remote Management: SSH & SCPSSH (Secure Shell) - The "Magic Portal"SSH allows you to remotely log into a server located anywhere in the world and control its terminal as if you were sitting right in front of it.Bashssh username@remote_host_ip
SCP (Secure Copy Protocol) - The "Courier Service"Used to securely copy files between your local computer and a remote server.💡 The Golden Rule of SCP: The command always follows this structure:scp [Where FROM] [Where TO](Whichever path contains the @ and : is the remote server).Send a file from Local to Server:Bashscp resume.pdf ubuntu@192.168.1.50:/home/ubuntu/
Bring a file from Server to Local:Bashscp ubuntu@192.168.1.50:/home/ubuntu/backup.zip .
(The . at the end means "save it here in my current local folder").Transfer an entire folder: Add the -r (recursive) flag.🌐 4. Serving Files (Python Web Server)If you need to transfer files from your computer to another device on the same Wi-Fi network (without a USB cable), you can turn your Linux machine into a temporary web server using Python.Start the Web Server: Navigate to the folder you want to share and run:Bashpython3 -m http.server 8000
Access the Files: Find your local IP address (using ip a), then open a browser on the receiving device and type: http://<your-ip>:8000Stop the Server: Press Ctrl + C in the terminal.⚠️ Security Warning: Never run this on a Public Wi-Fi network (like an airport), as anyone can access your files. However, it is 100% safe and highly recommended for transferring files inside isolated VPN labs like TryHackMe.🔍 5. Finding Files: Find & LocateThe find Command (Live Deep Search)This command performs a real-time search across the entire hard drive.Bashsudo find / -name "flag.txt"
sudo find / -iname "flag.txt"  # Case-insensitive (finds FLAG, flag, Flag)
sudo find / -name "*flag*"     # Wildcard (finds any file with "flag" in the name)
🛡️ Trick: Searching Without Root (Sudo) PrivilegesIf you search the whole server (/) without root access, Linux will spam your screen with "Permission Denied" errors. To hide them, send the errors to the Linux "black hole" (/dev/null):Bashfind / -name "flag.txt" 2>/dev/null
(This keeps your screen clean, showing only the files you are allowed to see).The locate Command (Instant Search)Searches instantly using a pre-built system database, making it much faster than find. However, for newly created files, you must manually update the database first:Bashsudo updated
locate flag.txt
⚙️ 6. Process Management (The Task Manager)Just like the Windows Task Manager, Linux allows you to view and kill running programs (processes). Every process is assigned a unique "Roll Number" called a PID (Process ID).View All Processes: ps aux (Shows every background and foreground process running on the server).Live Dynamic View: top or htop (Updates every few seconds to show CPU and RAM usage).Filter a Specific Process: ps aux | grep "apache"Killing Processes (Signals)To stop a process, we send it a "Signal" using its PID.Polite Exit (SIGTERM): kill 1997 (Tells the program to save its data and close safely).Force Kill (SIGKILL): kill -9 1997 (If a program is frozen, this forcefully terminates it instantly).Pause (SIGSTOP): kill -SIGSTOP 1997 (Freezes the process temporarily without killing it).🔀 7. Job Control (Backgrounding)When you run a long task (like a massive download), it blocks your terminal. Job control allows you to push tasks to the background so you can keep working.Start a Task in the Background: Add an & at the end of your command.Bash./heavy_script.sh &
Pause a Running Task: Press Ctrl + Z (Suspends the current foreground task).View Hidden Jobs: Type jobs to see all background tasks and their ID numbers.Resume in Background: Type bg %1 to keep the paused task running invisibly.Bring to Foreground: Type fg %1 to bring the task back to your main screen.⚙️ 8. Managing Services (systemctl)Services (Daemons) are background processes that start automatically when the computer boots up (e.g., Web Servers, Databases). We manage them using systemctl.Check Status: systemctl status apache2 (Is it running or dead?)Start/Stop (Current Session): sudo systemctl start apache2 | sudo systemctl stop apache2Restart: sudo systemctl restart apache2Boot-Time AutomationEnable (Auto-Start): sudo systemctl enable apache2 (Tells the OS to start this service automatically every time the computer turns on).Disable: sudo systemctl disable apache2 (Stops it from auto-starting).⏰ 9. Automation with Crontab (Cron Jobs)If you want a script or command to run automatically at a specific time (e.g., a daily midnight backup), you schedule it using the Cron service. The configuration file is called the Crontab.The Crontab Syntax (M-H-DOM-M-DOW)The schedule is defined by 5 asterisks:Plaintext.---------------- minute (0 - 59)
|  .------------- hour (0 - 23)
|  |  .---------- day of month (1 - 31)
|  |  |  .------- month (1 - 12)
|  |  |  |  .---- day of week (0 - 6) (Sunday=0 or 7)
|  |  |  |  |
*  *  *  *  *  /path/to/command
Examples:30 14 * * * /home/user/script.sh $\rightarrow$ Runs every day at 14:30 (2:30 PM).0 5 * * 1 /home/user/script.sh $\rightarrow$ Runs every Monday (1) at 05:00 AM.Essential Commands:crontab -e $\rightarrow$ Edit the cron jobs file.crontab -l $\rightarrow$ List all currently scheduled jobs.crontab -r $\rightarrow$ Remove all scheduled jobs entirely.📦 10. Package Management (apt)APT is the Linux equivalent of the Google Play Store. Software is not downloaded from random websites; it is fetched from secure, centralized servers called Repositories.Update App Registry: sudo apt update (Refreshes the list of available software).Install Software: sudo apt install sublime-textRemove Software: sudo apt remove sublime-textManual Workflow (Adding 3rd Party Apps)If an app (like Sublime Text) isn't in the default Linux store, you must add its custom repository manually:Trust the Developer (GPG Keys): You must download the developer's digital signature (GPG Key) so Linux knows the software hasn't been tampered with by hackers.Add the Repository: You create a new .list file inside /etc/apt/sources.list.d/ pointing to the new software warehouse.Update & Install: Run apt update to recognize the new store, then apt install.📋 11. System Logging (/var/log)Logs are the system's "CCTV cameras" or diary. Every file deletion, failed password attempt, and website visit is recorded here. All logs live in the /var/log directory.Log Rotation (Why files end in .gz)If a web server gets massive traffic, the log file would eventually fill up the entire hard drive. To prevent this, Linux uses "Log Rotation"—it takes old logs, compresses them into .gz zip files, and starts a fresh empty log file automatically.Critical Logs to Monitor:Apache2 (Web Server): /var/log/apache2/access.log (Tracks the IP addresses and request times of all website visitors).Fail2Ban: /var/log/fail2ban.log (Tracks brute-force hackers and the IP addresses the system has banned).UFW (Firewall): /var/log/ufw.log (Tracks allowed and blocked network traffic).Auth Logs: /var/log/auth.log (Tracks every login attempt and sudo command usage).💡 Interview Tip: Reading Massive Log Files (cat vs less)Never use cat to read log files. cat dumps the entire file onto your screen at once. If the file is huge, your terminal will flood with text and freeze.Always use less. The less command loads the file page-by-page, allowing you to scroll safely with your arrow keys without wasting system memory. Furthermore, less is smart enough to read compressed rotated logs (.gz files) directly, without you needing to unzip them first!
