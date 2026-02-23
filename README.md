# my-portfolio
# Hi, I'm Don Achema 👋

## 🛡 About Me
I am a cybersecurity analyst focused on threat detection, network security, and automation.

## 🔧 Skills
- SIEM (Splunk, Wazuh)
- Python scripting
- Linux administration
- Network security
- Incident response

## 📂 Projects
- [SIEM Home Lab](link)
- [Python Port Scanner](link)
- [Log Analysis Automation](link)

## 📫 Contact
Email: donatusachema@gmail.com
LinkedIn: www.linkedin.com/in/egwu-donatus-achema-8a9251378
🔹 3. What Projects Should You Post?

Since you're in cybersecurity, here are strong project ideas:

## 🔐 1. Home Lab Documentation

## Setting-up cybersecurity-home-lab

## Step 1: Install VirtualBox

Go to https://www.virtualbox.org
Download the latest VirtualBox for your host OS (Windows, macOS, or Linux).
Download and install the Extension Pack (same page, needed for better USB/network support).
Install both.

## Step 2: Download the Virtual Machine Images
We will use:

Kali Linux (attacker machine) — pre-built VirtualBox image (easiest)
Metasploitable 2 (intentionally vulnerable target) — classic, lots of vulnerabilities for scanning practice

Downloads:

Kali Linux VirtualBox image:
Go to https://www.kali.org/get-kali/
Scroll to “Virtual Machines” section
Download the VirtualBox image (usually a .7z or .ova file, ~3–4 GB)
Default credentials: kali/kali

Metasploitable 2:
Go to https://sourceforge.net/projects/metasploitable/files/Metasploitable2/
Download metasploitable-linux-2.0.0.zip (~800 MB)
Extract the zip — inside you’ll find a folder with Metasploitable.vmdk (the virtual disk)
Default credentials: msfadmin/msfadmin


## Step 3: Import and Configure the VMs in VirtualBox
Import Kali:

Open VirtualBox → File → Import Appliance
Select the downloaded .ova file for Kali
Accept defaults or adjust RAM (allocate 2–4 GB) and CPU (2 cores)
Finish import

Create Metasploitable 2 VM:

In VirtualBox → New
Name: Metasploitable2
Type: Linux → Version: Ubuntu (64-bit)
RAM: 2 GB recommended
Hard disk: Use an existing virtual hard disk file → browse to the extracted Metasploitable.vmdk
Finish

Network Configuration (Important for isolation and communication):

In VirtualBox → File → Host Network Manager → Create a host-only network (e.g., vboxnet0). This isolates the lab from your real network.
For both VMs:
Settings → Network → Adapter 1
Enable Adapter
Attached to: Host-only Adapter
Name: select the one you created (vboxnet0)

## The Attacks Tested are as Follows:
I tested/discovered potential attack surfaces by:

## 1. Host discovery (finding live hosts in the lab network)
→ Using tools like arp-scan, netdiscover, and nmap -sn — this is reconnaissance, not an attack.
## 2. Port scanning and service enumeration
→ Commands like:
nmap -sV --top-ports 1000 <TARGET_IP>
nmap -A <TARGET_IP>
nmap -sC -sV <TARGET_IP>
→ This revealed open ports and running services/versions on Metasploitable 2, such as:
Port 21/tcp → vsftpd 2.3.4 (backdoor vulnerability, CVE-2011-2523)
Port 22/tcp → OpenSSH 4.7p1
Port 80/tcp → Apache httpd 2.2.8 (with DAV/2, multiple known issues)
Port 139/445/tcp → Samba smbd 3.X–4.X (e.g., username map script command execution, CVE-2007-2447)
And many others (e.g., Telnet on 23, UnrealIRCd on 6667 with backdoor, ProFTPD on 2121, etc.)
These scans identify exploitable services but do not exploit them — they simulate what an attacker would do in the reconnaissance phase.
## 3. Vulnerability scanning
→ Using Nessus Essentials (or Greenbone/OpenVAS alternative)
→ This produced a report highlighting known vulnerabilities with CVSS scores, such as:
Critical: vsftpd 2.3.4 backdoor (CVSS 10.0) — allows unauthenticated root shell if triggered
High/Critical: Samba issues (e.g., potential remote code execution, symlink traversal)
High: Apache-related directory traversal, info disclosure
Others: Outdated software, weak configs, exposed services

## Lessons to learn from this are:
Here are the key lessons we can draw from it:
1. Outdated Software Is One of the Biggest Attack Vectors

Metasploitable 2 runs ancient versions (e.g., vsftpd 2.3.4 from 2011, Samba 3.x, Apache 2.2.8, OpenSSH 4.7p1).
Lesson: Patch management is non-negotiable. Systems that aren't regularly updated become low-hanging fruit. In production, implement automated patching, version inventories, and end-of-life retirement policies.

2. Default / Weak Credentials Enable Rapid Compromise

The primary user is msfadmin:msfadmin (username = password).
Many services allow easy brute-force or credential stuffing.
Lesson: Enforce strong, unique passwords everywhere. Disable or rename default accounts. Use credential management tools, MFA where possible, and monitor for brute-force attempts (fail2ban, account lockouts).

3. Vulnerability Scanners Are Essential but Require Interpretation

Nessus flagged hundreds of issues (often 300–400+), with clear CVSS scores, exploitability info, and remediation steps.
Many were critical (CVSS 9–10), but some were noise (false positives or low-impact in context).
Lesson: Scanning alone isn't enough — prioritize findings (exploitability + business impact), validate manually when needed, and track remediation over time. Integrate scanners into continuous monitoring (e.g., feed into SIEM like Wazuh/Security Onion in a later project).

4. Reconnaissance Is the Foundation of Almost Every Attack

Simple Nmap scans (-sV -O -sC -A) revealed service versions, OS guess, and even some script-detected vulns.
Attackers rarely jump straight to exploitation — they start with footprinting just like we did.
Lesson: Blue teams must assume attackers are doing the same scans. Run your own periodic external/internal scans to see what an adversary sees. Harden against fingerprinting (e.g., obscure banners, disable unnecessary version info).

5. Isolation and Safe Practice Are Non-Negotiable

We used host-only networking in VirtualBox — zero risk to real networks.
Lesson: Never test on production, shared, or internet-facing systems without explicit permission. Use labs like this (or TryHackMe, HackTheBox) to build muscle memory safely.










How you set up Kali Linux

Metasploitable lab

VirtualBox setup

Screenshots

What attacks you tested

Lessons learned

Recruiters LOVE this.

🐍 2. Python Security Tools

Examples:

Port scanner

Password strength checker

Log analyzer

Brute-force simulation (educational)

Structure:

project-folder/
│
├── main.py
├── README.md
└── requirements.txt

Your README should explain:

What it does

How to run it

Screenshot of output

🌐 3. Networking Projects

Example repos:

network-scanner

packet-analysis

firewall-config-lab

Explain:

The problem

The tool used (e.g., Nmap, Wireshark)

Output screenshots

What you discovered

🔹 4. How to Write a Strong Project README

Use this format:

# Project Name

## 📌 Description
Brief explanation of what this project does.

## ⚙ Tools Used
- Python
- Nmap
- Wireshark

## 🚀 How to Run
Step-by-step instructions.

## 📊 Sample Output
(screenshot here)

## 🎯 What I Learned
Explain what this project taught you.
