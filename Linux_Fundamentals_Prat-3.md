🐧 Linux Fundamentals - The Complete Admin & Hacker Guide
Welcome to the comprehensive Linux systems guide! These notes cover everything from core OS architecture, text editors, and networking to process management, automation, package management, and system logs. These concepts form the absolute backbone for systems administration, TryHackMe (THM) labs, and real-world Linux engineering.

1. Core OS Architecture & System Performance
Linux is fundamentally different from operating systems like Windows.

Lightweight Architecture: Linux is incredibly lightweight because it doesn't force a heavy Graphical User Interface (GUI) to run in the background. A minimal Linux server can run perfectly on as little as 512 MB of RAM.
The Linux Kernel: "Linux" itself is technically not an operating system; it is a Kernel (the core engine that lets software talk to hardware).
Linux Distributions (Distros): Operating systems built on top of the Linux kernel are called distributions.
Ubuntu: A user-friendly, lightweight distribution perfect for general server usage.
Kali Linux: A specialized distribution packed with security tools used for security testing.
2. Text Editors: Nano & Vim
When managing a Linux server remotely, you do not have access to graphical applications like Notepad. You must write and edit text files directly inside the command line terminal.

GNU Nano (The Simple Editor)
Nano is straightforward and beginner-friendly. All active shortcuts are visibly displayed at the bottom of the terminal screen.

Open or Create a file: nano filename.txt
Save Changes: Press Ctrl + O (WriteOut), then press Enter.
Exit Editor: Press Ctrl + X.
Vim (The Power Editor)
Vim is an advanced editor that operates entirely on keyboard shortcuts and relies heavily on Modes:

Command Mode (Default): You cannot type text here. Keys act as editing shortcuts.
Insert Mode (For Typing): Press i to enter Insert Mode. You can now type normally.
Return to Command Mode: Press the Esc key to use shortcuts again.
Essential Vim Shortcuts (Command Mode): dd (delete line), yy (copy line), p (paste), x (delete character).

Exiting Vim: Type a colon (:) followed by wq (save and quit) or q! (force quit without saving).

3. Downloading Files: wget vs curl
Tools used instead of a browser to download files and software tools from the internet.

wget (Web Get)
wget https://example.com/file.zip
wget -O custom_name.zip https://example.com/file.zip  # Save with a new filename
curl (Client URL)
curl -O https://example.com/photo.jpg  # Save file with its original name
curl -o image.jpg https://example.com/photo.jpg  # Save file with a custom name
4. Remote Management & File Transfer (SSH & SCP)
SSH (Secure Shell)
ssh username@remote_host_ip
SCP (Secure Copy Protocol)
The Golden Rule of SCP Direction: Always structure your command as:
scp [Where FROM] [Where TO]
# Upload a file from Local Machine to Remote Server:
scp document.pdf ubuntu@192.168.1.50:/home/ubuntu/

# Download a file from Remote Server to Local Machine:
scp ubuntu@192.168.1.50:/home/ubuntu/backup.zip .
5. Serving Files (Python Web Server Method)
If you need to transfer files from a target server back to your host machine easily, you can turn any directory into a temporary web server.

# Start the Temporary Web Server:
python3 -m http.server 8000

# Download the File on the Host Machine:
wget http://<target-server-ip>:8000/flag.txt
Note: If the file name starts with a dot, such as .flag.txt, it is a hidden file. Use ls -a to view it after downloading.
6. Deep File Searching (Find & Locate)
The find Command (Live Deep Search)
find / -name "flag.txt" 2>/dev/null  # 2>/dev/null hides permission denied errors
The locate Command (Instant Indexed Search)
sudo updatedb && locate flag.txt
7. Process Management (The Task Manager)
View All Active Processes: ps aux
Live Dynamic Monitoring: top or htop
Killing Processes: kill PID (Polite exit via SIGTERM) or kill -9 PID (Force kill via SIGKILL).

8. Job Control (Backgrounding & Multitasking)
Launch into the Background: Add an & at the end of your command.
Pause a Foreground Task: Press Ctrl + Z.
Manage Jobs: Use jobs to view, bg %1 to resume in background, and fg %1 to bring to foreground.
9. Managing Services & Daemons (Systemctl)
systemctl status apache2   # Check health
sudo systemctl start apache2  # Start service
sudo systemctl enable apache2 # Auto-start on boot
10. Task Automation (Crontab Rules & Syntax)
The schedule syntax is mapped out using 5 distinct time positions: Minute, Hour, Day of Month, Month, Day of Week (M-H-DOM-M-DOW).

# Syntax: * * * * * /path/to/command
0 5 * * 1 /scripts/cleanup.sh  # Fires once a week every single Monday at exactly 05:00 AM.
11. Package Management & Software Repositories (APT)
sudo apt update   # Refresh local store index
sudo apt install sublime-text  # Install software
12. System Logging & Monitoring (/var/log Architecture)
Service	Log File Location	What it tracks
Apache2	/var/log/apache2/access.log	Inbound visitor IPs, timestamps, and requested pages.
Fail2Ban	/var/log/fail2ban.log	Brute-force guessing attempts and banned IPs.
UFW	/var/log/ufw.log	Blocked and allowed network connections.
Auth Logs	/var/log/auth.log	User logins, failed attempts, and sudo history.
System Engineering Pro-Tip: Never use cat for logs as it can freeze your terminal buffer. Always use the less command because it loads text files page-by-page and can natively read compressed .gz log files without unzipping them first.
