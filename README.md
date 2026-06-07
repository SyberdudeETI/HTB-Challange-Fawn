# HTB-Challange-Fawn
Level: Easy


📋 Protokoll: FTP Enumeration & Exploitation (HTB Fawn)
1. Phase: Scanning & Reconnaissance (Erkundung)
    • Was du getan hast: Du hast Nmap genutzt, um den Zielserver zu scannen.
    • Wichtige Befehle: nmap -sV <IP> (Versionserkennung) und nmap -p 21 <IP> (Port-Check).
    • Ergebnis: Du hast herausgefunden, dass Port 21 offen ist und welche FTP-Software (z. B. vsftpd 3.0.3) läuft.
2. Phase: Enumeration (Dienst-Analyse)
    • Was du getan hast: Du hast geprüft, wie man den FTP-Client bedient (ftp -?) und ob ein Anonymous Login erlaubt ist.
    • Ergebnis: Login erfolgreich mit Benutzer anonymous und leerem Passwort. Bestätigung durch den Server-Code 230.
3. Phase: Exploitation (Datenextraktion)
    • Was du getan hast:
        1. Verzeichnisliste abgerufen mit ls.
        2. Fehlersuche betrieben: Du hast gemerkt, dass root.txt nicht da war (Error 550) und stattdessen flag.txt gefunden.
        3. Datei heruntergeladen mit get flag.txt.
    • Ergebnis: Die Flag wurde lokal gesichert und ausgelesen (cat flag.txt).

🛡️ Blue Team Perspektive (Absicherung)
Wie verhindert man, dass jemand wie du diese Daten klaut?
Schwachstelle
Schutzmaßnahme (Fix)
Anonymous Login
Deaktivieren! In der Konfiguration (vsftpd.conf) anonymous_enable=NO setzen.
Klartext-Übertragung
FTP ist unsicher. Nutze SFTP (über SSH) oder FTPS (mit TLS-Verschlüsselung).
Information Leakage
Das FTP-Banner ändern. Der Server sollte nicht verraten, welche Version (vsftpd 3.0.3) er nutzt, damit Angreifer keine passenden Exploits suchen können.
Firewall
Den Port 21 nur für bekannte IP-Adressen freigeben, anstatt ihn für das ganze Internet zu öffnen.
Intrusion Detection (IDS)
Tools wie Fail2Ban installieren, die IP-Adressen nach zu vielen falschen Login-Versuchen automatisch sperren.

