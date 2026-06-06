# 🧠 Neuron-AI OS

<div align="center">

[![CI](https://github.com/Shubhampandey1git/neuron-ai-os/actions/workflows/ci.yml/badge.svg)](https://github.com/Shubhampandey1git/neuron-ai-os/actions/workflows/ci.yml)
[![Python](https://img.shields.io/badge/python-3.11+-blue?logo=python&logoColor=white)](https://www.python.org/)
[![FastAPI](https://img.shields.io/badge/FastAPI-0.110+-009688?logo=fastapi&logoColor=white)](https://fastapi.tiangolo.com/)
[![LangChain](https://img.shields.io/badge/LangChain-0.2+-1C3C3C?logo=chainlink&logoColor=white)](https://langchain.com/)
[![Ollama](https://img.shields.io/badge/Ollama-local%20LLM-black)](https://ollama.ai/)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)
[![PRs Welcome](https://img.shields.io/badge/PRs-welcome-brightgreen.svg)](CONTRIBUTING.md)
[![Code style: ruff](https://img.shields.io/endpoint?url=https://raw.githubusercontent.com/astral-sh/ruff/main/assets/badge/v2.json)](https://github.com/astral-sh/ruff)

**A fully local, privacy-first AI assistant that runs on your machine — no cloud, no API keys, no data leaving your device.**

[Features](#-features) · [Architecture](#-architecture) · [Quick Start](#-getting-started-in-5-commands) · [Contributing](CONTRIBUTING.md) · [Roadmap](#-roadmap)

</div>

---

<!-- Add your demo GIF to docs/demo.gif and uncomment the line below -->
> 📸 **Demo incoming** — recording a walkthrough shortly. Star the repo to get notified.
>
> *Voice → Whisper → LangChain Agent → Ollama (llama3.2) → OS tools + RAG retrieval*

---

## ✨ Features

| Feature | Status | Tech |
|--------|--------|------|
| 🎤 Voice input (fully offline) | ✅ Live | OpenAI Whisper |
| 🤖 Local LLM reasoning | ✅ Live | Ollama + llama3.2 |
| 🗂️ RAG over your documents | ✅ Live | ChromaDB + LangChain |
| 🖥️ OS tool execution (files, apps, shell) | ✅ Live | LangChain Tools |
| 🌐 REST API | ✅ Live | FastAPI |
| 💬 Conversation memory | ✅ Live | In-memory context |
| 🔌 Plugin system | 🚧 Planned | — |

---

## 🏗️ Architecture

```
┌─────────────────────────────────────────────────────────┐
│                     User Interface                      │
│              (Voice / REST API / Chat UI)               │
└──────────────────────┬──────────────────────────────────┘
                       │
┌──────────────────────▼──────────────────────────────────┐
│                   FastAPI Server                        │
│              app/api/  (routes + schemas)               │
└──────┬─────────────────────────────┬────────────────────┘
       │                             │
┌──────▼──────┐             ┌────────▼────────┐
│  Voice Core │             │  LangChain Agent │
│  (Whisper)  │             │  app/core/       │
│  app/voice/ │             │  agent.py        │
└──────┬──────┘             └────────┬─────────┘
       │                    ┌────────┴──────────────┐
       │              ┌─────▼──────┐   ┌────────────▼────┐
       └──────────────►   Ollama   │   │   Tool Router   │
                      │ (Local LLM)│   │   app/tools/    │
                      └────────────┘   └────────┬────────┘
                                                │
                      ┌─────────────────────────┼──────────────────┐
                      │                         │                  │
               ┌──────▼──────┐        ┌─────────▼──────┐  ┌───────▼────┐
               │  ChromaDB   │        │   OS Executor   │  │ Web Tools  │
               │  (RAG store)│        │  (apps, shell,  │  │ (search)   │
               └─────────────┘        │   system info)  │  └────────────┘
                                      └─────────────────┘
```

---

## 🚀 Getting Started in 5 Commands

**Prerequisites:** Python 3.11+, [Ollama](https://ollama.ai) installed

```bash
# 1. Clone and enter the repo
git clone https://github.com/Shubhampandey1git/neuron-ai-os.git && cd neuron-ai-os

# 2. Set up a virtual environment and install dependencies
python -m venv .venv && source .venv/bin/activate
pip install -r requirements.txt

# 3. Pull your local model
ollama pull llama3.2:3b

# 4. Copy config
cp .env.example .env

# 5. Start the assistant
uvicorn app.main:app --reload
```

Then open `http://localhost:8000/docs` to explore the API, or send your first query:

```bash
curl -X POST http://localhost:8000/chat \
  -H "Content-Type: application/json" \
  -d '{"message": "What files did I modify today?"}'
```

---

## 📁 Project Structure

```
neuron-ai-os/
├── app/
│   ├── api/              # FastAPI routes and Pydantic schemas
│   ├── core/             # LangChain agent, prompt templates
│   ├── memory/           # ChromaDB setup and RAG pipeline
│   ├── tools/            # OS, file, and web tools (LangChain Tools)
│   └── voice/            # Whisper transcription pipeline
├── tests/
│   ├── unit/             # Fast mocked tests — no Ollama needed
│   └── integration/      # End-to-end tests (requires Ollama)
├── docs/                 # Architecture diagrams, demo GIF
├── scripts/              # Helper scripts (setup, model pull)
├── .github/
│   ├── workflows/        # GitHub Actions CI
│   ├── ISSUE_TEMPLATE/   # Bug report + feature request templates
│   └── PULL_REQUEST_TEMPLATE.md
├── .env.example
├── pyproject.toml        # ruff + pytest config
├── requirements.txt
└── requirements-dev.txt
```

---

## ⚙️ Configuration

Copy `.env.example` to `.env` and adjust:

```env
# Model settings
OLLAMA_BASE_URL=http://localhost:11434
OLLAMA_MODEL=llama3.2:3b

# Memory
CHROMA_PERSIST_DIR=./data/chroma

# Voice
WHISPER_MODEL_SIZE=base   # tiny | base | small | medium | large

# API
API_HOST=0.0.0.0
API_PORT=8000
LOG_LEVEL=info
```

---

## 🗺️ Roadmap

- [ ] **v0.2** — Plugin architecture for custom tools
- [ ] **v0.3** — Web UI (chat frontend)
- [ ] **v0.4** — Text-to-speech response output
- [ ] **v0.5** — Scheduled tasks ("remind me every morning")
- [ ] **v1.0** — One-click installer script

Track progress on the [Issues](https://github.com/Shubhampandey1git/neuron-ai-os/issues) board.

---

## 🤝 Contributing

Contributions are welcome! See [CONTRIBUTING.md](CONTRIBUTING.md) for how to get started.
First time contributing to open source? Look for [`good first issue`](https://github.com/Shubhampandey1git/neuron-ai-os/labels/good%20first%20issue) labels.

---

## 📄 License

MIT © 2026 [Shubham Pandey](https://github.com/Shubhampandey1git)

---

<div align="center">
  <sub>Built with ❤️ and zero cloud dependencies.</sub>
</div>
