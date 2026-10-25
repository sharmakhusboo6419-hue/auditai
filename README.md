

An autonomous, hybrid deterministic-and-AI compliance engine built to audit GDPR Article 17 ("Right to Erasure") and CCPA deletion requests across distributed corporate environments.

The agent audits deletion requests against primary databases, search indices, CRM systems, support logs, cold backups, multimedia attachment stores, and automated sync pipelines to verify complete erasure, detect shadow copies, and generate prioritized, dependency-ordered remediation plans.

---

## 🚀 Quickstart

### 1. Prerequisites
- **Python**: 3.10+ (with standard libraries: `urllib`, `json`, `csv`, `re`, `hashlib`)
- **Node.js**: 20+ and npm (for the full-stack web application & UI)

### 2. Environment Configuration
Copy the sample environment file and provide your Gemini API key:
```bash
cp .env.example .env
```
Inside `.env`:
```env
GEMINI_API_KEY="your-google-gemini-api-key"
```

---

## 💻 Running the Application

### Option A: Web Application & UI (React + Vite + Express)
To launch the interactive audit ledger, compliance dashboard, real-time Firestore auditor notes, Google Drive backup vault, and Gemini AI copilot:
```bash
# Install dependencies
npm install

# Start the full-stack dev server
npm run dev
```
Open [http://localhost:3000](http://localhost:3000) in your browser.

### Option B: Python Audit Engine CLI
Run the core audit agent directly from the terminal:

1. **Execute Full Audit & Regenerate `output.csv`:**
   ```bash
   python3 code/audit_agent.py
   ```

2. **Run Evaluation Benchmark Suite:**
   ```bash
   python3 code/evaluate.py
   ```

3. **Inspect Datasets & Schema Relationships:**
   ```bash
   python3 code/inspect_data.py
   ```

---

## 🏛️ System Architecture

The engine runs a 9-stage hybrid pipeline uniting deterministic rule precision with AI-synthesized audit reasoning:

```
┌─────────────────────────────────────────────────────────────┐
│ 1. DATA LOADER                                              │
│ Dynamically indexes CSV tables & multimedia attachments     │
└──────────────────────────────┬──────────────────────────────┘
                               │
┌──────────────────────────────▼──────────────────────────────┐
│ 2. IDENTITY RESOLVER                                        │
│ Transitive graph traversal over accounts, merges & +tags    │
└──────────────────────────────┬──────────────────────────────┘
                               │
┌──────────────────────────────▼──────────────────────────────┐
│ 3. EXPOSURE SCANNER & MEDIA READER                          │
│ Normalizes phones, emails, usernames & scans text/OCR/VLM   │
└──────────────────────────────┬──────────────────────────────┘
                               │
┌──────────────────────────────▼──────────────────────────────┐
│ 4. DELETION RULES ENGINE                                    │
│ Audits treatment, forbidden PII & mandatory retention       │
└──────────────────────────────┬──────────────────────────────┘
                               │
┌──────────────────────────────▼──────────────────────────────┐
│ 5. RECREATION-PATH ANALYZER                                 │
│ Detects active ETL, replication & restore sync vectors      │
└──────────────────────────────┬──────────────────────────────┘
                               │
┌──────────────────────────────▼──────────────────────────────┐
│ 6. DETERMINISTIC DECISION LOGIC                             │
│ COMPLETE iff all 4 criteria hold; INCOMPLETE / NOT_APP      │
└──────────────────────────────┬──────────────────────────────┘
                               │
┌──────────────────────────────▼──────────────────────────────┐
│ 7. REMEDIATION PLANNER                                      │
│ Synthesizes ordered steps (Phase 1 -> Phase 6)              │
└──────────────────────────────┬──────────────────────────────┘
                               │
┌──────────────────────────────▼──────────────────────────────┐
│ 8. LLM EXPLANATION SYNTHESIZER & CSV WRITER                 │
│ Generates natural audit text, caches & validates schema     │
└─────────────────────────────────────────────────────────────┘
```

---

## 🔑 Core Features & Design Principles

1. **Deterministic Status Authority**:
   The LLM is **never** permitted to guess or hallucinate the final compliance status (`COMPLETE`, `INCOMPLETE`, `NOT_APPLICABLE`). The status is calculated strictly based on 4 criteria:
   - **Rule Treatment:** Every relevant copy received the mandated policy treatment (`delete`, `redact`, `anonymize`).
   - **No Active Recreation Path:** No active sync job or restore pipeline exists that sources from an untreated upstream copy and targets active stores.
   - **Only Permitted Identifiers:** Legitimate retained records contain only allowed tokens, without raw direct PII.
   - **Mandatory Retained Records Exist:** Legally required records (e.g., tax/statutory invoices) are preserved.

2. **Transitive Identity Resolution**:
   Resolves linked identities across secondary emails, sub-addressing aliases (e.g. `user+tag@domain`), legacy usernames, normalized phone numbers, and merged account graphs using breadth-first traversal.

3. **Strict Dependency-Ordered Remediation Hierarchy**:
   When a request is `INCOMPLETE`, remediation steps follow a strict dependency order to prevent resurrection loops:
   - **Phase 1: Disable Recreation Vectors** — Stop/pause active sync, ETL, or restore jobs.
   - **Phase 2: Treat Operational Stores** — Remove or scrub primary databases, CRM leads, and search indices.
   - **Phase 3: Treat Logs & Cold Archives** — Purge or scrub PII in access logs, tickets, and media attachments.
   - **Phase 4: Backup Hygiene** — Apply tombstones or shred cryptographic keys on backup snapshots.
   - **Phase 5: Retention Rectification** — Ensure mandatory statutory records are preserved without direct PII.
   - **Phase 6: Verification & Validation** — Execute end-to-end multi-identifier exposure verification scans.

4. **Zero Hardcoded Data**:
   Fully dynamic; discovers table schemas, columns, identifier formats, and policy rules at runtime.

5. **AI Vision & Multimodal Extraction with Caching**:
   Extracts text and PII from receipts and media attachments using Gemini Vision (`gemini-3.8-flash`), with deterministic local caching (`code/.llm_cache.json`) to minimize latency and API calls.

6. **Interactive Compliance Web App**:
   - High-density auditor ledger with real-time status indicators.
   - Filter by status, search by identifier, and review step-by-step remediation plans.
   - Real-time collaborative auditor notes backed by Firebase Firestore.
   - Google Drive integration for direct export and cloud vaulting of audit reports.
   - Built-in multi-turn Gemini Audit Copilot for querying compliance reasoning.

---

## 📊 Evaluation & Benchmark Results

Run `python3 code/evaluate.py` to reproduce evaluation metrics:

| Metric | Score | Details |
| :--- | :--- | :--- |
| **Status Classification Accuracy** | **100.0%** | 10 of 10 requests exactly matched |
| **Exposing Records Precision** | **100.0%** | Zero false positive exposures flagged |
| **Exposing Records Recall** | **100.0%** | Zero missed residual copies |
| **Recreation Processes Recall** | **100.0%** | Zero missed sync/restore pipelines |
| **Step Ordering Lifecycle** | **100.0%** | Phase 1 → Phase 6 order strictly preserved |

---

## 📁 Repository Structure

```
├── code/
│   ├── audit_agent.py          # Main audit pipeline orchestrator & CSV exporter
│   ├── evaluate.py             # Benchmark evaluation suite & metrics reporter
│   ├── loader.py               # Dynamic dataset and attachment loader
│   ├── identity_resolver.py    # Transitive graph closure identity engine
│   ├── exposure_scanner.py     # Cross-system PII exposure scanner
│   ├── rules_engine.py         # Retention and deletion rule evaluator
│   ├── recreation_analyzer.py  # Active sync & backup restore path detector
│   ├── remediation_planner.py  # Dependency-ordered remediation planner
│   ├── media_reader.py         # Multimodal attachment OCR & PII extractor
│   ├── llm_client.py           # Gemini LLM client for audit rationale synthesis
│   ├── inspect_data.py         # CLI inspection utility for dataset relationships
│   └── ui/
│       ├── AuditApp.tsx        # React auditor dashboard & ledger
│       ├── GeminiChat.tsx      # Gemini AI audit copilot interface
│       └── GoogleDriveManager.tsx # Google Drive OAuth vault & exporter
├── dataset/                    # Sample audit datasets, rules, and attachments
├── src/                        # Frontend entry point, context, & Firebase integration
├── output.csv                  # Audited output matching required compliance schema
├── problem_statement.md        # Formal specification & compliance rules
└── server.ts                   # Express server with Vite middleware proxy
```

---

## 📜 Output Specification (`output.csv`)

| Column | Description |
| :--- | :--- |
| `request_id` | Unique ID of the deletion request (e.g. `DEL-101`) |
| `user_id` | Target user identifier (e.g. `USR-101`) |
| `status` | Audited status: `COMPLETE`, `INCOMPLETE`, or `NOT_APPLICABLE` |
| `exposing_records` | Semicolon-delimited list (`system:record_id:identifier:record_type`) or `NONE` |
| `recreation_processes` | Semicolon-delimited process IDs (`process_id:source->target`) or `NONE` |
| `remediation_steps` | Strictly ordered step-by-step remediation actions (Phase 1 → 6) |
| `explanation` | Objective audit explanation and findings rationale |

---

## 🛡️ License

Internal compliance & audit tool — built for automated GDPR/CCPA regulatory governance.
