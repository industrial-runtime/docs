

# Pflichtenheft – Flowline  
Version 1.0

---

## 1. Einleitung

### 1.1 Ziel des Dokuments

Dieses Pflichtenheft beschreibt die **konkrete fachlich‑technische Umsetzung**
der im Lastenheft definierten Anforderungen für das System **Flowline**.

Es beantwortet die Frage **„Wie wird das System die Anforderungen erfüllen?“**
und dient als verbindliche Grundlage für Design, Implementierung, Tests
und Abnahme.

### 1.2 Bezug zum Lastenheft

Dieses Dokument basiert auf:

- `docs/02_requirements/lastenheft/lastenheft_v1.md`

Alle Anforderungen dieses Pflichtenhefts sind **ableitbar und rückverfolgbar**
auf das Lastenheft. Abweichungen sind explizit zu begründen.

### 1.3 Begriffe und Abkürzungen

- **Flowline Runtime**  
  Ausführungskomponente zur deterministischen Prozesssteuerung.

- **Flow**  
  Ein modellierter Prozessablauf bestehend aus Zuständen, Übergängen und Regeln.

- **Step**  
  Atomarer Arbeitsschritt innerhalb eines Flows.

- **Poka‑Yoke**  
  Fehlervermeidung durch Systemdesign und erzwungene Korrektheit.

---

## 2. Systemübersicht

### 2.1 Systemkontext

Flowline ist eine modulare, verteilte Prozessplattform zur Ausführung
geführter industrieller Workflows.

Das System besteht logisch aus:

- **Runtime** (Ablaufsteuerung)
- **User Interface** (Bedienerführung)
- **Integrationen** (Anbindung externer Systeme und Hardware)
- **Dokumentation & Konfiguration**

### 2.2 Abgrenzung

Dieses Pflichtenheft beschreibt **keine**:
- konkrete Hardware
- spezifischen Feldbusse
- kundenspezifischen Geräteimplementierungen

---

## 3. Fachliche Architektur

### 3.1 Grundprinzip

Flowline folgt einem **deterministischen, zustandsbasierten Ausführungsmodell**.

- Jeder Flow besteht aus expliziten Zuständen
- Übergänge sind eindeutig definiert
- Ungültige Zustandswechsel sind systemisch ausgeschlossen
- Prozesslogik ist unabhängig von UI und Integrationen

### 3.2 Prozessmodell

Ein Prozess (Flow) besteht aus:

- eindeutig identifizierbaren Steps
- vordefinierten Start‑ und Endzuständen
- validierten Übergängen
- optionalen Fehler‑ und Abbruchpfaden

---

## 4. Funktionale Umsetzung der Anforderungen

### 4.1 Ablaufsteuerung (Runtime)

Die Runtime muss:

- Flows laden, validieren und ausführen
- nur gültige Steps aktivieren
- automatische und manuelle Übergänge unterstützen
- Abbrüche, Wiederholungen und Fehlerfälle explizit behandeln
- deterministisches Verhalten garantieren

### 4.2 Poka‑Yoke‑Mechanismen

Das System muss:

- ungültige Aktionen technisch verhindern
- Eingaben vor Zustandswechseln validieren
- Abhängigkeiten zwischen Steps erzwingen
- Korrektheit vor Fortschritt priorisieren

### 4.3 Bedienerführung

Die UI muss:

- den aktuellen Step eindeutig anzeigen
- erlaubte Aktionen klar hervorheben
- nicht erlaubte Aktionen blockieren
- den nächsten gültigen Schritt führen

### 4.4 Inklusion und geführte Ausführung

Die Umsetzung muss sicherstellen:

- Reduktion kognitiver Last durch klare Schrittführung
- keine impliziten Entscheidungen durch Bediener
- visuelle und strukturelle Unterstützung bei jeder Aktion

---

## 5. Daten, Zustände und Nachvollziehbarkeit

### 5.1 Zustandsverwaltung

- Jeder Flow‑Zustand ist explizit repräsentiert
- Zustandswechsel sind nachvollziehbar
- Der aktuelle Zustand ist jederzeit eindeutig bestimmbar

### 5.2 Protokollierung

Das System muss:

- relevante Zustandswechsel protokollieren
- Abweichungen und Fehler dokumentieren
- eine spätere Analyse ermöglichen

---

## 6. Nicht‑funktionale Umsetzung

### 6.1 Determinismus

- gleiche Eingaben → gleiches Verhalten
- keine zeitabhängigen Seiteneffekte
- reproduzierbare Abläufe

### 6.2 Wartbarkeit

- klare Modulgrenzen
- austauschbare Komponenten
- testbare Einheiten

### 6.3 Erweiterbarkeit

- neue Steps ohne Änderung bestehender Flows
- neue Integrationen ohne Einfluss auf die Runtime

---

## 7. Tests und Verifikation

Das System muss unterstützen:

- Unit‑Tests für Prozesslogik
- Simulation von Flows ohne reale Hardware
- reproduzierbare Testläufe

---

## 8. Abnahmekriterien

Ein Flowline‑System gilt als konform, wenn:

- alle Lastenheft‑Anforderungen erfüllt sind
- keine ungültigen Zustandswechsel möglich sind
- Prozessausführung vollständig nachvollziehbar ist
- geführte Ausführung Fehler systemisch verhindert

---

## 9. Ausblick

Dieses Pflichtenheft bildet die Grundlage für:

- detaillierte Architekturentscheidungen (ADRs)
- konkrete Implementierungsrichtlinien
- modulare Repository‑Struktur