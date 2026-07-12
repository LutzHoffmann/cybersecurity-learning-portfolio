{\rtf1\ansi\ansicpg1252\cocoartf2870
\cocoatextscaling0\cocoaplatform0{\fonttbl\f0\fswiss\fcharset0 Helvetica;}
{\colortbl;\red255\green255\blue255;}
{\*\expandedcolortbl;;}
\paperw11900\paperh16840\margl1440\margr1440\vieww11520\viewh8400\viewkind0
\pard\tx720\tx1440\tx2160\tx2880\tx3600\tx4320\tx5040\tx5760\tx6480\tx7200\tx7920\tx8640\pardirnatural\partightenfactor0

\f0\fs24 \cf0 # John the Ripper (JTR) Automation & Practical Lab Notes\
\
A professional toolkit and automated helper script developed during the practical completion of the **John the Ripper** modules on TryHackMe. This repository showcases automation skills in password auditing, hash extraction, and credential recovery.\
\
---\
\
## \uc0\u55357 \u57056 \u65039  Features & Contents\
\
1. **`jtr-automator.sh`**: A custom Bash script that automatically detects target file types (SSH Keys, ZIPs, RARs), extracts their hashes via the correct `*2john` dependency, and feeds them into JTR.\
2. **Comprehensive Cheat Sheet**: A rapid-reference guide for Linux shadowing, standard formats, and post-exploitation viewing.\
\
## \uc0\u55357 \u56960  Getting Started with the Automator Script\
\
### Prerequisites\
Make sure `john` (John the Ripper) and its utility tools are installed (default on Kali Linux).\
\
### Usage\
\
Clone the repository and make the script executable:\
```bash\
git clone https://github.com\
cd john-the-ripper-toolbox/scripts\
chmod +x jtr-automator.sh\
```\
\
Run the automation tool against an encrypted asset:\
```bash\
# General Syntax\
./jtr-automator.sh [mode] [target_file] [optional_wordlist_path]\
\
# Example: Crack an encrypted SSH Private Key (id_rsa)\
./jtr-automator.sh ssh id_rsa\
\
# Example: Crack a password-protected ZIP archive using a custom wordlist\
./jtr-automator.sh zip confidential.zip /usr/share/wordlists/rockyou.txt\
```\
\
---\
\
## \uc0\u55357 \u56541  Core Concepts Covered (Cheat Sheet)\
\
### 1. Linux Credential Auditing (`/etc/shadow`)\
Combining standard Linux authentication files before cracking.\
```bash\
unshadow /etc/passwd /etc/shadow > unshadowed_hashes.txt\
john --wordlist=/usr/share/wordlists/rockyou.txt unshadowed_hashes.txt\
```\
\
### 2. Manual Hash Extraction & Cracking Reference\
If you prefer running commands manually instead of using the script:\
\
| Asset Type | Extraction Command | Cracking Command |\
| :--- | :--- | :--- |\
| **SSH Key** | `python3 ssh2john.py id_rsa > hash.txt` | `john --wordlist=rockyou.txt hash.txt` |\
| **ZIP File** | `zip2john file.zip > hash.txt` | `john --wordlist=rockyou.txt hash.txt` |\
| **RAR File** | `rar2john file.rar > hash.txt` | `john --wordlist=rockyou.txt hash.txt` |\
\
### 3. Verification (Viewing Results)\
To display successfully cracked credentials cleanly from the pot file without rerunning the attack:\
```bash\
john --show extracted_hash.txt\
```\
\
---\
\
## \uc0\u55356 \u57235  Certification & Context\
This project was built to internalize and practicalize offensive security concepts taught in the **TryHackMe JTR Learning Path**. \
\
* **Topics covered:** Mutation rules, custom hash formats, single-crack mode, and asymmetric key cracking.\
\
---\
*Disclaimer: This repository is created strictly for educational purposes, authorized penetration testing, and defensive security auditing. Never use these tools on systems you do not own or do not have explicit written permission to test.*\
}