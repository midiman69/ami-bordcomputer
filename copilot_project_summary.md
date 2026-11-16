# Ami Bordcomputer

Modularer Bordcomputer für den Citroën Ami auf Basis von Raspberry Pi, Home Assistant, ESP32 und WiCAN.

## Projektziele

- Fahrzeugdaten über WiCAN auslesen
- Home Assistant im Fahrzeug betreiben
- Eigenes Fahrzeug-WLAN bereitstellen
- Rückfahrkamera und Parksensoren integrieren
- Audio- und Infotainment-Funktionen erweitern
- Stromverbrauch überwachen
- Fahrzeug und Bordcomputer strikt voneinander trennen

Grundsatz:

> Der Ami muss auch bei Ausfall des gesamten Bordcomputers vollständig fahrbereit bleiben.

---

# Systemübersicht

## Fahrzeugseite

- Citroën Ami
- OBD2-Port
- WiCAN

Der WiCAN ist direkt am OBD-Port angeschlossen und liefert Fahrzeuginformationen wie Fahrstufe und CAN-Daten.

## Bordcomputerseite

- 50 Ah LiFePO4 Batterie
- intAct Battery Guard
- Raspberry Pi
- Home Assistant
- ESP32 "Ami-Fahr"
- Xmini Wächter
- Nextion Display
- Lepy LP-269S Verstärker
- TP-Link WR3602BE Router
- TP-Link M7350 LTE-Router
- INA226 Stromsensor

---

# Stromversorgung

## Hauptversorgung

50 Ah LiFePO4

geschützt durch:

- intAct Battery Guard

Überwachung:

- INA226

## Dauerhaft aktiv

- Xmini Wächter

## Bei Bedarf aktiv

- Raspberry Pi
- Home Assistant
- TP-Link WR3602BE
- TP-Link M7350
- Ami-Fahr ESP
- Lepy

## Rückfahrsystem

Aktivierung über den Ami-Fahr ESP.

Fahrstufe R wird über WiCAN erkannt.

Dann wird die Heckversorgung aktiviert.

Verbraucher:

- Rückfahrkamera
- Rückfahrscheinwerfer
- Parksensoren
- Heck-ESP

---

# Netzwerk

## Lokales Bordnetz

TP-Link WR3602BE

Aufgaben:

- WLAN im Fahrzeug
- Kommunikation zwischen ESPs
- Home Assistant Netzwerk

## Mobiles Internet

TP-Link M7350

Aufgaben:

- Internetzugang unterwegs
- Tailscale
- Updates
- Fernzugriff

Geplante Steuerung:

- SwitchBot Bot (Power-Taste)

---

# Home Assistant

Aufgaben:

- Dashboard
- Fahrzeugstatus
- Energieüberwachung
- Automationen
- ESPHome
- Tailscale

Der Raspberry Pi ist ein Komfortsystem und nicht fahrzeugkritisch.

---

# Ami-Fahr ESP

Aufgaben:

- Fahrzeuglogik
- Nextion-Ansteuerung
- IR-Steuerung
- Rückfahrlogik
- Dashcam-Steuerung

Versorgung über MP1584 Step-Down-Wandler.

---

# Rückfahrsystem

Bestandteile:

- Heck-ESP
- Parksensoren
- Buzzer
- Rückfahrkamera
- Rückfahrscheinwerfer

Die Parksensoren sollen zusätzlich auf dem Nextion dargestellt werden.

---

# Audio

Signalweg:

CarPlay Display
→ 3,5 mm Line Out
→ Lepy LP-269S
→ Lautsprecher

Geplante Steuerung über IR.

---

# Ambientebeleuchtung

Originalcontroller bleibt erhalten.

Steuerung über IR:

- KY-022 IR-Empfänger
- KY-005 IR-Sender

Dadurch bleiben die originalen Effekte und Modi erhalten.

---

# Sprachsteuerung

## Siri

- Navigation
- Musik
- Telefonie
- CarPlay

## Alexa (Echo Pop)

- Home Assistant Sprachinterface
- Fahrzeugstatus
- Automationen
- Statusabfragen

## Home Assistant Voice

Mögliches späteres Ausbauprojekt.

---

# Hardwarestatus

Vorhanden:

- WiCAN
- Raspberry Pi
- Nextion
- ESP32
- ESP32-C3
- Lepy LP-269S
- 50 Ah LiFePO4
- Battery Guard
- WR3602BE
- M7350
- Echo Pop
- 70mai Dashcam

Bestellt:

- INA226
- MP1584 Module
- KY-005
- KY-022
- Lochrasterplatinen
- Abstandshalter
- Widerstands- und Kondensatorsortiment

---

# Nächste Schritte

1. INA226 integrieren
2. WiCAN einrichten
3. Fahrstufe R identifizieren
4. Rückfahrsystem aufbauen
5. Nextion Rückfahransicht erstellen
6. Router- und Tailscale-Konzept finalisieren
7. Home Assistant Dashboards erstellen
