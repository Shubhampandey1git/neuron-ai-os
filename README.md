# 🧠 Neuron AI OS

<div align="center">

[![CI](https://github.com/Shubhampandey1git/neuron-ai-os/actions/workflows/ci.yml/badge.svg)](https://github.com/Shubhampandey1git/neuron-ai-os/actions/workflows/ci.yml)
[![Python](https://img.shields.io/badge/python-3.11+-blue?logo=python&logoColor=white)](https://www.python.org/)
[![FastAPI](https://img.shields.io/badge/FastAPI-0.110+-009688?logo=fastapi&logoColor=white)](https://fastapi.tiangolo.com/)
[![LangChain](https://img.shields.io/badge/LangChain-0.2+-1C3C3C?logo=chainlink&logoColor=white)](https://langchain.com/)
[![Ollama](https://img.shields.io/badge/Ollama-local%20LLM-black)](https://ollama.ai/)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)
[![PRs Welcome](https://img.shields.io/badge/PRs-welcome-brightgreen.svg)](CONTRIBUTING.md)
[![Code style: ruff](https://img.shields.io/endpoint?url=https://raw.githubusercontent.com/astral-sh/ruff/main/assets/badge/v2.json)](https://github.com/astral-sh/ruff)

**A cognitive AI architecture, built in layers — perception, memory, reasoning, planning, action, learning, and self-evaluation.**

*Starting as a fully local voice assistant. Built to grow into a self-improving, multimodal AI operating system.*

[Vision](#-vision) · [Architecture](#-cognitive-architecture) · [V1 — What's Live Now](#-v1--whats-live-now) · [Roadmap](#-roadmap) · [Quick Start](#-getting-started-in-5-commands) · [Contributing](CONTRIBUTING.md)

</div>

---

> 📸 **Demo incoming** — recording a walkthrough of V1 shortly. Star the repo to get notified.

---

## 🌌 Vision

Neuron AI OS is not a chatbot, a RAG wrapper, or a single model fine-tuned for a task. It's a long-term attempt to build a **cognitive architecture** — a system that perceives, remembers, reasons, plans, acts, learns, and evaluates itself, all under one coherent design.

Every component exists to serve a specific cognitive function, not because the technology is trendy. The project is built incrementally, one functional layer at a time, starting with a working local assistant (V1) and growing toward a self-improving multimodal AI OS (V5).

**Core principle:** the system should never become "another chatbot." It should remember, see, hear, reason, plan, act, learn, evaluate itself, and improve over time.

---

## 🧩 Cognitive Architecture

Neuron is designed across eight functional layers. Not all layers exist yet — see [Roadmap](#-roadmap) for what's built versus planned.

| Layer | Purpose | Key Components | Status |
|-------|---------|-----------------|--------|
| **1. Perception** | Understand the world across modalities | Speech recognition, OCR, computer vision, screen understanding | 🟢 Voice live, rest planned |
| **2. Memory** | Remember and retrieve information | RAG, vector DBs, embeddings, knowledge graphs, episodic/semantic memory | 🟢 RAG live |
| **3. Reasoning** | Think through problems | LLMs, multi-step reasoning, context understanding | 🟢 Live (Ollama) |
| **4. Planning** | Decide what should happen next | Agent architectures, task decomposition, goal planning | 🟡 Basic routing live, full planner planned |
| **5. Action** | Interact with systems | Tool calling, file ops, OS actions, API integration | 🟢 Live (OS tools) |
| **6. Learning** | Improve from experience | Reinforcement learning, reward functions, preference learning | 🔴 Planned (V4) |
| **7. Creation** | Generate new information | GANs, diffusion models, synthetic data | 🔴 Planned (V5) |
| **8. Self-Evaluation** | Analyze its own performance | Critic models, reward models, failure analysis | 🔴 Planned (V5) |

---

## ✅ V1 — What's Live Now

V1 is the functional foundation: a fully local voice assistant covering Perception (voice), Memory (RAG), Reasoning (LLM), and Action (OS tools).

| Feature | Status | Tech |
|--------|--------|------|
| 🎤 Voice input (fully offline) | ✅ Live | OpenAI Whisper |
| 🤖 Local LLM reasoning | ✅ Live | Ollama (llama3.2 or any local model) |
| 🗂️ RAG over your documents | ✅ Live | ChromaDB + LangChain |
| 🖥️ OS tool execution (files, apps, shell) | ✅ Live | LangChain Tools |
| 🌐 REST API | ✅ Live | FastAPI |
| 💬 Conversation memory | ✅ Live | In-memory context |
| 🔌 Plugin system | 🚧 In progress | — |

No cloud. No API keys. No data leaving your device.

### V1 System Diagram

```
┌─────────────────────────────────────────────────────────┐
│                     User Interface                      │
│              (Voice / REST API / Chat UI)                │
└──────────────────────┬──────────────────────────────────┘
                       │
┌──────────────────────▼──────────────────────────────────┐
│                   FastAPI Server                         │
│              app/api/  (routes + schemas)                │
└──────┬─────────────────────────────┬─────────────────────┘
       │                             │
┌──────▼──────┐             ┌────────▼────────┐
│  Voice Core │             │  LangChain Agent │
│  (Whisper)  │             │  app/core/       │
│  app/voice/ │             │  agent.py        │
└──────┬──────┘             └────────┬─────────┘
       │                    ┌────────┴──────────────┐
       │              ┌─────▼──────┐   ┌────────────▼────┐
       └──────────────►   Ollama   │   │   Tool Router    │
                      │ (Local LLM)│   │   app/tools/      │
                      └────────────┘   └────────┬──────────┘
                                                │
                      ┌─────────────────────────┼──────────────────┐
                      │                         │                  │
               ┌──────▼──────┐        ┌─────────▼──────┐  ┌───────▼────┐
               │  ChromaDB   │        │   OS Executor   │  │ Web Tools  │
               │  (RAG store)│        │  (apps, shell,  │  │ (search)   │
               └─────────────┘        │   system info)  │  └────────────┘
                                      └──────────────────┘
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
│   ├── core/              # LangChain agent, prompt templates
│   ├── memory/            # ChromaDB setup and RAG pipeline
│   ├── tools/              # OS, file, and web tools (LangChain Tools)
│   └── voice/              # Whisper transcription pipeline
├── tests/
│   ├── unit/                # Fast mocked tests — no Ollama needed
│   └── integration/        # End-to-end tests (requires Ollama)
├── docs/                  # Architecture diagrams, demo GIF
├── scripts/               # Helper scripts (setup, model pull)
├── .github/
│   ├── workflows/         # GitHub Actions CI
│   ├── ISSUE_TEMPLATE/    # Bug report + feature request templates
│   └── PULL_REQUEST_TEMPLATE.md
├── .env.example
├── pyproject.toml         # ruff + pytest config
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

The long-term plan moves through five major versions, each adding a new cognitive layer.

### V1 — Functional Assistant *(current)*
Local LLM · RAG memory · voice interface · tool usage · file interaction.
**Goal:** a working AI operating system assistant.

### V2 — Multimodal Perception
Vision module · OCR · image understanding · screen analysis.
**Goal:** make Neuron multimodal.

### V3 — Planning & Agents
Planning system · agent architecture · multi-agent coordination.
**Goal:** let Neuron break down and solve complex, multi-step tasks.

### V4 — Learning
Reinforcement learning · adaptive decision-making · reward optimization.
**Goal:** let Neuron learn which actions produce the best outcomes.

### V5 — Self-Improving Ecosystem
Synthetic data generation · self-evaluation · continuous improvement.
**Goal:** a system that critiques and improves its own performance over time.

Track progress on the [Issues](https://github.com/Shubhampandey1git/neuron-ai-os/issues) board — each version will get its own milestone.

---

## 🤝 Contributing

Contributions are welcome at any layer of the architecture — from a V1 bug fix to proposing how a future planning or learning module should work. See [CONTRIBUTING.md](CONTRIBUTING.md) for how to get started.

First time contributing to open source? Look for [`good first issue`](https://github.com/Shubhampandey1git/neuron-ai-os/labels/good%20first%20issue) labels.

---

## 📄 License

MIT © 2026 [Shubham Pandey](https://github.com/Shubhampandey1git)

---

<div align="center">
  <sub>Built with ❤️, zero cloud dependencies, and a long-term plan.</sub>
</div>
