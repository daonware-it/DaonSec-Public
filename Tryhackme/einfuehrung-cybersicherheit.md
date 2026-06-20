# 🖥️ TryHackMe – Cybersecurity Lernzettel

> **Pre Security Path** · *Was, Warum und Wie – alles auf einen Blick*

---

## 📋 Schnellübersicht

| Room | Thema | Kernkonzept |
|------|-------|-------------|
| [⚔️ Room 1](#room-1--offensive-security-intro) | Offensive Security Intro | Schwachstellen finden wie ein Hacker |
| [🛡️ Room 2](#room-2--defensive-security-intro) | Defensive Security Intro | Angriffe erkennen und stoppen |
| [🎯 Room 3](#room-3--careers-in-cyber) | Careers in Cyber | Rollen im Cyberteam kennenlernen |

---

# Room 1 · Offensive Security Intro

> 🔗 `tryhackme.com/room/offensivesecurityintro` · 🟢 Easy · ⏱ 10 min

**Ziel des Rooms:** Eine FakeBank-Website legal hacken und dabei sehen, wie Ethical Hacker denken und arbeiten.

---

## Task 1 – Think like a Hacker!

### 📖 Was passiert
- Einführung in das Konzept **Offensive Security**
- Das Ziel: Schwachstellen finden, *bevor* echte Angreifer sie ausnutzen
- Du hackst eine FakeBank-Website – legal, in einer sicheren Sandbox-Umgebung

### 💡 Warum ist das wichtig
- **Offensive Security** = Man denkt und handelt *wie ein Angreifer*, um Lücken zu finden
- Nur wer versteht, wie Hacker vorgehen, kann Systeme wirklich absichern
- Die legale Version davon nennt sich **Ethical Hacking** / **Penetration Testing**
- Firmen *beauftragen* Ethical Hacker, um ihre eigenen Systeme zu testen

> ✅ **Antwort:** `Offensive Security`

---

## Task 2 – Starting the Lab

### 📖 Was passiert
- Ein virtueller Desktop startet direkt im Browser – simuliert ein echtes System
- Die **FakeBank**-Anwendung lädt: eine simulierte Online-Banking-Website
- Du siehst Kontonummern, Kontostände und ein Terminal

### 💡 Warum ist das wichtig
- Cybersecurity-Training braucht eine **sichere Sandbox** – du übst mit echten Tools, ohne echte Systeme zu gefährden
- Virtuelle Maschinen (VMs) sind das Standardwerkzeug für sicheres Testen in der Praxis

---

## Task 3 – Find Hidden Pages

### 📖 Was passiert
- Websites lassen manchmal **versteckte Seiten** zugänglich, die nirgends verlinkt sind
- Im Terminal wird `dirb` ausgeführt, um genau diese Seiten aufzuspüren
- Ergebnis: dirb findet zwei Seiten – `/images` und `/bank-transfer`

### 💡 Warum ist das wichtig
- **Security through obscurity funktioniert nicht:** eine Seite nicht zu verlinken ≠ sie zu sichern
- Angreifer nutzen genau solche Scan-Tools, um Einfallstore zu finden
- Jede nicht benötigte Seite sollte *wirklich gesperrt oder entfernt* werden, nicht nur versteckt

### ⌨️ Befehl im Terminal

```bash
dirb http://fakebank.thm
```

### 🔧 Wie `dirb` funktioniert
- **dirb** = Directory Buster: probiert automatisch tausende typische URL-Pfade durch
- Findet Seiten wie `/admin`, `/bank-transfer`, `/login` per Brute-Force
- Zeilen mit `+` in der Ausgabe = erreichbare, gefundene Seiten

> ✅ **Gefundene versteckte URL:** `/bank-transfer`

---

## Task 4 – Attack the Admin Page

### 📖 Was passiert
- Die URL `/bank-transfer` direkt in die Adressleiste eingeben
- Ein verstecktes **Admin-Panel** erscheint: Geld zwischen Konten übertragen
- Zielkonto **8881** auswählen, **$2000+** einzahlen → Flag erscheint als grüner Text

### 💡 Warum ist das wichtig
- Ein Admin-Panel *ohne Authentifizierung* ist eine **kritische Sicherheitslücke**
- Jeder Angreifer, der die URL kennt (z.B. durch `dirb`), kann sofort darauf zugreifen
- Dies demonstriert **Broken Access Control** – Platz #1 in der [OWASP Top 10](https://owasp.org/Top10/)

### 🔧 Schritte im Detail
1. URL eingeben: `http://fakebank.thm/bank-transfer`
2. Zielkonto `8881` auswählen
3. Betrag `≥ $2000` eingeben → „Deposit Money" klicken
4. Flag als grüner Pop-up-Text kopieren → ins Antwortfeld einfügen (ALL CAPS)

### 🛠️ Gegenmaßnahmen in der Praxis
| Schwachstelle | Lösung |
|--------------|--------|
| Kein Login auf Admin-Seite | Starke Authentifizierung (Login + 2FA) |
| Versteckte statt geschützte URLs | Zugriffskontrolle auf Server-Ebene |
| Kein Rate-Limiting auf Scans | `dirb`-Traffic durch WAF blockieren |

---

# Room 2 · Defensive Security Intro

> 🔗 `tryhackme.com/room/defensivesecurityintro` · ℹ️ Info · ⏱ 15 min

**Ziel des Rooms:** Einen laufenden Angriff auf FakeBank als SOC-Analyst erkennen, analysieren und stoppen.

---

## Task 1 – Think like a Defender

### 📖 Was passiert
- Einführung in **Defensive Security**: Systeme schützen statt angreifen
- Fokus auf: Angriffe *erkennen*, *untersuchen* und *darauf reagieren*
- Gegensatz zu Offensive Security: kein aktiver Angriff – Überwachung und Schutz

### 💡 Warum ist das wichtig
- Offensive und Defensive Security sind **kein Gegensatz** – beide Seiten braucht man für echte Sicherheit
- Jedes Unternehmen braucht ein Team, das Angriffe *bemerkt*, bevor Schaden entsteht
- Ziel: **Dwell Time** minimieren – die Zeit, die ein Angreifer unentdeckt im System verbringt

> ✅ **Antwort:** `Detect and respond to attacks`

---

## Task 2 – Detect Suspicious Activity

### 📖 Was passiert
- Szenario: **Joe** ist Anfänger-SOC-Analyst auf seinem ersten Solo-Shift
- Das Monitoring-Dashboard zeigt ungewöhnliche Aktivitäten
- Aufgabe: Die **verdächtige IP-Adresse** im Dashboard identifizieren

### 💡 Warum ist das wichtig
- **SOC-Analysten** sitzen täglich genau vor so einem Dashboard
- Die meiste Aktivität ist normal – verdächtige Muster fallen durch Anomalien auf (z.B. viele Anfragen in kurzer Zeit von einer IP)
- Früherkennung = weniger Schaden → *schnelle Reaktion ist entscheidend*

### 🔧 Vorgehen im Dashboard
1. „View Site" klicken → Monitoring-Dashboard öffnet sich
2. Aktuelle Alerts prüfen
3. Die **Source IP** identifizieren, die auffällig viele Anfragen sendet

---

## Task 3 – Identify the Attack

### 📖 Was passiert
- Joe weiß jetzt, *dass* etwas passiert – jetzt muss er herausfinden, *was* der Angreifer vorhat
- Liste der **URL Discovery Attempts** einsehen
- Den *letzten Eintrag* in der Liste notieren (= URL, die der Angreifer gerade sucht)

### 💡 Warum ist das wichtig
- „URL Discovery" = Der Angreifer macht genau das Gleiche wie Room 1 mit `dirb` – er scannt nach versteckten Seiten
- Die Angriffsziele zeigen, *wonach* der Angreifer sucht → Verteidigungsmaßnahmen können priorisiert werden
- **Logs sind das Gedächtnis eines Systems** – ohne Logs keine Analyse, keine Forensik

### 🔧 Vorgehen
1. Dashboard → „URL Discovery Attempts" aufrufen
2. Letzten Eintrag in der Liste anschauen
3. URL kopieren → als Antwort eintragen

---

## Task 4 – Stop the Attack

### 📖 Was passiert
- **Containment**: Den Angriff stoppen, während er aktiv läuft
- IP des Angreifers mit einer Firewall-Regel blockieren
- IP in „Add Firewall Rule" eingeben → Dropdown „BLOCK" → „Apply"

### 💡 Warum ist das wichtig
- **Firewall-Regeln** sind die erste Verteidigungslinie – sie blockieren Verbindungen nach IP, Port oder Protokoll
- Containment ≠ vollständige Lösung: danach folgen Analyse, Härtung und Wiederherstellung

### 🔧 Der Incident Response Prozess

```
1. Erkennen   →  2. Einschränken  →  3. Ausrotten  →  4. Wiederherstellen
  (Detect)         (Contain)          (Eradicate)        (Recover)
```

### 🔐 Blockierte Angreifer-IP (aus dem Room)

```
Firewall Rule:  32.122.195.63  →  DROP (BLOCK)
```

> ✅ **Flag erscheint als Erfolgsmeldung nach dem Blockieren**

---

# Room 3 · Careers in Cyber

> 🔗 `tryhackme.com/room/careersincyber` · 🟢 Easy · ⏱ 15 min

**Ziel des Rooms:** Verschiedene Rollen in der Cybersecurity kennenlernen und herausfinden, welche am besten passt.

---

## Task 1 – Help FakeBank (Security Operations Hub)

### 📖 Was passiert
- FakeBank wird von einem **Ransomware-Angriff** getroffen – Kundendaten werden gestohlen
- Du betrittst das **Security Operations Hub** und hilfst dem Team
- Du triffst vier verschiedene Rollen im Cyberteam

### 💡 Warum ist das wichtig
- Ein echter Cyberangriff braucht ein *ganzes Team* – nicht eine Person allein
- Jede Rolle hat spezifische Aufgaben, Werkzeuge und Denkweisen
- Dieses Szenario zeigt, wie ein Angriff *von innen* bewältigt wird

### 🧑‍💻 Die vier Kernrollen

| Rolle | Aufgabe | Denkweise |
|-------|---------|-----------|
| 👁️ **SOC Analyst** | Erkennt Angriffe in Echtzeit durch Log-Überwachung | Wachsam, mustererkennend |
| 🔓 **Pentester** | Findet heraus, *wie* der Angreifer reingekommen ist | Wie ein Angreifer |
| 🔍 **Forensic Analyst** | Untersucht, *was* der Angreifer im System gemacht hat | Wie ein Detektiv |
| 🔧 **Security Engineer** | Schließt Lücken, damit der Angriff nicht wiederholt werden kann | Konstruktiv, langfristig |

---

## Task 2 – Blue Teaming

### 📖 Was passiert
- Du hast aktiv am **Blue Team** teilgenommen – den verteidigenden Kräften
- Drei Blue-Team-Mitglieder werden vorgestellt: **David, Priya und Sam**

### 💡 Warum ist das wichtig
- **Blue Team** = alle Funktionen, die ein Unternehmen *verteidigen*
- Logs müssen *kontinuierlich* überwacht werden – Angreifer können sich wochenlang verstecken
- Forensik ist nötig, um denselben Angriff in Zukunft zu verhindern

### 🔧 Blue Team Rollen im Detail

#### 👁️ David – SOC Analyst
- Überprüft Logs täglich, sucht nach Anomalien in normaler Aktivität
- Erste Alarmstelle bei verdächtigen Ereignissen
- Nutzt Tools wie SIEMs (z.B. Splunk, ELK Stack)

#### 🔍 Priya – Forensic Analyst
- Rekonstruiert den Angriff: Was, Wann, Wie wurde das System kompromittiert?
- Bringt Ereignisse in chronologische Reihenfolge
- Ergebnisse fließen in zukünftige Schutzmaßnahmen ein

#### 🔧 Sam – Security Engineer
- Schließt die Sicherheitslücken nach dem Angriff
- Verbessert Systeme, damit der nächste Angriff früher auffällt
- Denkt langfristig und präventiv

> ✅ **Antwort:** `SOC Analyst` (die Rolle, die du im Practical gespielt hast)

---

## Task 3 – Red Teaming

### 📖 Was passiert
- **Maya** (Pentesterin) zeigt dir den Angriff aus der *Angreiferperspektive*
- Ihr rekonstruiert gemeinsam die Angriffskette Schritt für Schritt

### 💡 Warum ist das wichtig
- **Red Team** = Angreifer-Simulation: denkt und handelt wie ein echter Hacker, um Lücken zu finden
- Red + Blue Team zusammen = **Purple Team**: maximale Sicherheit durch Zusammenarbeit
- Die Angriffskette zeigt: aus *einer einzigen E-Mail* kann ein vollständiger Datenverlust entstehen

### ⛓️ Die Angriffskette (Attack Chain)

```
📧 Bösartige E-Mail
       ↓
⚙️  Script-Ausführung  (Malware wird gestartet)
       ↓
🖥️  Systemkontrolle   (Angreifer übernimmt Fernzugriff)
       ↓
💾  Daten gestohlen   (Kundendaten exfiltriert)
```

### 🔧 Was Red Teamer tun
- Simulieren echte Angriffe aus Angreifer-Sicht (ohne echten Schaden)
- Testen, ob das Blue Team sie *rechtzeitig* bemerkt
- Berichten gefundene Lücken an das Unternehmen

> ✅ **Antwort:** `Penetration Tester`

---

## Task 4 – Careers Quiz

### 📖 Was passiert
- Interaktives Quiz: Welche Cybersecurity-Rolle passt zu dir?
- „View Site" → Quiz abschließen → Flag erscheint am Ende

### 🎯 Welche Richtung könnte passen?

| Wenn du... | Dann schau dir an... |
|-----------|---------------------|
| Gerne Logs analysierst und Muster suchst | 👁️ SOC Analyst / Blue Team |
| Kreativ denkst und Lücken finden willst | 🔓 Pentester / Red Team |
| Puzzles liebst und Detektivarbeit magst | 🔍 Digital Forensics |
| Lieber Systeme baust und absicherst | 🔧 Security Engineer |
| Gesetze und Prozesse interessant findest | 📋 GRC / Compliance |
| Dich für Cloud-Infrastruktur begeisterst | ☁️ Cloud Security |

---

# 📚 Schlüsselbegriffe auf einen Blick

| Begriff | Bedeutung |
|---------|-----------|
| **Offensive Security** | Denken wie ein Angreifer, um Schwachstellen zu finden |
| **Defensive Security** | Systeme überwachen, schützen und auf Angriffe reagieren |
| **Ethical Hacker** | Legaler Hacker, der im Auftrag eines Unternehmens testet |
| **SOC** | Security Operations Center – das Überwachungszentrum |
| **dirb** | Tool zum Brute-Forcen von versteckten URLs/Verzeichnissen |
| **Firewall** | Netzwerkkomponente, die Verbindungen nach Regeln filtert |
| **OWASP Top 10** | Liste der 10 häufigsten Web-Sicherheitslücken |
| **Broken Access Control** | Wenn Seiten/Funktionen ohne nötige Rechte erreichbar sind |
| **Containment** | Sofortmaßnahme: Angriff stoppen, während er läuft |
| **Dwell Time** | Zeit, die ein Angreifer unentdeckt im System verbringt |
| **Red Team** | Greift an (simuliert) – findet Lücken |
| **Blue Team** | Verteidigt – erkennt und reagiert auf Angriffe |
| **Purple Team** | Red + Blue Team arbeiten zusammen |
| **Forensic Analysis** | Digitale Spurensicherung nach einem Angriff |
| **Attack Chain** | Abfolge der Schritte eines Angriffs von Anfang bis Ende |

---

*TryHackMe – Pre Security Path · Erstellt für persönlichen Lernzweck*
