# 🪨 Rocky — Geology AI Agent

> An intelligent conversational agent specialized in Earth Sciences, built with FastAPI, LangGraph, and RAG — designed as a full-stack AI portfolio project.

<div align="center">

![Rocky Banner](https://img.shields.io/badge/Rocky-Geology%20AI%20Agent-C97A3A?style=for-the-badge&logo=data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHZpZXdCb3g9IjAgMCAyNCAyNCI+PHBhdGggZmlsbD0id2hpdGUiIGQ9Ik0xMiAyQzYuNDggMiAyIDYuNDggMiAxMnM0LjQ4IDEwIDEwIDEwIDEwLTQuNDggMTAtMTBTMTcuNTIgMiAxMiAyeiIvPjwvc3ZnPg==)
![Python](https://img.shields.io/badge/Python-3.11+-3776AB?style=for-the-badge&logo=python&logoColor=white)
![FastAPI](https://img.shields.io/badge/FastAPI-0.110+-009688?style=for-the-badge&logo=fastapi&logoColor=white)
![LangGraph](https://img.shields.io/badge/LangGraph-Agent-FF6B35?style=for-the-badge)
![Frontend](https://img.shields.io/badge/Frontend-Vercel-000000?style=for-the-badge&logo=vercel&logoColor=white)
![Backend](https://img.shields.io/badge/Backend-Render-46E3B7?style=for-the-badge&logo=render&logoColor=white)

**[Live Demo](https://geology-agent-frontend-e8ecp9ji0-piriscs-projects.vercel.app)** · **[API Docs](https://geology-agent.onrender.com/docs)** · **[Report Bug](https://github.com/pirisc/geology_agent_frontend/issues)**

</div>

---

## 📖 Overview

Rocky is a domain-specific AI agent that answers questions about geology, mineralogy, paleontology, and Earth sciences. It combines a **Retrieval-Augmented Generation (RAG)** pipeline with a **LangGraph-powered agent** to deliver accurate, context-aware responses — complete with a polished, production-grade chat interface.

This project was built as part of an AI Engineering bootcamp, serving as a capstone that integrates prompt engineering, agent design, RAG systems, and full-stack deployment.

---

## ✨ Features

- 🤖 **LangGraph Agent** — Multi-step reasoning with tool use and memory via conversation threads
- 📚 **RAG Pipeline** — Retrieves relevant geological knowledge before generating responses
- ⚡ **Streaming Responses** — Real-time token streaming via Server-Sent Events (SSE)
- 🌐 **Bilingual Support** — Full English and Spanish language support
- 🎨 **Polished UI** — Dark/light mode, Rocky mascot, copy buttons, timestamps, inline image rendering
- 🛑 **Stop Generation** — Abort streaming mid-response
- 🖼️ **Inline Images** — Geological illustrations rendered directly in chat
- 📱 **Responsive Design** — Works across desktop and mobile

---

## 🏗️ Architecture

```
┌─────────────────────────────────────────────────────────┐
│                     Rocky Frontend                       │
│              (Vanilla HTML / CSS / JS)                   │
│         Streaming SSE  ·  Dark/Light Mode                │
└─────────────────────┬───────────────────────────────────┘
                      │  HTTP POST /chat (SSE stream)
┌─────────────────────▼───────────────────────────────────┐
│                   FastAPI Backend                        │
│                                                          │
│  ┌─────────────────────────────────────────────────┐    │
│  │              LangGraph Agent                     │    │
│  │                                                  │    │
│  │   User Input → [Retriever Tool] → LLM → Output  │    │
│  │                     ↕                            │    │
│  │              [Other Tools...]                    │    │
│  └──────────────────┬──────────────────────────────┘    │
│                     │                                    │
│  ┌──────────────────▼──────────────────────────────┐    │
│  │              RAG Pipeline                        │    │
│  │                                                  │    │
│  │   Vector Store → Semantic Search → Context       │    │
│  │   (Geology knowledge base)                       │    │
│  └─────────────────────────────────────────────────┘    │
└─────────────────────────────────────────────────────────┘
```

---

## 🛠️ Tech Stack

| Layer | Technology |
|-------|-----------|
| **Frontend** | HTML5, CSS3, Vanilla JS |
| **Backend** | Python, FastAPI |
| **Agent Framework** | LangGraph |
| **LLM** | OpenAI GPT |
| **RAG / Embeddings** | LangChain, OpenAI Embeddings |
| **Vector Store** | FAISS / Chroma |
| **Frontend Deployment** | Vercel |
| **Backend Deployment** | Render |
| **Streaming** | Server-Sent Events (SSE) |

---

## 🚀 Getting Started

### Prerequisites

- Python 3.11+
- An OpenAI key

### Installation

```bash
# Clone the repository
git clone https://github.com/pirisc/geology_agent_frontend.git
cd geology_agent_frontend

# Create a virtual environment
python -m venv venv
source venv/bin/activate  # On Windows: venv\Scripts\activate

# Install dependencies
pip install -r requirements.txt
```

### Environment Variables

Create a `.env` file in the root directory:

```env
OPENAI_API_KEY=your_openai_api_key_here

# Optional
LANGCHAIN_TRACING_V2=true
LANGCHAIN_API_KEY=your_langsmith_key
```

### Running Locally

```bash
uvicorn main:app --reload --port 8000
```

Then open `index.html` in your browser, or serve it with:

```bash
python -m http.server 3000
```

---


## 🔌 API Reference

### `POST /chat`

Sends a message to Rocky and streams the response.

**Request Body:**
```json
{
  "message": "What are the three types of rocks?",
  "thread_id": "optional-conversation-id"
}
```

**Response:** Server-Sent Events stream

```
data: {"thread_id": "abc123"}
data: {"content": "The three main"}
data: {"content": " types of rocks are..."}
data: [DONE]
```

---

## 🧠 How the RAG Pipeline Works

1. **Ingestion** — Geological texts, Wikipedia articles, and reference material are chunked and embedded into a vector store
2. **Retrieval** — When a user asks a question, the most semantically similar chunks are retrieved
3. **Augmentation** — Retrieved context is injected into the LLM prompt alongside the user's question
4. **Generation** — The LangGraph agent synthesizes a grounded, accurate response

---


## 🤝 Contributing

Contributions are welcome! Please open an issue first to discuss what you'd like to change.

```bash
git checkout -b feature/your-feature-name
git commit -m "feat: add your feature"
git push origin feature/your-feature-name
```

---

## 📄 License

This project is licensed under the MIT License. See [LICENSE](LICENSE) for details.

---

## 👩‍💻 Author

Built with 🪨 by **[pirisc](https://github.com/pirisc)**

*Part of an AI Engineering Bootcamp capstone project — integrating prompt engineering, LangGraph agents, RAG systems, and full-stack deployment.*

---

<div align="center">
  <sub>Rocky knows his rocks. Do you? 🌋</sub>
</div>
