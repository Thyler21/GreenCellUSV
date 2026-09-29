# GreenCellUSV 0.3.1 installieren

## Installation

1. In LoxBerry **Pluginverwaltung → Plugin installieren** öffnen.
2. Die Datei `GreenCellUSV-0.3.1.zip` hochladen und installieren.
3. Danach **GreenCellUSV** im LoxBerry-Menü öffnen.

Für die Installation ist kein SSH-Root- oder sudo-Passwort nötig. Die
Pluginverwaltung führt die notwendigen Installationsschritte selbst aus.

## Grundeinstellung

Das Plugin startet mit den bereits ermittelten Daten:

- Modell: GreenCell PowerProof 600 VA / 360 W
- Batterie: AGM, 12 V, 7,2 Ah
- Messintervall: 10 Sekunden
- MQTT: aktiviert
- Basistopic: `loxberry/greencellusv`

Nach Änderungen auf **Einstellungen speichern** drücken. Die laufende
Erfassung übernimmt sie spätestens beim nächsten Messintervall.

## MQTT-Werte für Loxone

Die Werte werden als retained Messages über das vorhandene LoxBerry MQTT
Gateway gesendet. Besonders nützlich sind:

| Topic | Inhalt |
|---|---|
| `loxberry/greencellusv/mode` | `mains`, `battery`, `battery_low` oder `offline` |
| `loxberry/greencellusv/battery_low` | `0` oder `1` |
| `loxberry/greencellusv/battery_charge_percent` | geschätzte Kapazität in Prozent |
| `loxberry/greencellusv/battery_runtime_minutes` | geschätzte Restlaufzeit |
| `loxberry/greencellusv/load_percent` | USV-Auslastung |
| `loxberry/greencellusv/input_voltage` | Eingangsspannung |
| `loxberry/greencellusv/output_voltage` | Ausgangsspannung |
| `loxberry/greencellusv/battery_voltage` | Batteriespannung |
| `loxberry/greencellusv/state` | alle Werte als JSON |

## Bedeutung der Anzeige

- **Netzbetrieb:** Netzspannung vorhanden.
- **Notstrombetrieb:** Die USV versorgt die Geräte aus der Batterie.
- **Batterie kritisch:** Die USV hat das schnelle Warnsignal und das
  Low-Battery-Bit gemeldet.

Kapazität und Laufzeit sind Schätzwerte. Das Gerät überträgt Spannung und
Last, aber keine verlässliche Prozent- oder Laufzeitangabe.

Das vorhandene APC-USV-Plugin und `/etc/nut/ups.conf` werden nicht verändert.
