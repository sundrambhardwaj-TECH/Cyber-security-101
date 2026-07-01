# Cyber Security 101: My Learning Journal 🚀

Welcome to my repository! I have started my journey in Cyber Security. I will be documenting my daily learnings and practical insights here.
---
## Module 1: Search Skills (Reconnaissance)

In this module, I learned how information gathering and OSINT (Open Source Intelligence) work, and how professionals research vulnerabilities using different tools.

### 1. Shodan
* **Concept:** Unlike Google which searches web content, Shodan scans the internet for connected devices (servers, routers, IoT, etc.). 
* **My Take:** I have personally used Shodan before and explored how easily accessible live, unsecured cameras can be found using specific queries. While learning platforms like TryHackMe show limited/controlled results for safety, the real-world data on Shodan is vast and powerful.

### 2. VirusTotal
* **Concept:** It is not a single antivirus, but an aggregator that combines around 70+ top antivirus engines and URL scanners.
* **Why it matters:** If we encounter a suspicious file or link, we can analyze it here. In a real security environment, searching for a file's **Hash Value** (digital fingerprint) on VirusTotal helps identify malware families quickly.

### 3. CVE & CVSS (Vulnerability Databases)
* **Concept:** **CVE** acts as a universal dictionary for security flaws, giving each a unique ID (CVE-Year-Number). **CVSS** is the scoring system (0 to 10) that tells us how risky a vulnerability is based on its impact and complexity.
* **Important Insight (Dynamic Risk):** A great question arises: *What if a low-scored vulnerability is later exploited more effectively by a hacker?* I learned that CVSS scores are **not fixed**. If a new exploit is discovered, or if hackers combine multiple low flaws together (**Vulnerability Chaining**), security bodies re-evaluate and upgrade the risk score.

### 4. Linux `man` Command
* **Concept:** The `man` (Manual) tool is the built-in user manual in Linux. 
* **Usage:** Typing `man <command>` (like `man ls`) displays the complete documentation and flags for that specific command.
* **Quick Tip:** Press `q` to exit the manual interface.

---
*Documented by me as part of my continuous learning path.*
