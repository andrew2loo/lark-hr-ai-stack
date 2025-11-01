# Lark HR AI Stack

AI-powered Human Resource stack for Lark — resume ingestion, CPU-based embedding, semantic search with MongoDB 8 vector indexing, and seamless Lark bot integration.

---

## 🧩 Overview

**Lark HR AI Stack** enables HR teams to drastically reduce manual screening time by transforming candidate resumes into vector embeddings and performing semantic search directly within **Lark**.

The entire system runs efficiently on **CPU-only infrastructure**, making it cost-effective and deployable anywhere — no GPU dependency required.

---

## ⚙️ Key Features

- 📄 Resume Ingestion: Automatically extract and parse text from PDF/DOCX files uploaded in Lark.
- 🧠 CPU-Optimized Embeddings: Generate semantic vectors using compact sentence models (MiniLM, BGE, E5, etc.) with ONNX Runtime.
- 🔍 MongoDB 8 Vector Search: Store and search resume vectors using native `$vectorSearch` with cosine similarity.
- 🤖 Lark Bot Integration: Query, upload, and interact with candidates directly inside Lark via slash commands and interactive message cards.
- 🧱 Modular Monorepo Architecture: Ingestion, search, and integration services share a unified codebase for easy CI/CD.

---

## 🏗️ Architecture Overview

Lark HR AI Stack
│
├── apps/
│   ├── lark-bot/           # Handles slash commands, file uploads, interactive cards
│   ├── search-api/         # Exposes semantic search endpoint to Lark
│   ├── ingestion-worker/   # Parses resumes, chunks text, and embeds vectors (CPU-only)
│   └── miniapp/            # (optional) Lark side panel or web dashboard
│
├── packages/
│   ├── shared-lib/         # Common logic (schemas, card builders, logging)
│   └── data-contracts/     # JSON Schemas, Mongo models, OpenAPI definitions
│
├── infra/
│   ├── docker/             # Dockerfiles and docker-compose setup
│   ├── k8s/                # Kubernetes manifests or Helm charts
│   └── terraform/          # MongoDB Atlas / VPC / Secrets / Cloud infra
│
└── .github/workflows/      # CI/CD pipelines

---

## 🧠 Technology Stack

| Layer | Technology | Notes |
|-------|-------------|-------|
| Messaging / UI | Lark Open Platform | Bot, Slash Commands, Interactive Cards |
| API Framework | FastAPI or Express.js | Choose Python or NodeJS backend |
| Embedding Models | SentenceTransformers / ONNX Runtime | CPU-only inference |
| Database | MongoDB 8.0+ | Native vector index + metadata filters |
| Containerization | Docker / Compose / K8s | Local and cloud deployments |
| CI/CD | GitHub Actions | Build → Test → Deploy |

---

## 🚀 Getting Started

### 1️⃣ Prerequisites
- Python 3.10+ or Node.js 18+
- Docker & Docker Compose
- MongoDB 8.0+ (Atlas or self-hosted)
- Lark Developer account and App credentials

### 2️⃣ Clone the repository
```
git clone https://github.com/<your-org>/lark-hr-ai-stack.git
cd lark-hr-ai-stack
```

### 3️⃣ Set up environment variables
Create a `.env` file in the root:
```
LARK_APP_ID=<your-app-id>
LARK_APP_SECRET=<your-app-secret>
MONGO_URI=mongodb+srv://user:pass@cluster/db
EMBED_MODEL=sentence-transformers/all-MiniLM-L6-v2
```

### 4️⃣ Run with Docker Compose
```
docker-compose up --build
```

The system will:
- Start the Lark Bot service
- Start the Search API
- Start the Ingestion Worker
- Connect automatically to MongoDB

---

## 🔍 Example Workflow

1. HR uploads a resume PDF to a Lark chat with the bot.  
2. Bot receives the event, extracts text, and queues it to Ingestion Worker.  
3. Worker embeds the text using ONNX Runtime → stores vectors in MongoDB.  
4. HR types `/search "senior java singapore >5y"` in Lark.  
5. Search API embeds the query → `$vectorSearch` in MongoDB → returns top candidates.  
6. Bot sends an interactive card with ranked candidates and filters.

---

## 🧪 Development Workflow

| Command | Description |
|----------|--------------|
| make dev | Start local dev environment (Compose + hot reload) |
| make lint | Lint and format all apps |
| make test | Run unit tests |
| make build | Build Docker images for all services |

(You can later replace `make` with npm or Poetry scripts.)

---

## 🧰 Folder Conventions

| Folder | Purpose |
|---------|----------|
| apps/ | Executable services (bot, api, worker, etc.) |
| packages/ | Shared libraries and data contracts |
| infra/ | Infrastructure-as-code, deployment manifests |
| .github/workflows/ | CI/CD pipelines |

---

## 🔒 Security and Privacy

- Candidate data is stored only within authorized databases.  
- All secrets (Lark tokens, Mongo credentials) are managed via GitHub Secrets or encrypted `.env` files.  
- Personal Identifiable Information (PII) redacted where possible before embedding.  

---

## 🧭 Roadmap

- [ ] Resume skill tagging and entity extraction  
- [ ] Hybrid (vector + keyword) search  
- [ ] Recruiter-side scoring dashboard  
- [ ] Lark Base integration for shortlisting  
- [ ] ONNX int8 quantization for faster embedding  

---

## 🧑‍💻 Contributing

Pull requests are welcome!  
Please open an issue first to discuss major changes.

---

## 🪪 License

MIT License © 2025 — Maintained by [Your Name or Organization]

---

"Automate the hiring pipeline. Let Lark talk to your candidates — and your data."
