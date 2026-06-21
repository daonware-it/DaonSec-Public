# 🌐 TryHackMe – Netzwerk-Grundlagen Lernzettel / Spickzettel

> Basierend auf den Rooms: **What is Networking?** | **Intro to LAN** | **OSI Model**  
> Erstellt als persönlicher Spickzettel zum Nachschlagen

---

## 📚 Inhaltsverzeichnis

1. [Room 1 – What is Networking?](#room-1--what-is-networking)
   - Task 1: Was ist ein Netzwerk?
   - Task 2: Was ist das Internet?
   - Task 3: Geräte im Netzwerk identifizieren (IP & MAC)
   - Task 4: Ping (ICMP)
2. [Room 2 – Intro to LAN](#room-2--intro-to-lan)
   - Task 1: LAN-Topologien (Star, Bus, Ring, Switch, Router)
   - Task 2: Subnetting
   - Task 3: ARP
   - Task 4: DHCP
3. [Room 3 – OSI Model](#room-3--osi-model)
   - Alle 7 Schichten im Überblick
   - Layer 1 – Physical
   - Layer 2 – Data Link
   - Layer 3 – Network
   - Layer 4 – Transport (TCP vs. UDP)
   - Layer 5 – Session
   - Layer 6 – Presentation
   - Layer 7 – Application
4. [Schnellreferenz & Merkhilfen](#schnellreferenz--merkhilfen)

---

## Room 1 – What is Networking?

### Task 1: Was ist ein Netzwerk? (`Network`)

**Was?** Ein Netzwerk = verbundene Geräte, die miteinander kommunizieren.

**Warum wichtig?** In der Cybersecurity ist Networking eine Grundlage – Angreifer nutzen Netzwerke, um sich zu bewegen, Daten zu stehlen oder Systeme zu kompromittieren.

**Merksatz:**
> *„Netzwerke sind einfach verbundene Dinge – wie ein Freundeskreis, der durch gemeinsame Interessen verbunden ist."*

| Beispiel im Alltag | Beispiel in IT |
|--------------------|----------------|
| Öffentlicher Nahverkehr | Router verbinden PCs |
| Stromnetz | Server verbinden sich mit Clients |
| Postsystem | Pakete (Datenpakete) werden verschickt |

- In der IT: von **2 Geräten bis Milliarden** (Laptops, Handys, Kameras, Ampeln, …)
- **Schlüsselbegriff:** `Network` (das verbindende Konzept)

---

### Task 2: Was ist das Internet? (`Tim Berners-Lee`)

**Was?** Das Internet = ein riesiges Netzwerk aus vielen kleinen Netzwerken.

**Warum?** Damit Geräte weltweit miteinander kommunizieren können, braucht es ein übergeordnetes Netz.

**Historischer Überblick:**

| Zeitpunkt | Ereignis |
|-----------|---------|
| Späte 1960er | **ARPANET** – erstes dokumentiertes Netzwerk (US-Verteidigungsministerium) |
| **1989** | **Tim Berners-Lee** erfindet das **World Wide Web (WWW)** |
| Heute | Das Internet als Repository für Informationen und Kommunikation |

**Netzwerktypen:**

| Typ | Beschreibung | Beispiel |
|-----|-------------|---------|
| **Private Network** | Internes Netz, nicht öffentlich | Heimnetzwerk, Firmennetz |
| **Public Network** | Das Internet – öffentlich zugänglich | Das gesamte Internet |

> 💡 **Merkhilfe:** Tim **B**erners-Lee → **B** wie **Browser** → Er ermöglichte das Surfen im Web.

---

### Task 3: Geräte identifizieren – IP & MAC

**Was?** Jedes Gerät hat zwei Identifikatoren:

| Identifikator | Typ | Veränderbar? | Beispiel |
|--------------|-----|-------------|---------|
| **IP-Adresse** | Logisch (Software) | ✅ Ja | `192.168.1.100` |
| **MAC-Adresse** | Physisch (Hardware) | ❌ Nein (aber spoofbar) | `a4:c3:f0:85:ac:2d` |

---

#### IP-Adresse (Internet Protocol)

- Besteht aus **4 Oktetten** (je 0–255), getrennt durch Punkte
- Beispiel: `192.168.1.1`
- Jedes Segment = ein **Octet**

**IPv4 vs. IPv6:**

| | IPv4 | IPv6 |
|-|------|------|
| Format | `192.168.1.1` | `2001:0db8:85a3::8a2e:0370:7334` |
| Adressen | ~4,3 Milliarden | ~340 Undezillionen |
| Problem | Werden knapp! | Lösung für Adressmangel |

**Private vs. Öffentliche IP:**

| Typ | Bereich | Wer sieht es? |
|-----|---------|--------------|
| **Private IP** | 192.168.x.x | Nur im lokalen Netz |
| **Public IP** | Vom ISP vergeben | Sichtbar im Internet |

> 💡 Cisco schätzte ~50 Milliarden Geräte bis Ende 2021 → IPv4 reicht nicht → IPv6 nötig!

---

#### MAC-Adresse (Media Access Control)

- Im **NIC (Network Interface Card)** eingebrannt → vom Hersteller fest gesetzt
- Format: `a4:c3:f0:85:ac:2d` (Hexadezimalzahlen, durch Doppelpunkte getrennt)
- **Erste 6 Zeichen** = Herstelleridentifikation
- **Letzte 6 Zeichen** = Eindeutige Gerätenummer

**MAC Spoofing:**
- Ein Gerät gibt vor, eine andere MAC-Adresse zu haben
- Gefahr: Firewall-Regeln, die auf MAC-Adressen basieren, können umgangen werden
- Beispiel: WLAN in Cafés nutzt oft MAC-Adress-Filterung → spoofbar!

> ⚠️ **Sicherheitsrisiko:** Schlecht implementierte Sicherheitssysteme, die auf MAC-Adressen vertrauen, sind angreifbar!

---

### Task 4: Ping (ICMP)

**Was?** Ping = eines der grundlegendsten Netzwerktools.

**Wie?** Sendet **ICMP (Internet Control Message Protocol)** Pakete und misst die Antwortzeit.

**Ablauf:**
```
Eigenes Gerät  ──→  [ICMP Echo Request]  ──→  Zielgerät
Eigenes Gerät  ←──  [ICMP Echo Reply]   ←──  Zielgerät
```

**Syntax:**
```bash
ping <IP-Adresse>
# Beispiel:
ping 192.168.1.254
ping 8.8.8.8
ping google.com
```

**Was zeigt Ping?**
- Ob die Verbindung besteht
- Wie zuverlässig die Verbindung ist
- **RTT (Round-Trip-Time)** in Millisekunden

> 💡 Ping ist auf Windows, Linux und macOS vorinstalliert!

---

## Room 2 – Intro to LAN

### Task 1: LAN-Topologien

**Was ist eine Topologie?** Das Design/Aussehen eines Netzwerks – wie die Geräte verbunden sind.

---

#### ⭐ Star Topology (Stern)

```
        [Switch/Hub]
       /     |      \
  [PC1]   [PC2]   [PC3]
```

| ✅ Vorteile | ❌ Nachteile |
|------------|-------------|
| Sehr zuverlässig (Ausfall eines Geräts = kein Ausfall des Netzes) | Teurer (mehr Kabel + Switch nötig) |
| Skalierbar (leicht erweiterbar) | Bei Ausfall des zentralen Geräts → ganzes Netz weg |
| Einfache Fehlerbehebung | |

**Warum heute am häufigsten?** Wegen Zuverlässigkeit und Skalierbarkeit.

---

#### 🚌 Bus Topology (Bus)

```
──────────────────────── (Backbone-Kabel)
  |       |       |
[PC1]   [PC2]   [PC3]
```

| ✅ Vorteile | ❌ Nachteile |
|------------|-------------|
| Günstig (wenig Kabel) | Anfällig für Flaschenhals/Bottleneck |
| Einfach aufzubauen | Schwer zu troubleshooten |
| | Alle teilen dasselbe Kabel → langsam bei hohem Traffic |

---

#### 🔄 Ring Topology (Ring)

```
[PC1] ──→ [PC2] ──→ [PC3]
  ↑                    |
  └────── [PC4] ←──────┘
```

| ✅ Vorteile | ❌ Nachteile |
|------------|-------------|
| Einfache Richtung → leichtes Troubleshooting | Ineffizient (Daten müssen alle Geräte durchlaufen) |
| Weniger Bottlenecks | Single Point of Failure: 1 Kabelbruch = ganzes Netz weg |

---

#### 🔀 Was ist ein Switch?

- **Zweck:** Verbindet mehrere Geräte in einem Netzwerk
- **Intelligenter als Hub:** Weiß, an welchen Port Daten gesendet werden sollen
- **Datenverteilung:** Sendet Daten NUR an den zuständigen Port (kein Broadcasting wie Hub)
- Typisch in: Büros, Schulen, größeren Netzwerken
- Können mit Switches und Routern verbunden werden → **Redundanz**

---

#### 🌐 Was ist ein Router?

- **Zweck:** Verbindet **verschiedene Netzwerke** miteinander
- **Routing:** Erstellt Pfade zwischen Netzwerken für die Datenübertragung
- Findet den besten Weg für Datenpakete
- Router + Router = mehr Pfade = **mehr Redundanz** (kein Downtime bei Ausfall eines Pfades)

> 💡 **Merkhilfe:** Switch = innerhalb eines Netzes | Router = zwischen Netzen

---

### Task 2: Subnetting

**Was?** Subnetting = ein Netzwerk in kleinere Teilnetzwerke aufteilen.

**Warum?** 
- Sicherheit: Abteilungen (HR, Finance, IT) trennen
- Effizienz: Weniger Traffic pro Segment
- Beispiel: Café-WLAN für Personal ≠ WLAN für Gäste

**Subnet Mask:**
- **32 Bits** (0 oder 255 pro Octet, z.B. `255.255.255.0`)
- Definiert, wie viele Hosts in einem Netz möglich sind

**Die drei wichtigen Adressen:**

| Adresstyp | Beschreibung | Beispiel |
|-----------|-------------|---------|
| **Network Address** | Identifiziert den Start des Netzwerks | `192.168.1.0` |
| **Host Address** | Identifiziert ein Gerät im Netz | `192.168.1.100` |
| **Default Gateway** | Gerät, das Daten in andere Netze schickt | `192.168.1.1` oder `192.168.1.254` |

> 💡 **Default Gateway** = meist `.1` oder `.254` – das ist dein Router!

---

### Task 3: ARP – Address Resolution Protocol

**Was?** ARP verbindet MAC-Adresse ↔ IP-Adresse auf einem Netzwerk.

**Warum?** Geräte kommunizieren über MAC-Adressen (physisch), kennen aber meist nur IP-Adressen (logisch) → ARP übersetzt!

**Ablauf:**

```
Gerät A weiß: "Ich will mit 192.168.1.5 reden"
Aber: Welche MAC-Adresse hat 192.168.1.5?

1. ARP REQUEST  → Broadcast an ALLE: "Wer hat 192.168.1.5?"
2. ARP REPLY    ← Nur das Gerät mit 192.168.1.5 antwortet: "Ich! Meine MAC ist xx:xx:xx:xx"
3. ARP CACHE    → Gerät A speichert die Zuordnung IP ↔ MAC lokal
```

**ARP Pakettypen:**

| Typ | Beschreibung |
|-----|-------------|
| **ARP Request** | Broadcast-Anfrage: "Wer hat diese IP?" |
| **ARP Reply** | Antwort des Geräts mit seiner MAC-Adresse |

**ARP Cache:** Lokale Tabelle auf jedem Gerät, die IP→MAC-Zuordnungen speichert (für zukünftige Kommunikation).

---

### Task 4: DHCP – Dynamic Host Configuration Protocol

**Was?** DHCP vergibt automatisch IP-Adressen an Geräte.

**Warum?** Ohne DHCP müsste jede IP manuell eingetragen werden – unpraktisch in großen Netzen!

**Der DHCP-Prozess (4 Schritte):**

```
Gerät          DHCP-Server
  |                |
  |─ DHCP DISCOVER ──→|   "Gibt es einen DHCP-Server?"
  |                |
  |← DHCP OFFER ────|   "Ja! Du kannst 192.168.1.50 haben"
  |                |
  |─ DHCP REQUEST ──→|   "Ja, ich nehme 192.168.1.50!"
  |                |
  |← DHCP ACK ──────|   "Bestätigt! Die IP gehört dir jetzt."
  |                |
```

**Merkhilfe DORA:** **D**iscover → **O**ffer → **R**equest → **A**CK

---

## Room 3 – OSI Model

### Überblick: Die 7 Schichten

**OSI = Open Systems Interconnection Model**

**Warum?** Standardisiertes Framework, damit verschiedene Geräte/Hersteller miteinander kommunizieren können. Jede Schicht hat eine klare Aufgabe.

**Encapsulation:** An jeder Schicht werden dem Datenpaket neue Informationen hinzugefügt (Header/Trailer).

```
┌─────────────────────────────────────────────┐
│  Layer 7 │ APPLICATION   │ HTTP, DNS, FTP   │  ← Nutzer-Ebene
│  Layer 6 │ PRESENTATION  │ SSL/TLS, Encoding│
│  Layer 5 │ SESSION       │ Verbindungsaufbau│
│  Layer 4 │ TRANSPORT     │ TCP / UDP        │
│  Layer 3 │ NETWORK       │ IP, Routing      │
│  Layer 2 │ DATA LINK     │ MAC, NIC, Frames │
│  Layer 1 │ PHYSICAL      │ Kabel, Signale   │  ← Hardware-Ebene
└─────────────────────────────────────────────┘
```

**Merkhilfe (englisch, 7→1):**  
> **A**ll **P**eople **S**eem **T**o **N**eed **D**ata **P**rocessing  
> Application – Presentation – Session – Transport – Network – Data Link – Physical

---

### Layer 1 – Physical (Physisch)

**Was?** Die unterste Schicht – physische Hardware.

**Aufgaben:**
- Überträgt **elektrische Signale** zwischen Geräten
- Nutzt **binäres System** (0 und 1)
- Bezieht sich auf physische Komponenten: Kabel, Stecker, NICs

**Beispiel:** Ethernet-Kabel verbinden Geräte → Signale laufen durch den Draht.

> 💡 Kein Protokoll, kein Routing – nur rohe Bits über physische Medien!

---

### Layer 2 – Data Link (Datensicherung)

**Was?** Physische Adressierung der Übertragung.

**Aufgaben:**
- Empfängt Paket von Layer 3 (mit IP-Adresse)
- Fügt die **MAC-Adresse** des Zielgeräts hinzu
- Präsentiert Daten in einem übertragbaren Format

**Wichtige Komponente:** NIC (Network Interface Card)
- In jedem Netzwerkfähigen Gerät verbaut
- Hat eine einzigartige, eingebrannte MAC-Adresse

> ⚠️ MAC-Adressen können **gespooft** (gefälscht) werden – auch wenn sie "eingebrannt" sind!

---

### Layer 3 – Network (Netzwerk)

**Was?** Routing und Re-Assembly der Datenpakete.

**Aufgaben:**
- Bestimmt den **optimalen Pfad** für Datenpakete
- Arbeitet mit **IP-Adressen**
- Reassembliert Pakete in der richtigen Reihenfolge

**Routing-Protokolle:**

| Protokoll | Voller Name | Beschreibung |
|-----------|------------|-------------|
| **OSPF** | Open Shortest Path First | Findet kürzesten Weg |
| **RIP** | Routing Information Protocol | Klassisches Routing-Protokoll |

**Entscheidungsfaktoren für den Pfad:**
1. **Kürzester Weg** – wenigste Geräte dazwischen
2. **Zuverlässigster Weg** – wo gehen keine Pakete verloren?
3. **Schnellste physische Verbindung** – Kupfer vs. Glasfaser

**Layer 3 Geräte:** Router (arbeiten mit IP-Adressen)

---

### Layer 4 – Transport (Transport)

**Was?** Übertragung von Daten – via TCP oder UDP.

#### TCP – Transmission Control Protocol

**Merksatz:** TCP = **Zuverlässig** wie ein eingeschriebener Brief mit Bestätigung

| ✅ Vorteile | ❌ Nachteile |
|------------|-------------|
| Garantiert Genauigkeit der Daten | Benötigt zuverlässige Verbindung |
| Error Checking eingebaut | Langsamer (durch Handshake & Bestätigungen) |
| Daten kommen in richtiger Reihenfolge an | Mehr Overhead |
| Verbindung bleibt bestehen (Connection-oriented) | |

**Verwendung:** E-Mail, Datei-Download, Webseiten (HTTP/HTTPS)

**TCP 3-Way Handshake:**
```
Client ──→ SYN      ──→ Server
Client ←── SYN-ACK  ←── Server  
Client ──→ ACK       ──→ Server
Verbindung hergestellt!
```

---

#### UDP – User Datagram Protocol

**Merksatz:** UDP = **Fire and forget** – senden und hoffen 🎲

| ✅ Vorteile | ❌ Nachteile |
|------------|-------------|
| Deutlich schneller als TCP | Keine Garantie, dass Daten ankommen |
| Keine aufgebaute Verbindung nötig | Kein Error Checking |
| Flexibel für Entwickler | Keine Reihenfolge garantiert |

**Verwendung:** Video-Streaming, Online-Gaming, VoIP-Telefonie

**Vergleich TCP vs. UDP:**

| | TCP | UDP |
|-|-----|-----|
| Verbindung | Connection-oriented | Connectionless |
| Zuverlässigkeit | Hoch | Niedrig |
| Geschwindigkeit | Langsamer | Schneller |
| Reihenfolge | Garantiert | Nicht garantiert |
| Anwendung | E-Mail, FTP, HTTP | Streaming, Gaming |

---

### Layer 5 – Session (Sitzung)

**Was?** Erstellt und verwaltet Verbindungen (Sessions) zwischen Computern.

**Aufgaben:**
- Baut Verbindung auf → **Session wird erstellt**
- Hält Session aktiv solange sie gebraucht wird
- Schließt Session bei Inaktivität oder Verbindungsverlust
- **Checkpoints**: Bei Datenverlust werden nur neueste Daten neu gesendet → spart Bandbreite

**Wichtig:** Sessions sind **einzigartig** – Daten können nicht zwischen Sessions wandern!

> 💡 Analogie: Wie ein Telefonanruf – Verbindung aufbauen, reden, auflegen.

---

### Layer 6 – Presentation (Darstellung)

**Was?** Standardisierung und Übersetzung der Daten.

**Aufgaben:**
- Agiert als **Übersetzer** zwischen Application Layer und Session Layer
- Stellt sicher, dass Daten unabhängig vom verwendeten Programm gleich dargestellt werden
- **Datenverschlüsselung** (z.B. HTTPS beim Websurfen)
- Datenkompression

**Beispiel:** Du verwendest Gmail, dein Freund Thunderbird → die E-Mail wird trotzdem korrekt dargestellt (dank Layer 6).

---

### Layer 7 – Application (Anwendung)

**Was?** Die Schicht, mit der Nutzer direkt interagieren.

**Aufgaben:**
- Stellt **GUI (Graphical User Interface)** für Nutzer bereit
- Protokolle für Benutzerinteraktion mit Daten

**Protokolle auf Layer 7:**

| Protokoll | Verwendung |
|-----------|-----------|
| **HTTP/HTTPS** | Webseiten aufrufen |
| **DNS** | Domainnamen → IP-Adressen übersetzen |
| **FTP** | Dateiübertragung |
| **SMTP/IMAP/POP3** | E-Mail senden/empfangen |
| **SSH** | Sichere Fernverbindung |

**Beispiele für Layer-7-Anwendungen:**
- Browser (Chrome, Firefox)
- E-Mail-Programme (Thunderbird, Outlook)
- Dateimanager (FileZilla)

---

## Schnellreferenz & Merkhilfen

### OSI-Schichten-Übersicht (Spickzettel)

| Layer | Name | Protokolle/Technologien | Schlüsselkonzept |
|-------|------|------------------------|-----------------|
| 7 | Application | HTTP, DNS, FTP, SMTP | Benutzer-Interaktion, GUI |
| 6 | Presentation | SSL/TLS, JPEG, ASCII | Verschlüsselung, Übersetzung |
| 5 | Session | NetBIOS, RPC | Session-Verwaltung, Checkpoints |
| 4 | Transport | TCP, UDP | TCP (zuverlässig) vs UDP (schnell) |
| 3 | Network | IP, OSPF, RIP | Routing, IP-Adressen |
| 2 | Data Link | Ethernet, MAC, ARP | MAC-Adressen, Frames, NIC |
| 1 | Physical | Ethernet-Kabel, WLAN | Bits, elektrische Signale |

---

### Wichtige Protokolle im Überblick

| Protokoll | Ausgeschrieben | Schicht | Zweck |
|-----------|---------------|---------|-------|
| **ICMP** | Internet Control Message Protocol | 3 | Ping, Netzwerkdiagnose |
| **ARP** | Address Resolution Protocol | 2 | IP → MAC-Auflösung |
| **DHCP** | Dynamic Host Configuration Protocol | 7 | Auto IP-Vergabe |
| **TCP** | Transmission Control Protocol | 4 | Zuverlässige Übertragung |
| **UDP** | User Datagram Protocol | 4 | Schnelle Übertragung |
| **OSPF** | Open Shortest Path First | 3 | Routing-Protokoll |
| **RIP** | Routing Information Protocol | 3 | Routing-Protokoll |
| **DNS** | Domain Name System | 7 | Domain → IP |
| **HTTP/S** | HyperText Transfer Protocol (Secure) | 7 | Webseiten |

---

### Befehle & Syntax

```bash
# Ping – Netzwerkverbindung testen
ping <IP-Adresse>
ping 10.10.10.10
ping google.com

# Unter Linux – ARP-Cache anzeigen
arp -a

# Unter Linux – IP-Konfiguration anzeigen
ip addr
ifconfig

# Unter Windows – IP-Konfiguration
ipconfig /all
```

---

### Kurzdefinitionen (Glossar)

| Begriff | Definition |
|---------|-----------|
| **Network** | Verbundene Geräte, die kommunizieren |
| **Internet** | Globales Netzwerk aus vielen kleinen Netzen |
| **IP-Adresse** | Logischer Identifikator eines Geräts (veränderbar) |
| **MAC-Adresse** | Physischer Identifikator (Hersteller eingebrannt) |
| **Subnet/Subnetting** | Netzwerk in kleinere Teilnetze aufteilen |
| **Default Gateway** | Router-Adresse für Daten außerhalb des Netzes |
| **Switch** | Verbindet Geräte innerhalb eines Netzes (Layer 2) |
| **Router** | Verbindet verschiedene Netze (Layer 3) |
| **Encapsulation** | Hinzufügen von Header-Infos an jeder OSI-Schicht |
| **ARP Cache** | Lokale Tabelle: IP ↔ MAC-Zuordnungen |
| **Session** | Aktive Verbindung zwischen zwei Geräten |
| **Spoofing** | Vortäuschen einer anderen Identität (z.B. MAC) |
| **DORA** | Discover → Offer → Request → ACK (DHCP-Prozess) |

---

### LAN-Topologien auf einen Blick

| Topologie | Aussehen | Stärke | Schwäche |
|-----------|---------|--------|---------|
| ⭐ **Star** | Sternförmig, zentraler Switch | Zuverlässig, skalierbar | Teuer, zentraler SPoF |
| 🚌 **Bus** | Alle an einem Kabel | Günstig, einfach | Bottleneck, schwer troubleshoot |
| 🔄 **Ring** | Kreisförmig | Kein Bottleneck | Kabelbruch = Netzausfall |

---

*Quellen: TryHackMe – Pre Security Path → Network Fundamentals*  
*Rooms: whatisnetworking | introtolan | osimodelzi*
