# AI-Powered-Cyber-Intelligence-Platform

> Production-Grade Conversational AI for Digital Forensics and Cyber Threat Intelligence

**AI-Powered-Cyber-Intelligence-Platform** is an intelligent, ChatGPT-inspired investigation workspace built for cybersecurity incident responders, digital forensics analysts, and SOC teams. It eliminates conventional dashboard clutter (tables, oversized cards, and redundant graphs on homepages) in favor of a focused, conversational workflow where analysts upload evidence, interrogate suspicious activity, correlate threat intelligence, and generate formal forensic reports in one unified stream.

---

## ⚡ Core Experience & Design Architecture

### 1. Minimalist ChatGPT-Inspired Homepage
- **Deep Slate Architecture**: Dark, utility-first visual design using Tailwind CSS scales (`bg-slate-950`, `border-white/10`).
- **Centered Hero**: Distinctive branding (*AI-Powered-Cyber-Intelligence-Platform*), concise value proposition, and an uncrowded interface.
- **Large Floating Message Composer**: Multi-line auto-expanding input with file attachment controls, drag-and-drop evidence ingestion, and intuitive keyboard interactions (Enter to send, Shift + Enter for new lines).
- **Curated Starter Suggestions**: Clean prompt suggestions beneath the composer to immediately initiate log triage, C2 URL assessment, script deobfuscation, or report generation.

### 2. Streamlined Conversational Investigation Stream
- **Collapsible Sidebar**: New Chat ("New Investigation"), searchable conversation history grouped by date (Today, Yesterday, Previous 7 Days), and settings.
- **Natural Multi-Turn Context**: Preserves previous findings and uploaded artifacts across follow-up queries.
- **In-Message Evidence Details**: Ingested files are displayed cleanly with verified cryptographic SHA-256 hashes.
- **Explainable Threat Findings**: Markdown explanations, inline MITRE ATT&CK® TTP alignments, and preliminary risk matrices displayed naturally within AI responses.
- **Fixed Bottom Composer**: Anchored cleanly at the base of the active conversation for seamless interaction.
- **Slide-Over Evidence Inspector**: Optional slide-over drawer summarizing ingested files, hashes, and extracted IOCs for quick copying to firewall rules without obstructing the conversation.

### 3. Safe, Non-Destructive Evidence Processing
- Supports `.log`, `.txt`, `.csv`, `.json`, `.xml`, `.pcap`, `.pcapng`, and `.evtx`.
- **In-Memory SHA-256 Digest**: Computes a cryptographic SHA-256 hash on upload using Node.js `crypto` before extracting readable ASCII text.
- **Zero-Execution Sandbox**: Artifacts are triaged purely in memory. No scripts, macros, or binary executables are run.

### 4. PostgreSQL Forensic Storage Integration
- **Relational Schema**: Backend SQLAlchemy models and API endpoints structured specifically for PostgreSQL storage and retrieval:
  - `forensic_cases`: Case metadata, triage status, and risk classifications.
  - `chat_messages`: Full multi-turn conversation history and forensic findings.
  - `forensic_artifacts`: File hashes (SHA-256), MIME types, byte sizes, and parsed summaries.
  - `threat_indicators`: Extracted IPs, domains, hashes, and MITRE ATT&CK TTP links.
- **Synchronized Data Access**: Real-time storage interface (`/api/postgres-sync`) supporting custom database connection strings configured via the Settings modal.

### 5. Multi-Format Report Export
- Compiles official forensic triage briefs downloadable as:
  - **Markdown (`.md`)**
  - **Structured JSON (`.json`)**
  - **Print / PDF** (with print-optimized stylesheets)

---

## 🚀 Quick Start Guide

### Running the Full-Stack Conversational App

1. Navigate to the `Frontend` directory:
   ```powershell
   cd "c:\Users\jithi\OneDrive\Documents\AI Cyber Threat Intelligence Platform\Frontend"
   ```

2. Install dependencies (if not already installed):
   ```powershell
   npm install
   ```

3. Start the Next.js development server:
   ```powershell
   npm run dev
   ```

4. Open your browser and navigate to:
   ```
   http://localhost:3000
   ```
   *(If port 3000 is occupied, Next.js will automatically run on `http://localhost:3001`).*

---

## ⚙️ Optional Backend & Provider Configuration

AI-Powered-Cyber-Intelligence-Platform functions out of the box in **100% verified offline deterministic mode** with zero external API keys required. All forensic heuristics, SHA-256 calculations, and MITRE ATT&CK mappings run locally.

To connect external providers, use the UI **Settings modal** (gear icon in sidebar) or set environment variables in `Frontend/.env.local`:
- `GROQ_API_KEY`: Enables real-time Llama-3.3-70B model narrative generation.
- `VIRUSTOTAL_API_KEY`: Enables live VirusTotal v3 IP/domain reputation queries.
- `DATABASE_URL`: PostgreSQL connection string (defaults to `postgresql://forensic_user:forensic_password@localhost:5432/forensic_db`).

---

## 🛡️ Forensic Chain of Custody & Security Guarantees
- **Non-Destructive Parsing:** Evidence files are strictly read as read-only byte buffers. No scripts or binaries are executed.
- **Truthful Telemetry:** If an external feed (VirusTotal) or model (Groq) is not configured, the platform transparently labels the status as "Not configured — local heuristics used" rather than fabricating artificial scores.
- **Data Privacy:** Sensitive logs persist in local browser storage (`localStorage`) or your private PostgreSQL database, never sent to third-party endpoints without authorization.
