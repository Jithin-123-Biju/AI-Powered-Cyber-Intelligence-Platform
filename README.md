OPCODE IMPACT 2026 Hackthon


Team ID: OPC022

 1. Problem Statement:

Security analysts face severe alert fatigue and prolonged Time-to-Detect (TTD) when dealing with massive volumes of raw endpoint logs and network telemetry. Traditional manual forensic investigations are too slow, allowing attackers to move laterally and exfiltrate data, while evasive zero-day threats frequently bypass signature-based detection systems. Furthermore, siloed threat data prevents real-time correlation of local anomalies with global cyber threat intelligence, delaying critical incident response.

 2. Solution Title
AI-Powered Cyber Intelligence Platform.

 3. Solution Description:

Our platform is a centralized cybersecurity architecture that automates Incident Response (IR) and Digital Forensics (DFIR) by rapidly ingesting and parsing raw digital evidence (syslogs, web logs, auth logs). It leverages unsupervised machine learning (Isolation Forests) for signatureless anomaly detection to catch zero-day threats and abnormal payload structures. Finally, it cross-references extracted Indicators of Compromise (IOCs) with global Threat Intelligence (STIX/MISP) to automatically generate human-readable forensic timelines and incident narratives.

 4. Architecture Diagram
Workflow:

1. Ingestion & Parsing: The FastAPI backend receives log files via a REST API. A custom Regex Extractor parses out critical IOCs (IPs, Domains, MD5/SHA256 hashes, timestamps).
2. Asynchronous Processing: Celery and a Redis message broker handle heavy AI and CTI tasks in the background so the API remains responsive.
3. AI Anomaly Scoring: Scikit-Learn's Isolation Forest models evaluate the parsed payloads to assign anomaly risk scores based on structural irregularities and payload metrics.
4. CTI Correlation: Extracted indicators are cross-referenced with MISP/STIX 2.1 threat feeds to identify known threat actor campaigns.
5. Storage & Search: Results are stored in PostgreSQL for relational integrity (cases, artifacts) and Elasticsearch for rapid forensic querying.

 5. Technology Stack:

Frontend: React.js / Next.js with Tailwind CSS
Backend: FastAPI (Python 3.10), Celery (Task Queue), Pydantic (Data validation)
Database: PostgreSQL (via `asyncpg` and SQLAlchemy), Elasticsearch (for rapid log search), Redis (for Celery brokering)
Other Technologies:  Scikit-Learn (Isolation Forest ML), MISP / STIX 2.1 API (Threat Intelligence), Docker & Docker Compose (Containerization)

6. Quick Start Guide

Prerequisites:

Docker and Docker Compose installed on your system.
 Port availability for `8000` (API), `5432` (Postgres), `6379` (Redis), and `9200` (Elasticsearch).

Installation & Execution:

  bash
1. Clone the repository
git clone https://github.com/jithin-123-biju/ai-cyber-threat-platform.git
cd ai-cyber-threat-platform/Backend

2. Set up environment variables
3.cp .env.example .env 
4.Build and start all services using Docker Composedocker-compose up --build -d

 4. Access the API documentation
Open your browser and navigate to: http://localhost:8000/docs


 7. Output Screenshots

 The dashboard displays an active forensic investigation case, visualizing the chronological timeline of the cyberattack based on parsed timestamps. It highlights high-severity log anomalies flagged by the machine learning model alongside their corresponding Threat Actor CTI matches from MISP.

 8. Future Scope

Agentic AI Responders (SOAR): Implementing autonomous AI agents capable of actively isolating compromised endpoints and updating firewall blocklists in real-time based on high-severity triage alerts.
     Cross-Cloud Ephemeral Forensics: Expanding the ingestion engine to capture volatile memory dumps and API logs from ephemeral cloud containers (Kubernetes, AWS EKS) before they spin down.
    LLM-Driven Report Generation: Integrating Large Language Models directly into the pipeline to read the triaged JSON data and auto-draft executive summaries for incident responders.

9. Team Contributions

 Member Name | Contribution

Jithin C Biju: Developed the FastAPI backend architecture, Docker containerization, and PostgreSQL database schemas and built the frontend dashboard.
Aswin A: Implemented the ML Anomaly Detection engine (Isolation Forest) and the regex log parsing system.
|Sanjay VR:Integrated MISP/STIX CTI feeds, configured the Celery/Redis async workersand.

 10. Tools Used

Tool / Platform | Purpose / Why Used 

FastAPI & PostgreSQL: Provides a highly performant, asynchronous API framework and robust relational data storage necessary for enterprise security tools.
Scikit-Learn (ML): Used the Isolation Forest algorithm for unsupervised machine learning to detect zero-day malware and behavioral anomalies without relying on known signatures.
Docker & Celery: Docker ensures a unified deployment environment across all services, while Celery prevents machine learning tasks from blocking real-time API responses.
