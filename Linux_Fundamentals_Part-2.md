# Linux Fundamentals - Part 2 Notes 🐧

Welcome to Part 2 of my Linux learning journey. This section covers Remote Access, Flags, Advanced File Management, User Permissions, and the Linux Directory Structure.

---

## 1. Remote Access & Help Commands 🌐
*   **SSH (Secure Shell):** Used to securely connect and control a remote Linux machine over a network using encryption (Port 22).
    ```bash
    ssh username@remote_ip
    ```
*   **Flags / Switches:** Arguments passed to commands to change their default behavior.
    *   `ls` (Normal list) vs `ls -la` (Long listing, including hidden files).
*   **Getting Help:**
    *   `command --help` - Quick summary of flags and usage directly in the terminal.
    *   `man command` - Opens the complete, detailed manual page using the `less` pager.
    *   *Navigation inside manual pages:* **Down Arrow** (Line down), **Spacebar** (Page down), **q** (Quit).

---

## 2. File & Directory Management 📁
*   **`mkdir`**: Creates a new directory/folder.
*   **`touch`**: Creates a blank file or updates timestamps.
*   **`file`**: Determines the actual file type, looking past the extension.
*   **`find`**: Searches for files and directories based on names, size, or permissions.
    ```bash
    find . -name "notes.txt"
    ```
*   **`cp` & `mv`**: For copying and moving/renaming. Can handle multiple files or use wildcards (`*`).
    ```bash
    # Moving multiple specific files to a destination
    mv file1.txt file2.txt /destination_path/
    
    # Copying all text files using a wildcard
    cp *.txt /destination_path/
    ```
*   **`rm`**: Permanently deletes files. Use `rm -r` for folders. *Warning: No Recycle Bin in the CLI!*

---

## 3. Linux User & File Permissions 🔒

### User Switch (`su`)
*   `su [user]`: Switches user but retains the current environment.
*   `su -l [user]`: Launches a clean login shell with the target user's environment.
*   *Note:* If you lack permissions, you might see the infamous `"This incident will be reported"` warning!

### UGO & Permissions
Permissions are divided into three categories: **User (Owner), Group, and Other (World)**.
A standard permission block looks like: `- rwx r-x r--` (Read as 3-3-3 chunks).

### Numeric Conversion (Octal Code)
*   `r` (Read) = **4**
*   `w` (Write) = **2**
*   `x` (Execute) = **1**
*   `-` (None) = **0**

#### Examples:
*   `rwxr-xr-x` ➔ $(4+2+1), (4+0+1), (4+0+1)$ ➔ **755**
*   `rwxr--r--` ➔ $(4+2+1), (4+0+0), (4+0+0)$ ➔ **744**
*   `rw-r-----` ➔ $(4+2+0), (4+0+0), (4+0+0)$ ➔ **640**

Command to change permission: `chmod 640 secret.txt`

---

## 4. System Directory Structure (FHS) 🏛️

| Directory | Purpose | Access Level (Normal User) |
| :--- | :--- | :--- |
| **`/root`** | Home directory for the system Administrator (Root). | ✗ **Permission Denied** |
| **`/etc`** | Stores system configuration and network settings. | ✓ Read-only |
| **`/var`** | Stores variable data like system logs (`/var/log`). | ✓ Read logs |
| **`/tmp`** | Stores temporary files. Wiped automatically on reboot. | ✓ Full access to create/edit |

---
*Notes compiled during practice on TryHackMe.*
