C4-Diagramme – Flowline

Dieses Dokument enthält die C4-System- und Container-Diagramme für Flowline in stabiler Markdown-Form.
Die Diagramme sind konsistent zu overview.md (ADR 0001 & 0002) und spiegeln exakt die dort festgelegten Architekturprinzipien wider.

⸻

C4 – Level 1: System Context

flowchart LR
    Operator[Person: Operator]
    Supervisor[Person: Supervisor / Admin]

    Flowline[System: Flowline\nFehlervermeidende Prozessplattform\nPoka-Yoke\nDeterministische Ablaufsteuerung]

    Automation[External System: Automatisierungsebene\nSPS / Maschinen\nSensorik & Aktorik]
    IT[External System: IT-Systeme\nERP / MES / QM]

    Operator -->|führt Arbeitsschritte aus| Flowline
    Supervisor -->|konfiguriert & überwacht| Flowline

    Flowline -->|Befehle / Status| Automation
    Flowline -->|Prozessdaten| IT


⸻

C4 – Level 2: Container

flowchart TB
    Operator[Person: Operator]
    Supervisor[Person: Supervisor / Admin]

    subgraph Flowline[System: Flowline]
        UI[Container: UI\nGeführte Bedienung\nKeine Prozesslogik]
        Runtime[Container: Runtime\nDeterministische State Machine\nPoka-Yoke Enforcement]
        Integrations[Container: Integrationen\nAdapter Layer\nKeine Fachlogik]
        Config[Container: Konfiguration\nFlows / Steps / Regeln]
        Audit[Container: Audit & Logs\nZustände / Übergänge]
    end

    Automation[External System: Automatisierungsebene]
    IT[External System: IT-Systeme]

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


⸻

Architekturregeln (aus ADR 0001 & 0002)
	•	Die Runtime ist die einzige Instanz mit Prozess- und Entscheidungslogik
	•	Geführte Workflows sind Bestandteil der Runtime (Poka-Yoke)
	•	UI ist rein darstellend und reaktiv
	•	Integrationen adaptieren Technik, treffen aber keine Entscheidungen
	•	Audit & Logs sind verpflichtend für Nachvollziehbarkeit

⸻

Dieses Dokument ist Teil der offiziellen Architektur-Dokumentation von Flowline.
Erstellt mit Unterstützung von ChatGPT und geprüft durch die Projektverantwortlichen.