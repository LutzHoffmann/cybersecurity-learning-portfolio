# 🔒 Cybersecurity Learning Portfolio

Mein praktisches Portfolio begleitend zur Umschulung und dem **TryHackMe Cybersecurity 101 Pfad**. Dieses Repository dient als Nachweis meiner praktischen Fähigkeiten in den Bereichen Offensive Security, Netzwerkanalyse und Automatisierung.

---

## 🧭 Inhaltsverzeichnis (Abgeschlossene Räume)

Hier dokumentiere ich meine Fortschritte und praktischen Umsetzungen. Jeder Raum ist in einem eigenen Ordner detailliert mit Befehlen, Methodiken und Skripten dokumentiert:

### 🔐 Kryptographie & Hashing
*   **[Asymmetrische Verschlüsselung mit OpenSSL](./01-kryptographie/)**
    *   *Fokus:* Public-Key-Kryptographie – Erzeugen eines RSA-2048-Schlüsselpaars, Ver-/Entschlüsselung mit OpenSSL und Bezug zur Ransomware- und TLS-Analyse.
*   **[Hashing-Grundlagen & Passwort-Analyse](./02-hashing-basics/)**
    *   *Fokus:* Kryptographische Einwegfunktionen, Cracking von MD5- und HMAC-SHA512-Hashes mit Hashcat (RockYou) sowie Abgrenzung von Hashing, Verschlüsselung und Base64-Kodierung.

### 🛠️ Tool- & Passwort-Sicherheit
*   **[John the Ripper (JTR) - Grundlagen](./03-john-the-ripper-toolbox/)**
    *   *Fokus:* Cracking von Linux-Systemhashes (`/etc/shadow`), Archiven (ZIP/RAR) und SSH-Schlüsseln.
    *   *Highlight:* Eigenes Bash-Automatisierungsskript zur Hash-Extraktion.

### 🌐 Netzwerk- & Exploit-Analyse
*   **[Moniker Link (CVE-2024-21413)](./CVE-2024-21413-MonikerLink/)**
    *   *Fokus:* Ausnutzung einer kritischen Outlook-Schwachstelle, Beheben von Port-Konflikten (Port 445) und Abfangen von NetNTLMv2-Hashes via `Responder`.

### 🛡️ Exploit Frameworks
*   **[Metasploit: Einführung](./Metasploit-Einfuehrung/)**
    *   *Fokus:* Architektur des Frameworks (Exploits, Payloads, Auxiliary), Grundlagen der `msfconsole` und Modul-Konfiguration für zielgerichtete Angriffe.
*   **[Metasploit: Exploitation](./Metasploit-Exploitation/)**
    *   *Fokus:* Kompletter Exploitation-Workflow – MSF-Datenbank & Workspaces, Scanning mit Auxiliary-Modulen, Ausnutzen verwundbarer Dienste sowie Post-Exploitation mit Meterpreter (`getsystem`, `hashdump`, `migrate`).
*   **[Metasploit: Meterpreter](./Metasploit-Meterpreter/)**
    *   *Fokus:* Tiefer Einstieg in Meterpreter – In-Memory-Payload & verschlüsselte C2-Kommunikation, Command-Kategorien (Core, File System, Networking, System), Prozess-Migration sowie Credential-Harvesting mit `hashdump` und Kiwi/Mimikatz.

### 🚩 Praktische Angriffs-Challenges (CTF)
*   **[Blue (EternalBlue / MS17-010)](./Blue-EternalBlue/)**
    *   *Fokus:* Vollständige Kompromittierung einer Windows-Box – Recon mit Nmap, Ausnutzung von MS17-010 (SYSTEM-Zugriff), Session-Upgrade zu Meterpreter (`shell_to_meterpreter`, `migrate`), Hash-Dump und Offline-Cracking mit John the Ripper. 🏅 *Badge erhalten.*
*   **[Basic Pentesting](./Basic-Pentesting/)**
    *   *Fokus:* Enumeration einer Linux-Box (Nmap, Gobuster, enum4linux, SMB), SSH-Brute-Force mit Hydra sowie User-Pivoting durch Cracken einer SSH-Key-Passphrase (`ssh2john` + John).

### 🕸️ Web Hacking
*   **[Web Application Basics](./Web-Application-Basics/)**
    *   *Fokus:* Grundlagen der Web-Sicherheit – Aufbau von URLs, HTTP-Requests/Responses, Methoden, Status-Codes und Header sowie die Trennung von Front End und Back End (DevTools, `curl`).


---

## 🛠️ Tech Stack & Tools

Im Rahmen des Pfads und meiner Umschulung verwende ich aktiv folgende Tools:
*   **Betriebssysteme:** Kali Linux, macOS (Terminal), Windows Server (AD-Umgebungen)
*   **Netzwerk & Analyse:** Responder, Wireshark
*   **Cracking & Krypto:** John the Ripper (JTR), Hashcat
*   **Automatisierung:** Bash-Scripting, Python


---
*Hinweis: Alle Labore und Exploits wurden in isolierten, legalen Testumgebungen von TryHackMe durchgeführt.*

