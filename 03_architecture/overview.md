# Architektur-Übersicht – Flowline

---

## 1. Zweck dieses Dokuments

Dieses Dokument beschreibt die **architektonische Gesamtstruktur** von Flowline
und enthält zugleich die **verbindlichen Architekturentscheidungen**.

Es beantwortet die Fragen:

- Wie ist Flowline grundsätzlich aufgebaut?
- Welche Architekturprinzipien sind verbindlich?
- Warum wurden diese Entscheidungen getroffen?
- Welche Konsequenzen ergeben sich daraus?

Dieses Dokument ersetzt einzelne ADR-Dateien und dient als **zentrale,
dauerhafte Referenz** für Architekturentscheidungen.

---

## 2. Kontext und Zielsetzung

Flowline ist eine industrielle Prozessplattform zur **fehlervermeidenden
(Poka-Yoke) Ausführung geführter Arbeits- und Prüfprozesse**.

Zentrale Ziele sind:

- Fehler **systemisch verhindern**, nicht tolerieren
- deterministische und reproduzierbare Prozessausführung
- geführte Arbeitsabläufe statt freier Bedienung
- Reduktion kognitiver Last
- schneller Einsatz neuer oder unerfahrener Arbeitskräfte
- Inklusion durch Systemgestaltung
- vollständige Nachvollziehbarkeit und Auditierbarkeit

Flowline ersetzt **keine SPS**, sondern ergänzt bestehende
Automatisierungs- und IT-Systeme durch strukturierte Ablaufsteuerung
und Bedienerführung.

---

## 3. Systemeinordnung

Flowline agiert **oberhalb** klassischer Automatisierungssysteme:

- keine Echtzeit-Maschinensteuerung
- keine hardwarenahe Regelung
- keine gerätespezifische Logik

Stattdessen übernimmt Flowline:

- Orchestrierung von Prozessabläufen
- Validierung von Arbeitsschritten
- Führung des Bedieners
- Dokumentation von Prozessausführung

---

## 4. Logische Hauptkomponenten

### 4.1 Runtime (Ablaufsteuerung)

Die Runtime ist das **zentrale Systemelement**.

Verantwortlichkeiten:

- Laden und Validieren von Prozessen
- Ausführen deterministischer Zustandsmodelle
- Erzwingen gültiger Zustandsübergänge
- Umsetzung von Poka-Yoke-Mechanismen
- Verwaltung des aktuellen Prozesszustands
- Protokollierung relevanter Ereignisse

Die Runtime kennt:

- **keine Benutzeroberfläche**
- **keine konkrete Hardware**

---

### 4.2 Benutzeroberfläche (UI)

Die Benutzeroberfläche ist verantwortlich für:

- Darstellung des aktuellen Prozesszustands
- Anzeige von Arbeitsanweisungen
- Hervorhebung erlaubter Aktionen
- Rückmeldung von Benutzeraktionen an die Runtime

Die UI:

- trifft **keine fachlichen Entscheidungen**
- enthält **keine Prozesslogik**
- spiegelt ausschließlich den Zustand der Runtime wider

---

### 4.3 Integrationen

Integrationen binden externe Systeme an, z. B.:

- Hardware
- Sensorik / Aktorik
- IT-Systeme

Integrationen:

- setzen Befehle um
- liefern Statusinformationen
- enthalten **keine fachliche Logik**
- beeinflussen den Prozess nur über definierte Schnittstellen

---

### 4.4 Konfiguration und Dokumentation

- Prozessdefinitionen
- Validierungsregeln
- Audit- und Protokolldaten
- Nachvollziehbarkeit von Abläufen

---

## 5. Architekturentscheidungen (ADR 0001)

### 5.1 Deterministische, zustandsbasierte Ablaufsteuerung

Alle Prozesse werden als **explizite Zustandsmodelle** beschrieben.

- Jeder Zustand ist eindeutig definiert
- Übergänge sind explizit modelliert
- Ungültige Übergänge sind technisch ausgeschlossen
- Gleiche Eingaben führen immer zum gleichen Ergebnis

**Begründung:**  
Determinismus ist Voraussetzung für Fehlervermeidung,
Testbarkeit und Auditierbarkeit.

---

### 5.2 Poka-Yoke als architektonisches Kernprinzip

Poka-Yoke ist ein **Domänenprinzip**, kein UI-Feature.

- Fortschritt ist nur bei erfüllten Bedingungen möglich
- Korrektheit wird vom System erzwungen
- Fehler werden nicht toleriert oder kaschiert
- Bediener können keine ungültigen Aktionen auslösen

**Begründung:**  
Fehlervermeidung muss durch Architektur erzwungen werden,
nicht durch Schulung oder Erfahrung.

---

### 5.3 Geführte Workflows statt freier Bedienung

Flowline setzt konsequent auf **geführte Arbeitsabläufe**:

- Das System zeigt immer den aktuellen, gültigen Schritt
- Nur erlaubte Aktionen sind verfügbar
- Der nächste Schritt ist eindeutig vorgegeben
- Implizite Entscheidungen werden vermieden

**Begründung:**  
Geführte Workflows reduzieren Fehler, senken kognitive Last
und ermöglichen Inklusion sowie schnellen Personaleinsatz.

---

### 5.4 Strikte Trennung von Verantwortlichkeiten

Flowline trennt strikt zwischen:

- Prozesslogik (Runtime)
- Darstellung und Interaktion (UI)
- Technischer Anbindung (Integrationen)

- Prozesslogik existiert ausschließlich in der Runtime
- UI und Integrationen reagieren auf Zustände, steuern sie aber nicht frei

**Begründung:**  
Diese Trennung ist Voraussetzung für Wartbarkeit,
Testbarkeit und langfristige Erweiterbarkeit.

---

### 5.5 Explizite Modellierung statt impliziter Logik

Flowline erlaubt **keine implizite Logik**:

- keine versteckten Seiteneffekte
- keine impliziten Zustände
- keine fachlichen Entscheidungen außerhalb der Runtime

**Begründung:**  
Implizite Logik ist nicht testbar, nicht nachvollziehbar
und widerspricht dem Ziel der Fehlervermeidung.

---

### 5.6 Simulation und Testbarkeit als Pflicht

Jeder Prozess muss:

- ohne reale Hardware ausführbar sein
- simulierbar und reproduzierbar getestet werden können
- vor Inbetriebnahme validiert werden

Simulation ist ein **gleichwertiger Ausführungsmodus**.

**Begründung:**  
Nur testbare Prozesse sind sichere Prozesse.

---

### 5.7 Geführte Workflows als eigenständiger Poka-Yoke-Mechanismus (ADR 0002)

Geführte Workflows stellen in Flowline einen **eigenständigen, verbindlichen
Poka-Yoke-Mechanismus** dar und sind nicht lediglich eine Darstellungs- oder
Usability-Eigenschaft der Benutzeroberfläche.

#### Entscheidung

Flowline implementiert geführte Workflows als **Bestandteil der fachlichen
Prozesslogik** innerhalb der Runtime.

Dies bedeutet:

- Der aktuell gültige Prozessschritt ist jederzeit eindeutig definiert
- Nur explizit erlaubte Aktionen sind pro Schritt möglich
- Der Übergang zum nächsten Schritt ist systemisch validiert
- Die Reihenfolge der Schritte ist nicht durch den Bediener beeinflussbar
- UI und Integrationen können keine freien Zustandswechsel auslösen

#### Begründung

Geführte Workflows sind ein zentrales Mittel zur Fehlervermeidung, da sie:

- implizite Entscheidungen durch den Bediener eliminieren
- kognitive Belastung reduzieren
- Abhängigkeiten zwischen Arbeitsschritten erzwingen
- Fehlbedienung systemisch verhindern
- reproduzierbare Qualität sicherstellen

Insbesondere ermöglichen sie:

- den direkten Einsatz neuer oder unerfahrener Arbeitskräfte
- die Einbindung von Personen mit körperlichen oder kognitiven Einschränkungen
- gleichbleibende Prozessqualität unabhängig von individueller Erfahrung

#### Konsequenzen

Durch diese Entscheidung gilt:

- Prozesslogik definiert die Führung, nicht die UI
- Abweichungen vom Prozess sind technisch ausgeschlossen
- Schulung ersetzt nicht Systemgestaltung
- Fehlervermeidung ist eine Eigenschaft des Systems, nicht des Benutzers

---

## 6. Konsequenzen der Architektur

### Positive Effekte

- hohe Prozesssicherheit
- reproduzierbares Verhalten
- klare Verantwortlichkeiten
- gute Auditierbarkeit
- saubere Erweiterbarkeit

### Bewusste Einschränkungen

- höherer Modellierungsaufwand
- weniger ad-hoc-Flexibilität
- strikte Architekturdisziplin erforderlich

Diese Einschränkungen werden bewusst akzeptiert,
um Qualität und Fehlervermeidung sicherzustellen.

---

## 7. Abgrenzung

Dieses Dokument trifft **keine Entscheidungen** zu:

- Programmiersprachen
- Frameworks
- Protokollen
- Hardware
- Deployment

Diese Aspekte werden bei Bedarf in separaten Dokumenten ergänzt.

---

## 8. Beziehung zu anderen Dokumenten

- Lastenheft: fachliche Anforderungen
- Pflichtenheft: fachlich-technische Umsetzung
- Dieses Dokument: verbindliche Architekturgrundlage