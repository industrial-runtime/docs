# C4-Diagramme – Flowline

Dieses Dokument enthält die **C4-System- und Container-Diagramme** für Flowline in stabiler Markdown-Form.
Die Diagramme sind konsistent zu `overview.md` (ADR 0001 & ADR 0002) und spiegeln exakt die dort festgelegten Architekturprinzipien wider.

---

## C4 – Level 1: System Context

```mermaid
flowchart LR
    Operator["Person: Operator"]
    Supervisor["Person: Supervisor / Admin"]

    Flowline["System: Flowline<br/>Fehlervermeidende Prozessplattform<br/>Poka-Yoke<br/>Deterministische Ablaufsteuerung"]

    Automation["External System: Automatisierungsebene<br/>SPS / Maschinen<br/>Sensorik & Aktorik"]
    IT["External System: IT-Systeme<br/>ERP / MES / QM"]

    Operator -->|führt Arbeitsschritte aus| Flowline
    Supervisor -->|konfiguriert & überwacht| Flowline

    Flowline -->|Befehle / Status| Automation
    Flowline -->|Prozessdaten| IT
```

---

## C4 – Level 2: Container

```mermaid
flowchart TB
    Operator["Person: Operator"]
    Supervisor["Person: Supervisor / Admin"]

    subgraph Flowline["System: Flowline"]
        UI["Container: UI<br/>Geführte Bedienung<br/>Keine Prozesslogik"]
        Runtime["Container: Runtime<br/>Deterministische State Machine<br/>Poka-Yoke Enforcement"]
        Integrations["Container: Integrationen<br/>Adapter Layer<br/>Keine Fachlogik"]
        Config["Container: Konfiguration<br/>Flows / Steps / Regeln"]
        Audit["Container: Audit & Logs<br/>Zustände / Übergänge"]
    end

    Automation["External System: Automatisierungsebene"]
    IT["External System: IT-Systeme"]

    Operator --> UI
    Supervisor --> Config

    UI -->|erlaubte Aktionen| Runtime
    Runtime -->|aktueller Zustand| UI

    Config -->|Prozessmodelle| Runtime
    Runtime -->|Audit Events| Audit

    Runtime -->|Kommandos| Integrations
    Integrations -->|Status| Runtime

    Integrations --> Automation
    Integrations --> IT
```

---

## Architekturregeln (aus ADR 0001 & ADR 0002)

- Die **Runtime** ist die einzige Instanz mit Prozess- und Entscheidungslogik.
- **Geführte Workflows** sind Bestandteil der Runtime (Poka-Yoke).
- Die **UI** ist rein darstellend und reaktiv.
- **Integrationen** adaptieren Technik, treffen aber keine Entscheidungen.
- **Audit & Logs** sind verpflichtend für Nachvollziehbarkeit.

---

Dieses Dokument ist Teil der offiziellen Architektur-Dokumentation von Flowline.  
Erstellt mit Unterstützung von ChatGPT und geprüft durch die Projektverantwortlichen.