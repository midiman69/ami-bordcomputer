# Ami Bordcomputer - Projektstatus

Stand: November 2026

# Projektziel

Modularer Bordcomputer für den Citroën Ami mit:

- Home Assistant
- Raspberry Pi
- ESP32-Systemen
- WiCAN
- Fahrzeugtelemetrie
- Rückfahrkamera
- Parksensoren
- Ambientebeleuchtung
- Audio-/Infotainment-System
- Fernzugriff

Grundsatz:

> Der Ami muss auch bei Ausfall des Raspberry Pi, Home Assistant oder einzelner Komponenten vollständig fahrbereit bleiben.

---

# Hauptkomponenten

## Fahrzeug

- Citroën Ami
- OBD2-Port

## Bordcomputer

- Raspberry Pi
- Home Assistant
- ESP32 Ami-Fahr
- ESP32-C3 Heckmodul
- Nextion Display
- WiCAN
- Lepy LP-269S
- 50 Ah LiFePO4
- intAct Battery Guard
- TP-Link WR3602BE
- TP-Link M7350
- Echo Pop
- 70mai Dashcam

---

# Stromversorgung

## Hauptbatterie

50 Ah LiFePO4

Schutz:

- intAct Battery Guard

Versorgt:

- Raspberry Pi
- Home Assistant
- Router
- LTE-Router
- Ami-Fahr ESP
- Hecksystem
- Lepy
- Innenbeleuchtung
- Dashcam

Nicht versorgt:

- Fahrzeug selbst
- OBD2-Port
- WiCAN

---

# Strommessung

## INA226

Installationsort:

```text
LiFePO4
↓
Battery Guard
↓
INA226
↓
Sicherungskasten
↓
Verbraucher
```

Messung:

- Spannung
- Strom
- Leistung

Ziele:

- Ruhestrom bestimmen
- Lastprofile erfassen
- Batterieverbrauch analysieren

---

# Spannungswandler

## MP1584

Verwendung:

- Xmini-Wächter
- Ami-Fahr ESP
- Heck-ESP

## USB-C KFZ-Wandler

Verwendung:

- Raspberry Pi

---

# Wächter-Konzept

## Xmini-Wächter

Dauerhaft aktiv.

Aufgaben:

- Batteriewächter
- Unterspannungsschutz
- Pi-Watchdog
- Hauptverbraucher schalten

Versorgung:

```text
LiFePO4
↓
MP1584
↓
Xmini
```

---

# Netzwerk

## TP-Link WR3602BE

Bordnetz-Router

Aufgaben:

- WLAN im Fahrzeug
- Home Assistant Netzwerk
- ESPHome Netzwerk
- Lokale Kommunikation

---

# Internetstrategie

Priorität:

1. Heim-WLAN
2. iPhone-Hotspot
3. M7350 LTE

## Zuhause

Der WR3602BE verbindet sich mit dem Heim-WLAN.

Vorteile:

- Updates
- GitHub
- Backups
- Tailscale

## Unterwegs

Internet über den iPhone-Hotspot.

## Fernzugriff

M7350 als LTE-Backup.

---

# M7350 LTE-Router

Eigenschaften:

- startet nicht automatisch nach Spannungswiederkehr
- lädt bei USB lediglich den Akku
- läuft bei Spannungsverlust auf Akku weiter

Geplante Steuerung:

SwitchBot Bot Rechargeable

Ablauf:

```text
SwitchBot
↓
Einschaltknopf
↓
M7350 EIN/AUS
```

Verwendung:

- Fernzugriff
- LTE-Backup
- Tailscale

---

# Raspberry Pi

Aufgaben:

- Home Assistant
- ESPHome
- MQTT
- Dashboards
- Tailscale

Der Pi ist nicht fahrzeugkritisch.

---

# WiCAN

Anschluss:

```text
OBD2
```

Versorgung:

```text
Fahrzeug
```

Aufgaben:

- Fahrstufe D
- Fahrstufe N
- Fahrstufe R
- Fahrzeugdaten

---

# ESP Ami-Fahr

Aufgaben:

- Fahrzeuglogik
- Nextion-Ansteuerung
- IR-Steuerung
- Rückfahrlogik
- Dashcam-Steuerung

Versorgung:

```text
MP1584
```

---

# Rückfahrsystem

## Aktivierung

```text
WiCAN erkennt R
↓
Ami-Fahr ESP
↓
MOSFET
↓
12V nach hinten
```

## Gemeinsame Heckversorgung

Eine Leitung versorgt:

- Rückfahrkamera
- Rückfahrscheinwerfer
- Heck-ESP
- Parksensoren
- Buzzer

Sobald Fahrstufe R aktiv ist, wird die gesamte Heckgruppe eingeschaltet.

---

# Heck-ESP

Aufgaben:

- Parksensoren
- Abstandsmessung
- Buzzer
- Kommunikation mit Nextion

Abstände sollen auf dem Nextion dargestellt werden.

---

# Nextion Display

Anzeige von:

- Bordspannung
- Stromaufnahme
- Leistung
- Fahrstufe
- Innen-/Außentemperatur
- Innenfeuchtigkeit
- Parksensoren
- Systemstatus

---

# Ambientebeleuchtung

Ursprüngliche Idee:

Direkte RGB-Steuerung über MOSFET.

Verworfen.

Aktueller Stand:

Originalcontroller bleibt erhalten.

Steuerung über IR:

- KY-005 Sender
- KY-022 Empfänger

Vorteile:

- Originaleffekte bleiben erhalten
- Musikmodus bleibt erhalten
- Kein Reverse Engineering

---

# Lepy LP-269S

Signalweg:

```text
iPhone
↓
CarPlay Display
↓
Klinkenausgang
↓
Lepy
↓
Lautsprecher
```

Steuerung geplant über IR.

Offen:

- Standby-Stromverbrauch messen
- Entscheidung Dauerstrom oder Abschaltung

---

# CarPlay Display

Rolle:

- Navigation
- Siri
- Telefonie
- Musik

Zu prüfen:

- Externes Mikrofon möglich?
- Mikrofonbuchse vorhanden?
- Mikrofon-Lötpads vorhanden?

---

# Sensorik

## INA226

- Strom
- Spannung
- Leistung

## BH1750

- Helligkeit

Geplante Nutzung:

- automatische Displayhelligkeit
- Nachtmodus
- Coming Home

## Innenraumsensor

- Temperatur innen
- Luftfeuchtigkeit innen

## Außensensor

- Außentemperatur

---

# Sprachsteuerung

## Siri

Verwendung:

- Navigation
- Telefonie
- Musik
- CarPlay

## Alexa (Echo Pop)

Verwendung:

- Home Assistant Statusabfragen
- Bordcomputerfunktionen
- Fahrzeugstatus

Beispiele:

- "Alexa, wie hoch ist die Bordspannung?"
- "Alexa, wie viel Strom verbraucht das Ami-System?"

## Home Assistant Voice

Späteres Erweiterungsprojekt.

---

# Coming Home

Geplant:

Nur bei Dunkelheit aktiv.

Bedingung:

```text
BH1750
↓
wenig Umgebungslicht
```

Funktion:

- Ambientebeleuchtung aktivieren
- Nachlaufzeit

---

# Dashcam

## 70mai

Geplante Steuerung:

- ACC-Signal über ESP/MOSFET
- verzögerte Abschaltung
- Batterieschutz

---

# Spätere Erweiterungen (nicht Teil von Version 1)

## Lüftersteuerung

Vorhandene Hardware:

- Funme Lüfter klein
- Funme Lüfter groß

Status:

Nicht Bestandteil von Version 1.

Offene Punkte:

- Steuerbarkeit prüfen
- Stromverbrauch messen
- IR/SwitchBot/Hardwaremodifikation evaluieren

Mögliche spätere Automationen:

- Temperaturgesteuerte Lüftung
- Feuchtigkeitsgesteuerte Lüftung
- Campingmodus

---

# Offene Aufgaben

## Hardware

- INA226 integrieren
- BH1750 integrieren
- KY-005 einbauen
- KY-022 einbauen
- Lepy Stromverbrauch messen
- CarPlay-Mikrofon prüfen

## Software

- WiCAN einrichten
- Fahrstufe R auswerten
- Nextion Rückfahransicht
- Home Assistant Struktur

## Infrastruktur

- Tailscale neu aufsetzen
- Router konfigurieren
- GitHub aktualisieren
- M7350 + SwitchBot testen
