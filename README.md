# RAGnor
🧠 Ragnar — Agentic RAG System (LangChain + LangGraph + Ollama)
 
Ragnar is a production-grade Agentic Retrieval-Augmented Generation (RAG) system built entirely on the LangChain ecosystem with fully local inference using Ollama.
 
It combines:
 
- 🔍 Hybrid Retrieval (BM25 + Dense)
- 🧠 Agentic Reasoning (LangGraph)
- 🔁 Self-Correcting Loops (Grader + Critic)
- 🗄️ Memory (Short + Long Term)
- 🛡️ Guardrails (PII + Toxicity)
- 📊 Evaluation (LangSmith + RAGAS)
 
---
 
🚀 Features
 
🧠 Agentic RAG (Core Intelligence)
 
- Planner → Retriever → Grader → Generator → Critic loop
- Query rewriting & retry mechanism
- Self-reflection for answer quality
 
🔍 Hybrid Search
 
- BM25 (sparse retrieval)
- Dense vector search (Chroma + Ollama embeddings)
- EnsembleRetriever
- Local reranking (BGE Cross-Encoder)
 
🧠 Memory System
 
- Short-term: LangGraph "MemorySaver"
- Long-term: PostgreSQL ("PostgresSaver")
- Conversation-aware responses
 
🛡️ Guardrails
 
- PII detection & masking (email, phone)
- Toxicity filtering (local model)
- Input + output safety checks
 
🌐 API Layer
 
- FastAPI backend
- Streaming responses (SSE)
- Async-first architecture
 
📊 Evaluation & Observability
 
- LangSmith tracing (per node)
- RAGAS metrics:
  - Faithfulness
  - Answer Relevancy
  - Context Precision/Recall
 
🧠 Fine-Tuning Ready
 
- LoRA training pipeline (PEFT)
- Ollama-compatible model deployment
 
---
 
🏗️ Project Structure
 
ragnar/
├── ingestion/       # Document loading & chunking
├── retrieval/       # Hybrid search + reranker
├── agents/          # LangGraph agent loop
├── memory/          # Short & long-term memory
├── guardrails/      # Safety filters (PII + toxicity)
├── api/             # FastAPI backend
├── evaluation/      # LangSmith + RAGAS
├── finetune/        # LoRA training pipeline
├── config/          # Settings & logging
└── main.py
 
---
 
⚙️ Tech Stack
 
- LLM: Ollama (LLaMA3 / Mistral)
- Embeddings: Ollama ("nomic-embed-text")
- Framework: LangChain + LangGraph
- Vector DB: Chroma (dev) → Pinecone (prod)
- Memory DB: PostgreSQL
- API: FastAPI
- Evaluation: RAGAS + LangSmith
- Guardrails: Transformers (Toxic-BERT)
 
---
 
📦 Installation
 
1. Clone Repo
 
git clone https://github.com/yourusername/ragnar.git
cd ragnar
 
2. Create Environment
 
python -m venv venv
source venv/bin/activate  # Mac/Linux
venv\Scripts\activate     # Windows
 
3. Install Dependencies
 
pip install -r requirements.txt
 
---
 
🧠 Setup Ollama
 
Install Ollama:
 
👉 https://ollama.com
 
Pull required models:
 
ollama pull llama3
ollama pull nomic-embed-text
 
---
 
🔑 Environment Variables
 
Create ".env":
 
OLLAMA_BASE_URL=http://localhost:11434
OLLAMA_LLM_MODEL=llama3
OLLAMA_EMBED_MODEL=nomic-embed-text
 
CHROMA_PERSIST_DIR=./chroma_db
 
POSTGRES_URI=postgresql+psycopg://user:password@localhost:5432/ragnar
 
LANGCHAIN_TRACING_V2=true
LANGCHAIN_API_KEY=
LANGCHAIN_PROJECT=ragnar
 
---
 
📥 Ingest Documents
 
from ragnar.ingestion.pipeline import ingest_file
import asyncio
 
asyncio.run(ingest_file("data/sample.pdf"))
 
---
 
▶️ Run API
 
uvicorn ragnar.api.app:app --reload
 
---
 
🧪 Test Streaming
 
curl -N -X POST http://localhost:8000/chat/stream \
-H "Content-Type: application/json" \
-d '{"user_id":"test_user","query":"What is Ragnar?"}'
 
---
 
📊 Run Evaluation
 
python -m ragnar.evaluation.runner
 
---
 
🛡️ Guardrails
 
Ragnar automatically:
 
- Masks PII (emails, phone numbers)
- Blocks toxic inputs/outputs
 
---
 
🧠 Fine-Tuning (LoRA)
 
python ragnar/finetune/train_lora.py
python ragnar/finetune/merge.py
 
Then load into Ollama:
 
ollama create ragnar-model -f Modelfile
 
---
 
🧪 Example Flow
 
User Query
   ↓
Planner (rewrite)
   ↓
Hybrid Retrieval (BM25 + Dense)
   ↓
Grader (check relevance)
   ↓
Generator (LLM)
   ↓
Critic (self-evaluation)
   ↓
Final Answer
 
---
 
⚠️ Known Limitations
 
- BM25 currently loads all docs in memory (optimize later)
- No Redis caching (planned)
- Token-level streaming not yet enabled
 
---
 
🚀 Roadmap
 
- [ ] Token streaming (Ollama callbacks)
- [ ] Redis semantic caching
- [ ] Multi-agent orchestration
- [ ] Tool usage (SQL, APIs)
- [ ] Kubernetes deployment
- [ ] UI (React frontend)
 
---
 
🤝 Contributing
 
PRs are welcome! Please:
 
- Follow code structure
- Add docstrings
- Write modular code
 
---
 
📄 License
 
MIT License
 
---
 
⭐ Acknowledgements
 
Built using:
 
- LangChain
- LangGraph
- LangSmith
- Ollama
- RAGAS
 

