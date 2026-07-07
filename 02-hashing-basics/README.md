# Praxis-Projekt: Hashing-Grundlagen & Passwort-Analyse

## Projekt-Übersicht
Dieses Projekt dokumentiert die erfolgreiche Durchführung des Moduls **"Hashing-Basics"** aus dem TryHackMe *Cybersecurity 101* Pfad. Im Fokus stand der praktische Umgang mit kryptographischen Einwegfunktionen (Hashes), das strukturierte Knacken von Passwort-Hashes mittels Brute-Force/Wortlisten-Angriffen sowie die Unterscheidung zwischen Verschlüsselung, Hashing und Codierung.

## Angewandte Werkzeuge & Frameworks
* **Hashcat (v6.2.6):** Advanced Password Recovery Utility
* **Linux Terminal (Bash):** Zur Datenmanipulation und Pipeline-Verarbeitung (`echo`, `pipe`, `base64`)
* **RockYou Wordlist:** Standard-Wortliste für Brute-Force-Analysen

---

## Praktische Fallstudien & Lösungswege

### 1. Identifikation und Knacken von MD5-Hashes
* **Herausforderung:** Ein unbekannter 32-Zeichen-Hex-Hash (`b6b0d451bbf6fed658659a9e7e5598fe`) musste analysiert und im Klartext wiederhergestellt werden.
* **Analyse:** Aufgrund der Länge und des Formats wurde der Typ als **MD5** identifiziert (Hashcat-Modus `-m 0`).
* **Befehl:**
  ```bash
  hashcat -m 0 -a 0 /Hashing-Basics/Task-6/hash4.txt /usr/share/wordlists/rockyou.txt
  ```
* **Ergebnis:** Der Hash wurde erfolgreich als Klartext **`funforyou`** enttarnt.

### 2. Fortgeschrittenes Cracking: HMAC-SHA512
* **Herausforderung:** Analyse eines komplexeren Hashes vom Typ **HMAC-SHA512 (key = $pass)**.
* **Lösung:** Für dieses spezifische Format wurde der Hashcat-Modus **`17500`** gewählt. Hierbei wurde besonders auf das korrekte Dateiformat (`[Hash]:[Salt/Key]`) geachtet, um Fehler beim Einlesen des Trennzeichens (*Separator unmatched*) zu verhindern.
* **Befehl:**
  ```bash
  hashcat -m 17500 -a 0 /Hashing-Basics/Task-6/hash_hmac.txt /usr/share/wordlists/rockyou.txt
  ```

### 3. Dekodierung von Base64 (Abgrenzung zur Verschlüsselung)
* **Herausforderung:** Der String `RU5jb2RlREVjb2RlCg==` sollte lesbar gemacht werden.
* **Lösung:** Im Gegensatz zu Hashes handelt es sich bei Base64 um eine reine Daten-Kodierung. Es wurde direkt die Linux-eigene Pipeline genutzt, um die Daten ohne Passwort im Terminal zu dekodieren.
* **Befehl:**
  ```bash
  echo "RU5jb2RlREVjb2RlCg==" | base64 -d
  ```
* **Ergebnis:** Klartext **`ENcodeDEcode`**

---

## Wichtige forensische Erkenntnisse

1. **Hashing ist keine Verschlüsselung:** Hashes sind mathematische Einwegfunktionen. Ein Zurückrechnen ist unmöglich. Die Wiederherstellung gelingt rein defensiv über den Abgleich von vorberechneten Wortlisten (Brute-Force).
2. **Kodierung bietet keinen Schutz:** Base64 dient lediglich der Formatierung von Daten (z. B. um Binärdaten in Textform zu übertragen). Da kein Schlüssel benötigt wird, kann jeder Angreifer Base64-Daten mit einem einzigen Terminal-Befehl sofort im Klartext mitlesen.
3. **Fehlersuche in Hashcat:** Fehlermeldungen wie *Separator unmatched* weisen präzise auf syntaktische Fehler in der Input-Datei hin. In der Cyber-Forensik ist die genaue Einhaltung von Datenformaten essenziell.

---
*Dieses Projekt ist Teil meiner praktischen Vorbereitung auf den Quereinstieg als Fachinformatiker für Systemintegration mit Spezialisierung auf Cyber-Forensik.*
