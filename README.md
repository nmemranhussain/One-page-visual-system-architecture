# System Architecture Portfolio: Multi-Agent AI Applications
### N M Emran Hussain | AI & Machine Learning Engineer

## 1. Cardiovascular Risk Assessment & Triage Assistant

**Architecture Overview:** A serverless, 4-agent clinical pipeline deployed on Google Cloud Platform, designed to parse unstructured vitals, predict mortality risk, and retrieve relevant medical guidelines using advanced RAG capabilities.

**Core Stack:** Vertex AI Gemini, BigQuery ML, Vertex AI Vector Search, Cloud Run, Docker, Streamlit.

**System Data Flow:**

**User Interface:** Serverless Streamlit dashboard hosted on Cloud Run receives unstructured patient vitals.

**Agent 1 (Parser):** Vertex AI Gemini processes and structures the raw text inputs.

**Agent 2 (Predictor):** BigQuery ML Boosted Tree ingests structured data to predict heart failure mortality, utilizing SHAP for feature explainability.

**Agent 3 (Retriever):** Vertex AI Vector Search executes a RAG workflow to retrieve contextually relevant medical guidelines.

**Agent 4 (Synthesizer):** Combines the SHAP explainability and retrieved guidelines into a final triage recommendation.

**Monitoring:** Active MLOps drift monitoring tracks model performance continuously.
```mermaid
graph TD
    A[Streamlit Dashboard / Cloud Run] -->|Unstructured Vitals| B(Vertex AI: Orchestrator)
    B -->|Text Parsing| C[Agent 1: Gemini Parser]
    C -->|Structured Data| D[Agent 2: BigQuery ML Boosted Tree]
    D -->|Mortality Risk + SHAP| F[Agent 4: Triage Synthesizer]
    B -->|Query| E[Agent 3: Vertex AI Vector Search / RAG]
    E -->|Medical Guidelines| F
    F -->|Final Triage Output| A
    D -.->|Drift Monitoring| G[(MLOps Monitoring)]
```
