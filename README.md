# 🔒 Cybersecurity Learning Portfolio

Mein praktisches Portfolio begleitend zur Umschulung und dem **TryHackMe Cybersecurity 101 Pfad**. Dieses Repository dient als Nachweis meiner praktischen Fähigkeiten in den Bereichen Offensive Security, Netzwerkanalyse und Automatisierung.

---

## 🧭 Inhaltsverzeichnis (Abgeschlossene Räume)

Hier dokumentiere ich meine Fortschritte und praktischen Umsetzungen. Jeder Raum ist in einem eigenen Ordner detailliert mit Befehlen, Methodiken und Skripten dokumentiert:

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


---

## 🛠️ Tech Stack & Tools

Im Rahmen des Pfads und meiner Umschulung verwende ich aktiv folgende Tools:
*   **Betriebssysteme:** Kali Linux, macOS (Terminal), Windows Server (AD-Umgebungen)
*   **Netzwerk & Analyse:** Responder, Wireshark
*   **Cracking & Krypto:** John the Ripper (JTR), Hashcat
*   **Automatisierung:** Bash-Scripting, Python


---
*Hinweis: Alle Labore und Exploits wurden in isolierten, legalen Testumgebungen von TryHackMe durchgeführt.*

