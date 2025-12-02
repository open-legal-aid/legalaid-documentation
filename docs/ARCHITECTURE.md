# LegalAId - Architecture & Technical Specification

## System Overview

```
┌─────────────────────────────────────────────────────────────────┐
│                     LegalAId System Architecture                │
└─────────────────────────────────────────────────────────────────┘

┌───────────────────────┐         ┌──────────────────────────────┐
│   End-User Layer      │         │   Berater:innen Layer        │
├───────────────────────┤         ├──────────────────────────────┤
│                       │         │                              │
│  Progressive Web      │◄───────►│  Human-in-the-Loop           │
│     App (PWA)         │         │     Dashboard                │
│                       │         │                              │
│  • Vue.js 3           │         │  • QA Verification           │
│  • IndexedDB Cache    │         │  • Source Attribution        │
│  • Service Worker     │         │  • Confidence Review         │
│  • Whisper.js Audio   │         │  • Workflow Management       │
│  • WCAG 2.1 AA        │         │                              │
└───────────────────────┘         └──────────────────────────────┘
         │                                    │
         │                                    │
         └────────────┬───────────────────────┘
                      │
         ┌────────────▼──────────────┐
         │  FastAPI Backend          │
         ├───────────────────────────┤
         │                           │
         │  • Session Management     │
         │  • State Machine (7 Phase)│
         │  • Workflow Orchestration │
         │  • API Endpoints          │
         │  • Auth & Logging         │
         │                           │
         └────────┬──────────┬───────┘
                  │          │
        ┌─────────▼┐    ┌───▼────────┐
        │   RAG    │    │  Document  │
        │ Engine   │    │  Checker   │
        ├──────────┤    ├────────────┤
        │          │    │            │
        │•LlamaIndex     │• Checklists│
        │•BGE-M3 Vector  │• Templates │
        │•BM25 Lexical   │• Validation│
        │•Qwen 2.5 7B    │            │
        │•ONNX Runtime   │            │
        │                │            │
        └────────┬───────┴────────────┘
                 │
        ┌────────▼──────────────┐
        │   Data Layer          │
        ├───────────────────────┤
        │                       │
        │ • BVerwG Urteile      │
        │ • Gesetze & GVO       │
        │ • Verwaltungsanweisung│
        │ • Checklisten         │
        │ • Case Templates      │
        │                       │
        └───────────────────────┘
```

---

## Frontend Architecture (Vue.js 3 PWA)

### Component Structure

```
frontend/
├── public/
│   └── poc/
│       └── whisper-poc.html          # Whisper PoC (aktuell)
│
├── src/
│   ├── components/
│   │   ├── SessionManager.vue        # Workflow-Management
│   │   ├── DocumentChecklist.vue     # Dokument-Prüfung
│   │   ├── TerminPrep.vue            # Terminvorbereitung
│   │   ├── AudioInput.vue            # Whisper.js Integration
│   │   └── QADashboard.vue           # Quality Assurance
│   │
│   ├── stores/                       # Pinia State Management
│   │   ├── sessionStore.ts           # Session State
│   │   ├── documentStore.ts          # Document State
│   │   └── uiStore.ts                # UI State
│   │
│   ├── services/
│   │   ├── api.ts                    # Backend API Client
│   │   ├── indexeddb.ts              # Local Cache
│   │   ├── whisper.ts                # Audio Processing
│   │   └── accessibility.ts          # A11y Utilities
│   │
│   ├── utils/
│   │   ├── formatters.ts             # Text/Date Formatting
│   │   ├── validators.ts             # Input Validation
│   │   └── i18n.ts                   # Internationalization
│   │
│   └── App.vue                       # Root Component
│
└── package.json
```

### Key Features

**Offline-First Approach:**
- Service Worker caches all assets
- IndexedDB stores sessions, checklists, documents
- Sync when online
- Progressive Enhancement

**Accessibility (WCAG 2.1 AA):**
- Semantic HTML
- ARIA labels & descriptions
- Keyboard navigation
- Color contrast 4.5:1 (normal text)
- Screen reader compatible
- Focus indicators

**Responsive Design:**
- Desktop (1920px+)
- Tablet (768px - 1919px)
- Mobile (< 768px)
- Touch-friendly buttons & inputs

---

## Backend Architecture (FastAPI)

### API Endpoints

```
POST   /api/v1/sessions               # Create session
GET    /api/v1/sessions/{id}          # Get session
PATCH  /api/v1/sessions/{id}          # Update session state
POST   /api/v1/sessions/{id}/query    # RAG Query

POST   /api/v1/documents/check        # Validate documents
GET    /api/v1/checklists/{usecase}   # Get checklist template
POST   /api/v1/checklists/{id}/verify # Verify against rules

POST   /api/v1/qa/review              # Human review
GET    /api/v1/qa/trace               # Get reasoning trace
POST   /api/v1/qa/feedback            # Store feedback

GET    /api/v1/health                 # System health
POST   /api/v1/logs                   # Logging endpoint
```

### Session State Machine (7 Phases)

```
Phase 1: INTAKE
├─ Persönliche Daten sammeln
├─ Sprache/Bedürfnisse abfragen
└─ Initial Assessment

Phase 2: DOCUMENT_CHECK
├─ Erforderliche Dokumente identifizieren
├─ Verfügbare Dokumente prüfen
└─ Lücken identifizieren

Phase 3: LEGAL_RESEARCH
├─ RAG-Abfrage (Rechtssicherheit prüfen)
├─ Relevante Urteile/Gesetze abrufen
└─ Berater:in reviewed Results

Phase 4: WORKFLOW_PREP
├─ Termin-Details sammeln
├─ Checklisten generieren
└─ Dokumente zusammenstellen

Phase 5: ADVISOR_REVIEW
├─ Berater:in verifiziert alles
├─ Ggfs. Korrektionen
└─ Sign-Off

Phase 6: CLIENT_COACHING
├─ Geflüchtete wird vorbereitet (optional)
├─ Audio/Video Coaching
└─ Fragen beantworten

Phase 7: TERMIN
├─ Session abschließen
├─ Feedback sammeln
└─ Archivierung
```

### FastAPI Components

```python
# auth.py - Session & Permission Management
- JWT-basierte Sessions
- Rate Limiting
- Audit Logging

# sessions.py - Session CRUD & State Management
- Session Creation/Update
- Phase Transitions
- Validation Rules

# rag_engine.py - Core RAG Logic
- Query Processing
- Vector Search (BGE-M3)
- BM25 Lexical Search
- Result Re-ranking
- Confidence Scoring

# quality_assurance.py - 5-Layer QA System
- Layer 1: Context Engineering
- Layer 2: Source Attribution
- Layer 3: Confidence Scoring
- Layer 4: Human Review Queue
- Layer 5: Fallback Logic

# document_validation.py - Document Checking
- Schema Validation
- Completeness Check
- Rule Engine

# models.py - Data Models
- Session (ORM)
- Document (ORM)
- QueryResult (Pydantic)
- Feedback (ORM)
```

---

## Quality Assurance: 5-Layer System

### Halluzination Prevention Architecture

```
┌─────────────────────────────────────────────────────────┐
│         User Query: "Welche Dokumente brauche ich?"     │
└────────────┬────────────────────────────────────────────┘
             │
             ▼
┌─────────────────────────────────────────────────────────┐
│ LAYER 1: Context Engineering (RAG)                      │
├─────────────────────────────────────────────────────────┤
│ ✓ Only retrieve from legal database                     │
│ ✓ System Prompt: "Nur aus Quellen antworten"            │
│ ✓ No generation beyond context                          │
│ → Result: Snippet from BVerwG ruling                    │
└────────────┬────────────────────────────────────────────┘
             │
             ▼
┌─────────────────────────────────────────────────────────┐
│ LAYER 2: Source Attribution (Tracking)                  │
├─────────────────────────────────────────────────────────┤
│ ✓ Tag: BVerwG 1 C 36.17 (Urteil vom 15.3.2018)         │
│ ✓ URL: www.bverwg.de/...                               │
│ ✓ Relevance Score: 0.92                                │
│ ✓ Text Extract: "[Zitat]"                              │
│ → Result: Fully attributed                              │
└────────────┬────────────────────────────────────────────┘
             │
             ▼
┌─────────────────────────────────────────────────────────┐
│ LAYER 3: Confidence Scoring (Uncertainty)               │
├─────────────────────────────────────────────────────────┤
│ ✓ Semantic Similarity: 0.85                             │
│ ✓ Source Credibility: 1.0 (Highest Court)              │
│ ✓ Temporal Relevance: 0.95 (Recent)                     │
│ ✓ Conflict Detection: 0 (No contradictions)             │
│ → Aggregate Score: 0.90 (90%)                           │
└────────────┬────────────────────────────────────────────┘
             │
             ▼
┌─────────────────────────────────────────────────────────┐
│ LAYER 4: Human-in-the-Loop (Review Queue)               │
├─────────────────────────────────────────────────────────┤
│ IF Confidence < 0.80:                                   │
│   → Flag for Berater:in review                          │
│   → Show confidence reason                              │
│   → Allow Override/Correction                           │
│ ELSE:                                                   │
│   → Show directly with confidence indicator             │
│                                                          │
│ Berater:in Actions:                                     │
│   • ✓ Approved                                          │
│   • ✓ Approved with Note                                │
│   • ✗ Rejected (reason)                                 │
│   • ⚠ Needs Verification                                │
└────────────┬────────────────────────────────────────────┘
             │
             ▼
┌─────────────────────────────────────────────────────────┐
│ LAYER 5: Fallback Logic (Graceful Degradation)          │
├─────────────────────────────────────────────────────────┤
│ IF all layers OK:                                       │
│   → Display: "Laut BVerwG 1 C 36.17 sind folgende       │
│             Dokumente erforderlich: [...]"              │
│                                                          │
│ ELSE IF confidence 0.60-0.80:                           │
│   → Display: "Wahrscheinlich erforderlich (90%         │
│             Sicherheit): [...]"                         │
│                                                          │
│ ELSE IF confidence < 0.60:                              │
│   → Display: ⚠️ "Nicht sicher. Bitte Berater:in fragen"│
│   → Fallback: Show default checklist                    │
│                                                          │
│ NEVER: Make up information                              │
└──────────────────────────────────────────────────────────┘
```

---

## RAG Engine: Technical Stack

### Vector Database & Search

```
Document Ingestion:
├─ BVerwG Urteile (500+ initial)
│  └─ PDFs → Text extraction → Chunking (512 tokens)
├─ Gesetze (AufenthV, AsylVfG)
│  └─ Strukturierte Daten → Chunking
└─ Verwaltungsanweisungen (AA-Leitfäden)
   └─ HTML → Clean text → Chunking

Vector Embedding (BGE-M3):
├─ Multi-lingual support (Arabisch, Türkisch, etc.)
├─ Dense vectors (768-dim)
├─ Semantic understanding
└─ Stored in Postgres vector extension (pgvector)

Hybrid Search Strategy:
├─ Query: "Welche Dokumente für Aufenthaltserlaubnis?"
├─ Vector Search: Find 10 most similar chunks
├─ BM25 Search: Find 10 most relevant (lexical)
├─ Re-ranking: Combine scores (0.7*Vector + 0.3*BM25)
└─ Return: Top 3 chunks with metadata

Qwen 2.5 7B LLM:
├─ Context: Top 3 chunks + System Prompt
├─ Generation: "Laut [Source]: Dokumente sind [...]"
├─ Output: Structured response with metadata
└─ ONNX Runtime: CPU inference (no GPU required)
```

### Data Models

```python
class Chunk(BaseModel):
    id: UUID
    source: str                  # "BVerwG_1_C_36.17"
    document_type: str           # "Urteil", "Gesetz", "AnwD"
    text: str                    # Raw text (512 tokens max)
    metadata: Dict              # {published: Date, court: str}
    vector: List[float]         # Embedding (768-dim)
    created_at: DateTime

class QueryResult(BaseModel):
    query: str
    results: List[Dict]         # [{chunk_id, source, score, text}]
    llm_response: str           # Generated answer
    confidence: float           # 0.0 - 1.0
    sources: List[str]          # Attribution list
    requires_review: bool       # if confidence < 0.80

class Session(BaseModel):
    id: UUID
    phase: Phase                # 1-7
    usecase: str                # "aufenthaltsverlaengerung"
    client_data: Dict           # Personal info
    documents: List[Document]   # Status of each doc
    qa_history: List[QAEntry]   # All questions & responses
    created_at: DateTime
    updated_at: DateTime
```

---

## Deployment Architecture

### Local Development

```bash
# Docker Compose for local dev
version: '3.8'
services:
  frontend:
    image: node:16
    ports: ["5173:5173"]
    volumes: ["./frontend:/app"]
    command: "npm run dev"

  backend:
    image: python:3.11
    ports: ["8000:8000"]
    volumes: ["./backend:/app"]
    environment:
      - QWEN_MODEL_PATH=/models/qwen-2.5-7b
    command: "uvicorn main:app --reload"

  postgres:
    image: postgres:15-pgvector
    ports: ["5432:5432"]
    volumes: ["pgdata:/var/lib/postgresql/data"]
    environment:
      - POSTGRES_DB=legalaId
      - POSTGRES_PASSWORD=dev_pw
```

### Production Deployment (Railway/Render)

```dockerfile
FROM python:3.11-slim as builder
WORKDIR /app
COPY requirements.txt .
RUN pip install --no-cache-dir -r requirements.txt

FROM node:16-alpine as frontend-build
WORKDIR /frontend
COPY frontend/ .
RUN npm install && npm run build

FROM python:3.11-slim
WORKDIR /app
COPY --from=builder /app .
COPY --from=frontend-build /frontend/dist ./static

EXPOSE 8000
CMD ["uvicorn", "main:app", "--host", "0.0.0.0"]
```

### Self-Hosting

```bash
# Docker Compose für Self-Hosting
docker-compose -f docker-compose.prod.yml up

# Nginx Reverse Proxy (SSL/TLS)
server {
    listen 443 ssl http2;
    server_name legalaId.example.com;
    
    ssl_certificate /etc/letsencrypt/live/...;
    ssl_certificate_key /etc/letsencrypt/live/...;
    
    location / {
        proxy_pass http://localhost:8000;
        proxy_set_header Host $host;
        proxy_set_header X-Real-IP $remote_addr;
    }
}
```

---

## Security & Data Protection

### Privacy by Design

```
 No Data Collection:
   - Sessions stored locally (IndexedDB)
   - No cloud upload
   - No third-party tracking
   - No Analytics

 Data Encryption:
   - TLS 1.3 for transport
   - Optional session encryption (AES-256)
   - Secure token storage

 Access Control:
   - JWT-based authentication
   - Role-based (Berater:in, Admin)
   - Session isolation
   - Audit logging

 Compliance:
   - DSGVO-compliant
   - No unnecessary data retention
   - User consent flows
   - Data export/deletion rights
```

---

## Performance Targets

| Metric | Target | Method |
|--------|--------|--------|
| Page Load | < 2s | Service Worker caching |
| RAG Query | < 3s | Vector search optimization |
| Audio Transcription | < 5s (10s audio) | Browser-native Whisper |
| Offline Functionality | 100% | Service Worker + IndexedDB |
| Mobile Performance | 80+ Lighthouse | Code splitting, lazy loading |

---

## Technology Decisions

| Component | Choice | Why |
|-----------|--------|-----|
| Frontend | Vue.js 3 | Smaller bundle, good DX, WCAG support |
| Backend | FastAPI | Type hints, speed, async support |
| LLM | Qwen 2.5 7B | German quality, Apache license, CPU inference |
| RAG | LlamaIndex | Modular, extensible, good documentation |
| Vector DB | Postgres pgvector | Self-hostable, no vendor lock-in |
| Audio | Whisper.js | Browser-native, no server required, 10 languages |
| Search | Hybrid (Vector+BM25) | Semantic + lexical best-of-both |

---

**Letzte Aktualisierung**: Dezember 2025
**Status**: MVP Phase - Concept Phase concluded
