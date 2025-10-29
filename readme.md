# 🧠 AI Document Creation System

An intelligent platform for **AI-powered document generation** using templates, agents, and retrieval-based knowledge grounding.  
Designed to produce accurate, consistent, and customized documents such as reports, proposals, or contracts.

---

## 🚀 Overview

This project enables users to **create, manage, and generate documents** automatically using predefined templates and AI agents.  
The system integrates:
- Template-based text composition
- Contextual data retrieval (RAG)
- Multi-agent orchestration for writing, reviewing, and validating
- Feedback loops for continual improvement

---

## 🧱 System Architecture
```bash
User → Frontend → API Gateway / Orchestrator → AI Agent Layer →
├── Template Manager
├── Context Retriever (RAG)
├── Document Composer
└── Validation & QA Agent
↓
Storage: Templates, Documents, Vector DB, User Data
```
---

## ⚙️ Core Components

### 1. Template Manager
Handles template creation, storage, and parsing.

- Supports placeholders like `{{client_name}}`, `{{project_description}}`
- Enables version control and reusable formats

**Tech stack:**
- Frontend: React + TipTap + Yjs for rich text editing and real-time collaboration  
- Backend: FastAPI (async support, type safety, automatic docs)  
- Database: PostgreSQL  
- Cache: Redis (for response caching and session state)

---

### 2. AI Agent Layer
The intelligent core that drives document generation.

#### Agents (MVP: Start with 2, expand later):
- **Document Composer Agent** — Generates drafts from templates  
- **Validation Agent** — Checks logic, consistency, and grammar  
- *(Phase 2)* **Knowledge Agent (RAG)** — Retrieves relevant contextual info  
- *(Phase 3)* **Critique Agent** — Improves clarity, tone, and structure  

#### Tools:
- **LangGraph** for lightweight AI workflow orchestration  
- **Redis** for state management and caching  
- **Celery** or **BullMQ** for background job processing

**Performance Strategy:**
- **Streaming responses** — Show partial results as they generate
- **Parallel execution** — Run independent agents concurrently
- **Prompt caching** — Cache system prompts to reduce costs by 50-90%
- **Model selection** — Use GPT-4o for generation, GPT-4o-mini for validation

---

### 3. Context & Knowledge Layer (RAG)
Ensures factual accuracy and domain relevance.

- Stores background material, reference docs, brand guides, etc.
- Uses vector embeddings for semantic search
- Filters results based on metadata (e.g., type, category, date)

**Tech options:**
- Vector DB: **Qdrant** (fast, open-source) or **PostgreSQL + pgvector** (simpler stack)
- Embeddings: OpenAI text-embedding-3-small or Hugging Face  
- **Hybrid search** — Combine semantic + keyword search for better accuracy
- **Reranking** — Use Cohere Rerank API or local model to improve top results
- **Metadata filtering** — Filter by doc type/date before vector search

---

### 4. Document Generator
Merges the AI-generated content with structured templates.

**Libraries:**
- `python-docx` / `docxtpl` — for Word docs  
- `WeasyPrint` or `Typst` — for modern HTML→PDF conversion  
- `Jinja2` — for HTML or Markdown templates  

**Export formats:** PDF, DOCX, HTML, Markdown

Includes post-processing to ensure consistent formatting and styling.

---

### 5. Validation & Feedback Layer
Provides high accuracy and control over generated output.

#### Techniques:
- **Fact-checking:** Compare claims with retrieved context  
- **Consistency checks:** Detect section mismatches or conflicting statements  
- **Style & tone validation:** Ensure brand or professional consistency  

#### Tools:
- **Ragas** — Response evaluation metrics  
- **TruLens** — AI evaluation and feedback loops  
- **Guardrails.ai** — Schema validation and safety checks  

---

## 🧠 Advanced Techniques

| Technique | Description | Priority |
|------------|-------------|----------|
| **Streaming responses** | Show partial results as they generate | 🔴 MVP |
| **Prompt caching** | Cache system prompts to reduce costs by 50-90% | 🔴 MVP |
| **Structured prompting (JSON schema)** | Ensures predictable, parseable AI outputs | 🔴 MVP |
| **Background job processing** | Queue long-running tasks, don't block API | 🔴 MVP |
| **Response caching (Redis)** | Cache generated sections for similar requests | 🟡 Phase 1.5 |
| **RAG (Retrieval-Augmented Generation)** | Grounds content in real data | 🟡 Phase 2 |
| **Hybrid search + reranking** | Better retrieval accuracy | 🟡 Phase 2 |
| **Multi-agent orchestration** | Modular agent-based document creation | 🟢 Phase 3 |
| **Human-in-the-loop feedback** | Learn from user corrections | 🟢 Phase 3 |
| **Fine-tuning / LoRA adapters** | Tailor tone and accuracy for specific domains | ⚪ Phase 4 |
| **Tool use & APIs** | Agents can call external APIs (CRM, calendar, etc.) | ⚪ Phase 5 |
| **Semantic memory** | Maintain long-term personalization | ⚪ Phase 5 |

---

## 💻 Tech Stack (Optimized)

| Layer | Tools / Frameworks | Why |
|-------|--------------------|-----|
| **Frontend** | React + Tailwind + TipTap + Yjs + SWR | Modern editor with real-time collab + efficient caching |
| **Backend API** | **FastAPI** | Async support, type safety, auto docs |
| **AI Layer** | OpenAI GPT-4o / GPT-4o-mini or Anthropic Claude | Use 4o for generation, mini for validation (cost savings) |
| **Vector Database** | **Qdrant** or PostgreSQL + pgvector | Fast & open-source OR simpler single-DB stack |
| **Cache & Queue** | **Redis** + **Celery** | Response caching, session state, background jobs |
| **Workflow Orchestration** | **LangGraph** | Lightweight AI workflow management |
| **Storage** | PostgreSQL + S3 | Structured data + document storage |
| **Auth & User Management** | Supabase Auth | Complete auth solution with minimal setup |
| **LLM Observability** | **Langfuse** or **Helicone** | Monitor token usage, costs, latency |
| **Evaluation & Safety** | Guardrails / Ragas / TruLens | Response validation and quality metrics |

---

## 🧩 Example User Flow

1. **Choose or upload a template**  
   → e.g., “Marketing Proposal”  
2. **Enter context or structured data**  
   → e.g., Client name, campaign type, budget, goals  
3. **AI Agents Run**  
   → Compose → Retrieve context → Validate → Style-check  
4. **User Reviews & Edits**  
   → Interactive AI-assisted editor  
5. **System Learns**  
   → Incorporates feedback to improve tone or format

---

## 🧭 Development Roadmap

| Phase | Goal | Key Features |
|-------|------|-------------|
| **MVP** | Basic document creation with template merging | • Template CRUD<br>• Single LLM generation<br>• Streaming responses<br>• Prompt caching<br>• Background jobs |
| **Phase 1.5** | Performance & Cost Optimization | • Response caching (Redis)<br>• Token usage monitoring<br>• Export to PDF/DOCX/HTML |
| **Phase 2** | RAG-based context retrieval | • Vector DB integration<br>• Hybrid search + reranking<br>• Knowledge Agent<br>• Template marketplace |
| **Phase 3** | Multi-agent orchestration & validation | • Critique Agent<br>• Feedback loops<br>• Version control for documents<br>• Comments & approval workflows |
| **Phase 4** | Fine-tuning & personalization | • Domain-specific fine-tuning<br>• Style & tone customization<br>• Analytics dashboard |
| **Phase 5** | SaaS release | • Real-time collaboration<br>• Team workspaces<br>• API access<br>• Usage analytics |

---

## 🔮 Optional Cutting-Edge Features

- **Voice-based document creation** ("Create a proposal for Tesla in our usual tone")  
- **Real-time collaboration** with agent suggestions (via Yjs)  
- **AI Reviewer** for structure and clarity scoring  
- **Knowledge Graph integration** for structured factual grounding  
- **Multimodal generation** (text + visuals + charts)  
- **Incremental generation** — Generate by sections, not entire documents
- **Template versioning** — Track changes, compare versions, rollback
- **Approval workflows** — Route documents for review and sign-off

---

## 🧰 Example Tool Integrations

| Function | Tool | Notes |
|-----------|------|-------|
| Template rendering | Jinja2 / docxtpl | Dynamic placeholder replacement |
| RAG retrieval | LangChain + Qdrant | Hybrid search for better accuracy |
| Workflow orchestration | LangGraph | Lightweight for AI workflows |
| Background jobs | Celery + Redis | Async document generation |
| AI model integration | OpenAI / Anthropic | Prompt caching enabled |
| LLM monitoring | Langfuse / Helicone | Track costs, latency, quality |
| Evaluation | TruLens / Guardrails | Validate outputs, safety checks |

---

## 📚 Example Directory Structure
```bash
ai-doc-system/
├── frontend/
│   ├── src/
│   │   ├── components/
│   │   ├── pages/
│   │   ├── services/
│   │   └── hooks/
│   └── package.json
├── backend/
│   ├── app.py
│   ├── routes/
│   ├── agents/
│   │   ├── composer.py
│   │   ├── validator.py
│   │   └── orchestrator.py
│   ├── templates/
│   ├── services/
│   │   ├── llm_service.py
│   │   ├── rag_service.py
│   │   └── cache_service.py
│   ├── tasks/              # Celery tasks
│   │   └── generation.py
│   └── utils/
├── storage/
│   ├── documents/
│   ├── templates/
│   └── embeddings/
├── docker-compose.yml   # Redis, PostgreSQL, Qdrant
├── README.md
├── requirements.txt
└── .env.example

```
---

## 🚀 Performance Best Practices

### Cost Optimization
1. **Enable prompt caching** — OpenAI/Anthropic cache system prompts automatically
2. **Use model tiers strategically** — GPT-4o for generation, GPT-4o-mini for validation
3. **Cache similar requests** — Redis cache for frequently generated sections
4. **Batch processing** — Queue multiple documents for off-peak generation

### Speed Optimization
1. **Streaming** — Stream LLM responses to show partial results immediately
2. **Parallel execution** — Run independent agents concurrently
3. **Background jobs** — Use Celery for long-running document generation
4. **CDN for assets** — Serve static templates and documents from CDN

### Quality Optimization
1. **Hybrid search** — Combine semantic + keyword for better RAG results
2. **Reranking** — Improve retrieval precision with reranking models
3. **Monitoring** — Track generation quality with Langfuse/Helicone
4. **A/B testing** — Test different prompts and models

---

## 📦 Setup & Run (Example)

```bash
# Clone repository
git clone https://github.com/your-org/ai-doc-system.git
cd ai-doc-system

# Environment setup
cp .env.example .env
# Edit .env with your API keys (OpenAI, etc.)

# Start infrastructure (Redis, PostgreSQL, Qdrant)
docker-compose up -d

# Backend
cd backend
pip install -r requirements.txt

# Start Celery worker (background jobs)
celery -A tasks worker --loglevel=info &

# Start FastAPI server
uvicorn app:app --reload

# Frontend (new terminal)
cd ../frontend
npm install
npm run dev
