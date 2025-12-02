# legalaid-documentation
LegalAId - KI-gestützte Rechtsberatung für Geflüchtete. Enthält Dokumentation, Workflow-Diagramme und lokale Installationsanleitungen. Open Source (MIT/Apache 2.0).
# LegalAId - Open-Source Legal-RAG für barrierefreie Migrationsrechtsberatung

## Projektmission

LegalAId ist ein **offenes, kostenloses Software-Framework** für KI-gestützte Rechtsberatung im Migrationsrecht. Wir ermöglichen **Berater:innen von NGOs, Refugee Law Clinics und Flüchtlingsberatungsstellen**, Geflüchtete systematisch auf Behördentermine vorzubereiten – mit **vertrauenswürdiger Technologie, ohne Cloud-Abhängigkeit**.

### Was uns wichtig ist
- **Open Source & kostenlos** - keine Lizenzgebühren, selbst-hostbar
- **Vertrauenswürdig** - 5-Layer Quality Assurance gegen Halluzinationen  
- **Barrierefrei** - WCAG 2.1 AA, 10 Sprachen, Offline-First
- **Datenschutzkonform** - lokal offline (Qwen 2.5 7B), keine Cloud-Abhängigkeit
- **Nutzer:innen-zentriert** - Human-in-the-Loop, Berater:innen-Dashboard

---

## Die Herausforderung

### Das Problem in Deutschland
- **800+ NGOs** beraten jährlich **hunderttausende Geflüchtete** im Migrationsrecht
- **Sprachbarrieren**: 40-60% sprechen kein Deutsch, professionelle Dolmetschung kostet 80-150€/Std
- **Terminausfälle**: 30-40% scheitern wegen fehlender Dokumente → Monate Verzögerung
- **Wissensmonopol**: Rechtsdatenbanken kosten 60-200€/Monat (Beck-Online, Juris)
- **Überlastung**: 350.000+ Asylanträge 2024, Behörden & Beratungsstellen am Limit

### Warum die Lage kritisch ist
- Fachkräfteeinwanderungsgesetz (März 2024) + EU-Asylreform = neue Rechtsunsicherheit
- NGOs arbeiten oft mit veralteter Rechtskenntnis
- Manuelle Dokumentenprüfung benötigt Zeit, die aber nicht verfügbar ist

---

## Die LegalAId-Lösung

### Was macht LegalAId?

**LegalAId ist eine Progressive Web App (PWA), die:**

1. **Dokumentation systematisiert** 
   - Automatische Checklisten für erforderliche Dokumente
   - Pausierbare Workflows für unterbrechungsfreie Beratung

2. **Sprachbarrieren überbrückt**
   - Whisper.js (lokale Spracherkennung im Browser)
   - 10 Sprachen: Arabisch, Türkisch, Farsi, Ukrainisch, Russisch, Somalisch, Albanisch, Serbisch, Tigrinya, Englisch

3. **Rechtswissen demokratisiert**
   - Legal-RAG (Retrieval Augmented Generation)
   - Zugriff auf BVerwG-Urteile, Gesetzestexte, Verwaltungsanweisungen
   - Hybrid Search: semantisch (Vector DB) + lexikalisch (BM25)

4. **Vertrauen durch Qualitätssicherung**
   - Layer 1: Context Engineering (nur aus belegbaren Quellen, nicht erfinden - daher RAG, Similarity Search)
   - Layer 2: Source Tracking (jede Aussage bekommt Quelle)
   - Layer 3: Confidence Scoring (0-100%)
   - Layer 4: Human-in-the-Loop Dashboard (Berater:in prüft ab)
   - Layer 5: Fallback-Logic (bei Unsicherheit: "Nicht verfügbar")

---

## Architektur & Tech Stack

### 100% Open Source

```
Frontend:
   - Vue.js 3 PWA (TypeScript)
   - Barrierefreie UI (WCAG 2.1 AA)
   - Service Worker + IndexedDB (Offline)
   - Whisper.js (10 Sprachen)

Backend:
   - FastAPI (Python)
   - LlamaIndex (RAG-Framework)
   - Hybrid Search: BGE-M3 (Vector) + BM25
   - Qwen 2.5 7B (Apache 2.0, lokal via ONNX)

Database:
   - Rechtsdaten: Scraper (BVerwG, VGH, VG)
   - Sessions: IndexedDB (Browser)
   - Skalierung: PostgreSQL (optional)

Deployment:
   - Docker Container
   - Railway.app / Render.com (kostenlos MVP)
   - Selbst-hostbar auf eigener Infrastruktur
```

---

## Projektentwicklung

### Abgeschlossene Konzeptphase 

- **Marktanalyse**: Law & Orga, Integreat-App, AsyLex evaluiert
  - **Lücke identifiziert**: Keine Legal-RAG mit Qualitätssicherung + Terminvorbereitung
  
- **Technische Evaluation**: 
  - 5 RAG-Frameworks getestet → LlamaIndex gewählt
  - 3 LLMs evaluiert → Qwen 2.5 optimal für Deutsch
  - 2 Vector DBs getestet → BGE-M3 implementiert
  
- **User Research**: 
  - RLC Berlin, Hamburg
  - Beratungsstellen Stuttgart + Tübingen
  - Bedarfsermittlung abgeschlossen
  
- **Prototyping**: 
  - Whisper.js Browser-Integration funktionsfähig
  - Proof-of-Concept erfolgreich

### MVP-Fokus: Verlängerung Aufenthaltserlaubnis

Der MVP konzentriert sich auf einen realen Use-Case:
- **Scenario**: Berater:in bereitet Geflüchtete auf Termin zur Aufenthaltserlaubnis-Verlängerung vor
- **Session Manager**: 7 strukturierte Phasen
- **Dokumenten-Checkliste**: 8 erforderliche Dokumente
- **Terminvorbereitung**: Was muss die Person wissen? Welche Unterlagen mitnehmen?
- **Sprachige Assistenz**: Audio-Input in 10 Sprachen

### Alleinstellungsmerkmal

**Erste Open-Source-Kombination aus:**
- Legal-RAG (spezialisiert auf Migrationsrecht)
- 5-Layer Quality Assurance (gegen Halluzinationen)
- Berater:innen-Dashboard (Human-in-the-Loop)
- Terminvorbereitung-Workflows
- Kostenlos + selbst-hostbar + vertrauenswürdig

**Im Unterschied zu:**
| Projekt | LegalAId | Unterschied |
|---------|----------|------------|
| Law & Orga | X | Keine KI, keine Terminvorbereitung, keine QS |
| Integreat | X | Keine juristische Tiefe, kein RAG, keine QS |
| Harvey AI | X | Kommerziell (500€+), nicht spezialisiert, proprietär |

---

## Zielgruppe und geplante Verbreitung

### Primär: Berater:innen von NGOs

- **Refugee Law Clinics** (35+ aktiv: Berlin, München, Frankfurt, Hamburg, etc.)
- **NGO-Beratungsstellen**: Pro Asyl, Flüchtlingsräte, Caritas-Migrationsberatung
- **Sozialverbände**: Diakonie, AWO

### Sekundär (Phase 2, ab Monat 5): Geflüchtete direkt

- PWA-Link von Berater:innen
- Self-Service Vorbereitung
- Mehrsprachige Oberfläche

### Verbreitungs-Netzwerk

- **Law & Orga Kooperation** (Netzwerk aus 35 RLCs)
- **#LeaveNoOneBehind Initiative** (NGO-Hosting + Verbreitung)
- **RLC Deutschland e.V.** Jahrestreffen (Mai 2026)
- **Beta-Partner**: RLC Netzwerke, hamburgasyl, Caritas + DRK Stuttgart
- **GitHub Community** + Discord Support

---

## Meilensteine (Teil 1 - 6 Monate Planung)

### Monat 1-2: Foundation
- GitHub Repo, CI/CD (GitHub Actions)
- Vue.js PWA Boilerplate (TypeScript)
- IndexedDB Schema für Sessions
- Rechtsdaten-Scraper (initial 500 BVerwG-Urteile)

### Monat 2-3: Core MVP (Use-Case: Verlängerung)
- Session Manager + State Machine (7 Phasen)
- Dokumenten-Checkliste (8 Dokumente)
- Terminvorbereitung-Workflow
- Whisper.js Integration (10 Sprachen)
- FastAPI Backend + LlamaIndex RAG

### Monat 3-4: Quality Assurance
- 5-Layer Quality System implementieren
- Confidence Scoring
- Reasoning Traces & Source Attribution
- Human-in-the-Loop Dashboard

### Monat 4-5: Polish
- UI/UX Refinement
- Performance Tuning
- Video-Tutorials (Deutsch + Englisch)
- Barrierefreiheits-Audit

### Monat 6: Beta + Launch
- 3 NGO Beta-Testung
- Public GitHub Release
- Dokumentation finalisieren
- Community-Setup (Discord, etc.)

---

## Teil 2 - 4 Monate Planung: Second Stage

### Ziel: Von Prototyp zu nachhaltigem Ökosystem

**Community-Aufbau & Support**
- Monatliche "Office Hours" für NGO-Support
- Discord mit Kanälen (User, Developer, Translator)
- Quarterly Meetups (hybrid) mit RLCs
- Onboarding-Dokumentation

**Intensive User Testing & UX**
- Feldtests mit 10 NGOs über 4 Monate
- A/B-Testing verschiedener Workflows
- Usability-Tests mit realen Geflüchteten
- Barrierefreiheits-Audit durch Expert:innen

**Nachhaltiges Finanzierungsmodell**
- Gründung gemeinnütziger Verein oder gUG
- Spendeninfrastruktur (Betterplace, OpenCollective)
- Anschlussförderungen (Mozilla, Mercator Stiftung)
- Hosting-Verhandlungen mit #LeaveNoOneBehind

**Technische Erweiterung**
- Zusätzliche Use-Cases (Familiennachzug, Erstantrag)
- Skalierung zu 72B Modell (optional)
- Multi-Tenancy für Shared-Hosting

**Erfolgsindikatoren:**
- 50+ aktive NGOs
- Selbsttragende Community
- 5+ externe Contributor:innen
- Nachhaltiges Finanzierungsmodell etabliert

---

## Lizenz & Open Source

- **Lizenz**: MIT (oder Apache 2.0 für Backend)
- **Repository**: https://github.com/open-legal-aid
- **Commitments**: 
  - Alle Komponenten Open Source
  - Kostenlos für NGOs
  - Selbst-hostbar
  - Keine proprietären Abhängigkeiten

---

## Weiterführende Ressourcen

- **Concept Document**: `/docs/ARCHITECTURE.md` (detaillierte Tech-Docs)
- **Development Guide**: `/docs/DEVELOPMENT.md`
- **Whisper POC Status**: `/docs/WHISPER.md` (aktueller Stand)
- **Deployment Guide**: `/docs/DEPLOYMENT.md`
- **Community**: Discord (Link folgt nach Launch)

---

## Kontakt & Support

- **Lead**: Dave Tjiok (tjiokdave@gmail.com)
- **GitHub**: https://github.com/open-legal-aid


---

**LegalAId – Open-Source Legal-RAG für barrierefreie Migrationsrechtsberatung**
