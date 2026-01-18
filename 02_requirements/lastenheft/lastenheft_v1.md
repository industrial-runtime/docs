

# Lastenheft – Flowline  
Version 1.0

---

## 1. Einleitung

### 1.1 Ziel des Dokuments

Dieses Lastenheft beschreibt die **fachlichen und nicht‑funktionalen Anforderungen**
an das System **Flowline** aus Sicht des Auftraggebers bzw. der Anwender.

Es beantwortet bewusst die Frage **„Was soll das System leisten?“**  
Die konkrete technische Umsetzung ist **nicht** Bestandteil dieses Dokuments
und wird im Pflichtenheft beschrieben.

### 1.2 Ziel des Systems

Ziel von Flowline ist es, industrielle Arbeits‑ und Prüfprozesse so zu unterstützen,
dass **Fehler durch Systemdesign vermieden werden** (Poka‑Yoke‑Prinzip),
anstatt sie lediglich zu erkennen oder zu tolerieren.

Flowline soll:

- geführte, validierte und nachvollziehbare Prozessabläufe ermöglichen
- Bedienfehler systemisch verhindern
- neue oder unerfahrene Arbeitskräfte schnell produktiv einsetzbar machen
- Menschen mit körperlichen oder kognitiven Einschränkungen
  die Teilnahme an Produktionsprozessen ermöglichen
- Prozesswissen dauerhaft im System verankern

### 1.3 Begriffe und Definitionen

- **Flowline**  
  Plattform zur Definition, Ausführung und Überwachung geführter industrieller Prozessabläufe.

- **Poka‑Yoke**  
  Prinzip der Fehlervermeidung durch Gestaltung von Prozessen und Systemen,
  sodass fehlerhafte Handlungen verhindert oder unmittelbar erkannt werden.

- **Arbeitsstation**  
  Ein physischer Arbeitsplatz (z. B. Montage‑ oder Prüfplatz), an dem ein Prozess ausgeführt wird.

- **Prozess / Ablauf**  
  Eine definierte Folge von Arbeitsschritten mit klaren Zuständen, Übergängen und Validierungen.

---

## 2. Ausgangssituation

In vielen industriellen Umgebungen sind Prozesse:

- implizit dokumentiert
- stark vom Erfahrungswissen einzelner Personen abhängig
- fehleranfällig bei Personalwechsel oder Anlernphasen
- schwer auditierbar und nur eingeschränkt reproduzierbar

Bestehende Systeme reagieren häufig **erst nach Auftreten eines Fehlers**
oder verlassen sich auf organisatorische Maßnahmen (Schulung, Erfahrung),
statt Fehler systemisch zu vermeiden.

---

## 3. Gesamtübersicht des Systems

Flowline ist als **zentrale Prozessplattform** konzipiert, die:

- Prozesslogik von konkreter Hardware entkoppelt
- mehrere Arbeitsstationen koordiniert
- Bediener aktiv durch Abläufe führt
- Status, Ergebnisse und Abweichungen dokumentiert

Das System besteht aus mehreren logisch getrennten Komponenten
(z. B. Runtime, Benutzeroberfläche, Integrationen),
deren konkrete Ausgestaltung **nicht** Teil dieses Lastenhefts ist.

---

## 4. Funktionale Anforderungen

### 4.1 Prozessführung und Ablaufsteuerung

Das System soll:

- die Definition strukturierter Prozessabläufe ermöglichen
- Arbeitsschritte explizit modellieren (Zustände, Übergänge, Bedingungen)
- nur gültige Prozessschritte zulassen
- falsche oder unzulässige Aktionen verhindern
- manuelle und automatische Übergänge unterstützen
- Abbrüche, Wiederholungen und Fehlerfälle explizit behandeln

### 4.2 Poka‑Yoke und Fehlervermeidung

Flowline muss:

- fehlerhafte Prozesszustände systemisch ausschließen
- Abhängigkeiten zwischen Schritten prüfen
- Eingaben und Aktionen validieren
- den Bediener aktiv auf den korrekten nächsten Schritt führen
- Abweichungen eindeutig erkennen und dokumentieren

### 4.3 Bedienerführung und Usability

Das System soll:

- klare, verständliche Arbeitsanweisungen anzeigen
- visuelle Unterstützung (z. B. Bilder, Hinweise) ermöglichen
- eine einfache und reduzierte Benutzeroberfläche bieten
- ohne tiefgehende Schulung bedienbar sein
- unterschiedliche Qualifikationsniveaus berücksichtigen

### 4.4 Inklusion und Zugänglichkeit

Flowline soll so gestaltet sein, dass:

- Tätigkeiten in klar abgegrenzte, geführte Schritte zerlegt sind
- kognitive Belastung durch implizite Entscheidungen reduziert wird
- Menschen mit Einschränkungen produktiv eingesetzt werden können
- Assistenz‑ und Führungssysteme Fehler vermeiden helfen

Der Fokus liegt dabei auf **Systemgestaltung**, nicht auf Personalisierung.

### 4.5 Einsatz neuer Arbeitskräfte

Das System soll:

- einen direkten Einsatz neuer oder unerfahrener Mitarbeiter ermöglichen
- Prozesswissen explizit bereitstellen
- Abhängigkeit von individueller Erfahrung reduzieren
- Anlernzeiten verkürzen
- reproduzierbare Qualität sicherstellen

### 4.6 Nachvollziehbarkeit und Dokumentation

Flowline muss:

- Prozessausführungen nachvollziehbar dokumentieren
- relevante Zustände und Übergänge protokollieren
- eine spätere Analyse und Auditierung ermöglichen
- Transparenz über Prozessfortschritt und Ergebnisse schaffen

---

## 5. Nicht‑funktionale Anforderungen

### 5.1 Zuverlässigkeit

- deterministische Prozessausführung
- reproduzierbares Verhalten
- konsistente Zustandsverwaltung

### 5.2 Benutzbarkeit

- klare, reduzierte Benutzerführung
- eindeutige Rückmeldungen
- Vermeidung von Fehlbedienung

### 5.3 Wartbarkeit und Erweiterbarkeit

- modulare Struktur
- klare Abgrenzung von Verantwortlichkeiten
- Erweiterbarkeit ohne Anpassung bestehender Prozesse

### 5.4 Sicherheit und Kontrolle

- kontrollierter Zugriff auf Funktionen
- Schutz vor unbeabsichtigten Aktionen
- klare Verantwortlichkeiten im System

---

## 6. Abgrenzung (Nicht‑Ziele)

Flowline soll **nicht**:

- eine klassische SPS ersetzen
- gerätespezifische Logik enthalten
- implizite oder unkontrollierte Abläufe zulassen
- Fehler lediglich tolerieren oder kaschieren
- als monolithisches All‑in‑One‑System fungieren

---

## 7. Rahmenbedingungen

- Einsatz in industriellen Produktions‑ und Prüfbereichen
- Nutzung an stationären Arbeitsplätzen
- Integration in bestehende IT‑ und Automatisierungslandschaften möglich
- langfristige Wartbarkeit und Erweiterbarkeit erforderlich

---

*Dieses Lastenheft beschreibt den fachlichen Rahmen für Flowline.
Die konkrete technische Umsetzung wird im Pflichtenheft spezifiziert.*