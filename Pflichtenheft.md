# Pflichtenheft – Performance-Test Siemens S7

## Projektbezeichnung
Performance-Test verschiedener Technologien zur Kommunikation mit einer Siemens S7 Industriesteuerung

## Projektteam
- Team: 5AHIT
- Mitglieder: Philipp Wurm, Markus Strohmaier

## Zielsetzung
Untersuchung der Performance unterschiedlicher Kommunikationsprotokolle für Siemens S7, insbesondere:

1. Hochfrequentes Schreiben einzelner Variablen (Bool, Int16, Int32)
2. Übertragung größerer Datenmengen (~1 kByte)

**Protokolle:**
- Siemens Web API
- OPC UA
- Proprietäres S7-Protokoll (Snap7)

---

## Anforderungen

### Funktionale Anforderungen
1. **Web API Kommunikation**
   - Hochfrequentes Schreiben einzelner Variablen
   - Lesen/Werteänderung prüfen
   - Latenz und Durchsatz messen

2. **OPC UA Kommunikation**
   - Hochfrequentes Schreiben einzelner Variablen über OPC UA Server
   - Latenz messen
   - Verbindung zum OPC UA Server herstellen / trennen

3. **Snap7 (proprietäres S7-Protokoll)**
   - Hochfrequentes Schreiben von Datenblöcken (~1 kByte)
   - DB-Nummer, Startadresse und Größe anpassbar
   - Latenzmessung pro Schreibvorgang

4. **Datenaufzeichnung**
   - Speicherung der Latenzwerte in CSV-Dateien
   - Erstellung von Diagrammen zur Visualisierung (Matplotlib)

5. **Konfigurierbarkeit**
   - SPS-IP, Rack, Slot, Node-IDs, DB-Nummer und Testvariablen müssen leicht anpassbar sein

### Nicht-funktionale Anforderungen
- Python 3.10+
- Plattformunabhängig (Windows/Linux)
- Wiederverwendbarkeit und Erweiterbarkeit des Codes
- Lesbarkeit und Dokumentation der Software

---

## Umsetzung

### Technischer Ansatz
1. **Architektur**
   - Python-basierte Testskripte
   - Klassenstruktur für Web API (`sps_api.py`)
   - Funktionen für OPC UA und Snap7 Hochfrequenztests
   - Ergebnisse automatisch in `results/` (CSV)
   - Plots in `plots/`

2. **Testskript (`highfreq_test.py`)**
   - Drei Hauptfunktionen:
     - `run_webapi_test()`
     - `run_opcua_test()`
     - `run_snap7_test()`
   - Jede Funktion misst Zeit pro Schreibvorgang und speichert die Werte
   - Plots werden automatisch erstellt

3. **Bibliotheken**
   - `requests` → Web API Kommunikation
   - `opcua` → OPC UA Client
   - `python-snap7` → Snap7 Client
   - `matplotlib` → Diagramme
   - `csv` → Speicherung von Messdaten

4. **Testvariablen**
   - Bool, Int16, Int32
   - Datenblock ~1 kByte für Snap7
   - Anpassbare Iterationen (z. B. 100 pro Test)

5. **Ordnerstruktur**
```

S7_PerformanceTest_Complete/
├── README.md
├── requirements.txt
├── sps_api.py
├── highfreq_test.py
├── results/   # CSV-Dateien
└── plots/     # Diagramme

````

---

### Durchführung
1. Installieren der Abhängigkeiten:
```bash
pip install -r requirements.txt
````

2. SPS-Parameter, Node-IDs und DB-Nummern in `highfreq_test.py` anpassen
3. Test starten:

```bash
python highfreq_test.py
```

4. Ergebnisse in CSV und Diagrammen überprüfen

---

### Ergebnis

* Vergleich der Latenzen und Durchsatzraten zwischen Web API, OPC UA und Snap7
* Visualisierung der Performance pro Variable und Protokoll
* Dokumentation der Erkenntnisse für Präsentation

---

### Anhang

* Tabellen für Testvariablen und Parameter
* Hinweise zur Anpassung der SPS-Parameter
* Hinweise zu Variablenarten (Bool, Int16, Int32)
* Messmethodik: Min/Max/Durchschnitt pro Test

```
```
