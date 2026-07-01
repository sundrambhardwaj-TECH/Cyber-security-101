# 🐧 My Linux Fundamentals Journey

I have started learning Linux fundamentals, and this repository is my personal log. I have documented everything I learned today—history, architecture, commands, and operators—all compiled directly into this single master sheet.

---

## 🏛️ Linux Core Fundamentals, Commands & Operators Master-Log

### 1. The Core Architecture (Unix, Linux & Kernels)
* **The Unix Ancestry:** Developed in 1970 at AT&T's Bell Labs, Unix is the "ancestor" of modern OS platforms like Linux and macOS. It is a proprietary, closed-source system.
* **The Linux Reality:** Linux is NOT a complete Operating System; it is technically a **Kernel** (the core engine). First released by **Linus Torvalds** on **September 17, 1991**, it is open-source, fast, and secure because bugs get patched by the global community within hours.
* **Distributions (Distros):** A distribution is a full OS built by putting software tools on top of the Linux Kernel. Examples include **Ubuntu** (super lightweight, runs on just **512MB RAM**) and **Kali Linux** (pre-packed with ethical hacking tools).
* **Linux vs Windows Kernels:** Linux uses a **Monolithic Kernel** where hardware drivers and core tasks run inside the kernel space (extremely fast). Windows uses a closed-source **NT (Hybrid) Kernel** which splits tasks between user and kernel modes, making it heavier and more resource-intensive.

### 2. Complete CLI Cheat-Sheet (Navigation, Search, Redirection & Operators)
Here is the entire breakdown of every command and operator I practiced, compiled together into a single execution guide:

```bash
# ==========================================
# PART A: DIRECTORY NAVIGATION & BASIC CLI
# ==========================================

# Print Working Directory: Tells me exactly which folder I am standing in right now.
pwd
# Output example: /home/user/Documents

# List: Displays all files and folders in the current directory.
ls
ls -la        # The '-la' flag reveals hidden files along with detailed permissions.

# Change Directory: Used to jump between folders.
cd Documents  # Moves into the Documents directory.
cd ..         # Moves one step backward to the parent directory.
cd ~          # Takes me straight back to the user's Home directory.

# Concatenate: Outputs the text content of a file directly onto the terminal screen.
cat notes.txt


# ==========================================
# PART B: ADVANCED SEARCHING & COUNTING
# ==========================================

# Find: Used specifically to locate a file or directory by its NAME.
find . -name "my_file.txt"     # Searches the current folder ('.') and all sub-folders.

# Grep: Used specifically to search for a string of TEXT INSIDE a file's content.
grep "error" server.log        # Prints every line containing the word "error" inside server.log.

# Recursive Grep: Automatically crawls through a main folder, its sub-folders, and scans every single file.
grep -r "todo" /home/projects/ # Checks all project files recursively for the text "todo".

# Word Count (with Piping): Uses the pipe (|) operator to send cat's output into wc to count data.
cat notes.txt | wc -l          # Counts and prints the total number of lines in the file.
cat notes.txt | wc -w          # Counts and prints the total number of words in the file.


# ==========================================
# PART C: OPERATORS, REDIRECTION & TRICKS
# ==========================================

# Background Execution (&): Runs a heavy or time-consuming task in the background, keeping the CLI free.
sleep 100 &

# Logical AND (&&): Conditional execution. Command 2 runs ONLY IF Command 1 completes successfully.
mkdir test_folder && cd test_folder

# Overwrite Redirection (>): Sends output to a file, completely wiping out its existing content first.
echo "sam" > file1.txt

# Append Redirection (>>): Sends output to a file, adding the text to the bottom without touching existing data.
echo "ram" >> file1.txt

# Stream Editor (sed) Trick: Finds a specific string and replaces it inline inside the file.
sed -i 's/sam/ram/g' file1.txt  # Changes every instance of "sam" to "ram" inside file1.txt.

# Tee Command Trick: Pipes data and writes it to multiple files simultaneously without overwriting them.
echo "sam" | tee -a file1.txt file2.txt  # Appends "sam" to both file1 and file2 at the exact same time.
