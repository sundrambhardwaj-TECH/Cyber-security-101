# Windows Fundamentals - Part 1

Comprehensive study notes covering the core concepts of the Windows Operating System, GUI components, file systems, user account management, access controls, and basic troubleshooting tools.

---

## 1. History & Evolution of Windows

*   **Dominance:** Introduced in **1985**, Microsoft Windows remains the dominant operating system for both consumer desktops and enterprise networks.
*   **The OS Cycle (Hits vs. Misses):**
    *   **Windows XP:** Highly successful, stable, and long-lived.
    *   **Windows Vista:** A complete overhaul that suffered from major compatibility and performance issues; quickly phased out.
    *   **Windows 7:** Released as a stable successor to Vista. The End-of-Life (EOL) migration from XP to 7 caused massive infrastructure scrambles for corporations and hospitals.
    *   **Windows 8.x:** Short-lived and poorly received due to radical UI changes aimed at touchscreens.
    *   **Windows 10 & 11:** Modern standards. Windows 11 comes in two primary consumer flavors: **Home** and **Pro**.
*   **Windows Server:** The dedicated enterprise server edition, with **Windows Server 2025** being the current modern standard (older enterprise environments often still run legacy versions like Server 2019/2022).

---

## 2. Windows Graphical User Interface (GUI)

The Windows Desktop environment greets users immediately after passing the secure login screen (where local or Active Directory credentials are validated).

### Core GUI Components:
*   **The Desktop:** The main workspace for quick-access shortcuts, folders, and files. 
    *   *Display Settings:* Adjust screen resolution, orientation, and multi-monitor setups. (Note: Often disabled or limited during Remote Desktop/VM sessions).
    *   *Personalize:* Modify background wallpapers, themes, and color schemes.
*   **Start Menu:** The centralized launcher for applications, divided into three structural zones:
    1.  *Left Sidebar:* Quick shortcuts for User Account management, Documents, Pictures, Settings (Gear icon), and Power controls.
    2.  *App List:* An alphabetical directory of all installed applications. Clicking a letter header brings up an alphabet grid for fast navigation.
    3.  *Tiles Section:* The right pane where frequently used programs can be customized and pinned as responsive tiles.
*   **Taskbar:** Displays currently active or explicitly pinned applications. Hovering over icons provides thumbnail previews and tooltips.
*   **Notification Area (System Tray):** Located at the bottom right; hosts system essentials like Date/Time, Volume mixer, Network/Wi-Fi status, and background app indicators.

---

## 3. The NTFS File System

Modern versions of Windows rely exclusively on the **New Technology File System (NTFS)** for internal storage drives, replacing older file systems like FAT16, FAT32, and HPFS.

### FAT32 vs. NTFS Comparison

| Feature | FAT32 | NTFS |
| :--- | :--- | :--- |
| **Primary Use Cases** | USB Flash Drives, MicroSD cards | Windows System Drives ($C:\$), Servers |
| **Max File Size** | Limited to **4 GB** | Practically unlimited ($16\text{ TB}$) |
| **Fault Tolerance** | Low (prone to corruption on crash) | High (**Journaling file system** repairs itself via log files) |
| **Security Features** | None | Folder/File permissions & **EFS Encryption** |

### NTFS Permissions Matrix
Access control is managed via the `Properties -> Security` tab of any file or folder:
*   **Full Control:** Modify, read, write, delete, and alter security permissions.
*   **Modify:** Read, write, and delete files, but cannot change ownership/permissions.
*   **Read & Execute:** View files and run executable applications or scripts.
*   **List Folder Contents:** View the names of files within a directory without accessing file content.
*   **Read:** View or open the content of a file.
*   **Write:** Edit the contents of a file or add new files to a folder.

### Alternate Data Streams (ADS)
*   **Definition:** An NTFS file attribute that allows files to contain more than one stream of data. Every standard file has a default `$DATA` stream, but additional hidden streams can be attached.
*   **Visibility:** Natively invisible inside Windows Explorer. Requires PowerShell or specialized tools to detect.
*   **Use Cases:**
    *   *Non-malicious:* Windows uses it to append a `Zone.Identifier` tag to files downloaded from the internet to trigger security warnings.
    *   *Malicious:* Frequently abused by malware authors to hide malicious code or binaries behind legitimate files without altering their visible file size.

---

## 4. Crucial System Folders & Environment Variables

### The Windows Directory (`%windir%`)
*   Traditionally located at `C:\Windows`, this directory contains the core operating system architecture.
*   **Environment Variables:** System shortcuts used by the OS to reference paths dynamically. For instance, entering `%windir%` into the Run dialog (`Win + R`) automatically opens the active Windows installation folder, regardless of its host drive letter.

### The `System32` Folder
*   **Path:** `C:\Windows\System32`
*   **Significance:** The absolute brain of the OS. Contains critical `.dll` (Dynamic Link Libraries) and system executables (`.exe`).
*   **Warning:** Modifying or deleting files inside `System32` can break the operating system entirely and cause catastrophic boot failures. Most native Windows administration and troubleshooting utilities (like `cmd.exe`, `taskmgr.exe`) are located here.

---

## 5. User Account & Access Management

Windows segregates authority on a local machine using distinct user types and administrative groups.

*   **Administrator:** Complete system privileges. Can install software, create/delete users, alter system settings, and modify core system files.
*   **Standard User:** Restricted privileges. Can only modify files within their own user profile directory. Cannot make system-wide changes or install global applications.
*   **User Profiles (`C:\Users`):** Triggered by the *User Profile Service* on initial login. Generates a isolated environment folder structure (e.g., `C:\Users\Username`) for every account, providing distinct Desktops, Documents, and Downloads paths.

### Local Users and Groups Manager (`lusrmgr.msc`)
A powerful administrative snap-in accessed via the Run dialog.
*   **Users:** View all active, disabled, or built-in system accounts.
*   **Groups:** View collections of privileges. Rather than assigning permissions individually, administrators place users into groups (e.g., the *Administrators Group*). The user automatically **inherits** the complete permissions assigned to that group.

---

## 6. User Account Control (UAC)

Introduced in Windows Vista to counter the inherent risks of users running tasks with constant administrative privileges.

*   **How it Works:** Even when logged into an Administrator account, standard daily processes run in a non-elevated context. When a task requires elevated system-level access, UAC halts the action and prompts for confirmation.
*   **The Shield Indicator:** Programs requiring elevated privileges display a distinct shield icon over their native shortcut graphics.
*   **Behavioral Differences:**
    *   *On an Admin Account:* Prompts the user with a simple "Yes/No" dialog box to temporarily elevate execution privileges.
    *   *On a Standard User Account:* Prompts for an explicit **Administrator username and password**. Failure to provide valid admin credentials results in immediate termination of the execution request.
*   **Security Value:** Serves as a critical defense layer against unauthorized background software installations or silent malware execution. *(Note: By default, UAC does not apply to the built-in local Administrator account).*

---

## 7. Configuration Tools: Settings vs. Control Panel

Windows splits its configuration architecture across two key utilities, which often interlink dynamically.

*   **Settings Menu:** The modern, touch-friendly UI introduced in Windows 8/10. Handles routine user-focused adjustments like display personalization, basic networking, and update management.
*   **Control Panel:** The traditional administrative hub. Reserved for deep system modifications, hardware drivers, and complex networking. Clicking an advanced link within Settings (such as *Change Adapter Options*) will frequently route the user directly into a classic Control Panel window.
*   **Programs and Features (`Control Panel -> Programs -> Programs and Features`):** The definitive inventory check for a system administrator or security analyst. Lists every globally installed application alongside its **Name**, **Publisher**, and **Version** to easily audit and uninstall unauthorized software or potential malware.

---

## 8. Resource Monitoring via Task Manager

The primary application for real-time monitoring and process troubleshooting, accessible via the shortcut **`Ctrl + Shift + Esc`**.

*   **Simple View:** Displays a basic list of active, user-facing applications with direct "End Task" functionality for frozen windows.
*   **More Details View:** Expands into a robust system diagnostic utility:
    *   *Processes Tab:* Displays resource consumption (CPU, Memory, Disk, Network) across individual foreground applications and hidden background Windows services. Crucial for identifying anomalous files or resource-hijacking malware.
    *   *Performance Tab:* Provides interactive, real-time telemetry graphs indicating raw hardware utilization limits.
