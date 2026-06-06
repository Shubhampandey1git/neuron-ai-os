# Contributing to Neuron-AI OS

First off — thank you! Whether you're fixing a typo or adding a whole new tool, every contribution matters. This guide will get you from zero to merged PR.

---

## 📋 Table of Contents

- [Before You Start](#before-you-start)
- [Setting Up Locally](#setting-up-locally)
- [Branch Naming](#branch-naming)
- [Making Changes](#making-changes)
- [Running Tests](#running-tests)
- [Opening a PR](#opening-a-pr)
- [PR Checklist](#pr-checklist)
- [Code Style](#code-style)
- [Questions?](#questions)

---

## Before You Start

1. **Check existing issues** — your idea or bug might already be tracked. Search [open issues](../../issues).
2. **For large features**, open an issue first and describe your plan. Saves everyone time.
3. **For small fixes** (typos, docs, obvious bugs) — just open the PR directly.

---

## Setting Up Locally

```bash
# 1. Fork the repo on GitHub, then clone your fork
git clone https://github.com/Shubhampandey1git/neuron-ai-os.git
cd neuron-ai-os

# 2. Add the upstream remote (to pull future updates)
git remote add upstream https://github.com/Shubhampandey1git/neuron-ai-os.git

# 3. Create a virtual environment
python -m venv .venv
source .venv/bin/activate      # Windows: .venv\Scripts\activate

# 4. Install all dependencies including dev tools
pip install -r requirements.txt
pip install -r requirements-dev.txt   # ruff, pytest, pytest-asyncio, etc.

# 5. Copy the example env
cp .env.example .env

# 6. (Optional) Pull Ollama model if you want to run integration tests
ollama pull mistral

# 7. Start the server
uvicorn app.main:app --reload
```

Visit `http://localhost:8000/docs` — you should see the FastAPI Swagger UI.

---

## Branch Naming

Always branch off `main`. Use these prefixes:

| Prefix | When to use | Example |
|--------|-------------|---------|
| `feat/` | New features | `feat/plugin-system` |
| `fix/` | Bug fixes | `fix/whisper-timeout-crash` |
| `docs/` | Documentation only | `docs/update-setup-guide` |
| `refactor/` | Code cleanup, no behavior change | `refactor/agent-chain-split` |
| `test/` | Adding or fixing tests | `test/chroma-memory-unit` |
| `chore/` | Deps, CI, config | `chore/bump-langchain-0.3` |

```bash
# Example
git checkout -b feat/web-search-tool
```

---

## Making Changes

- Keep PRs **focused** — one feature or fix per PR. Reviewers (and future-you) will thank you.
- Write or update **tests** for any behavior change.
- If you add a new LangChain tool, add it to `app/tools/` and register it in `app/tools/__init__.py`.
- If you change the `.env.example`, document the new variable in the README config table.

---

## Running Tests

```bash
# Fast unit tests only (no Ollama needed — LLM is mocked)
pytest tests/unit/ -v

# Full suite including integration (requires Ollama running)
pytest tests/ -v

# With coverage report
pytest tests/unit/ --cov=app --cov-report=term-missing

# Lint check (must pass before opening PR)
ruff check .
ruff format --check .

# Auto-fix lint issues
ruff check . --fix
ruff format .
```

The CI runs `tests/unit/` only — no Ollama is available in GitHub Actions. Keep unit tests fast and mocked.

---

## Opening a PR

1. Push your branch to **your fork**:
   ```bash
   git push origin feat/your-feature
   ```
2. Open a PR against `main` of this repo.
3. Fill out the PR template completely — incomplete templates will be sent back.
4. Link any related issues with `Closes #123` in the PR description.

---

## PR Checklist

Before marking your PR as ready for review:

- [ ] Tests added or updated for the change
- [ ] `pytest tests/unit/` passes locally
- [ ] `ruff check .` and `ruff format --check .` pass
- [ ] No new Ollama/Whisper calls in unit tests (mock them)
- [ ] `.env.example` updated if you added a new env variable
- [ ] PR description explains *why*, not just *what*

---

## Code Style

We use **[ruff](https://github.com/astral-sh/ruff)** for both linting and formatting. Config lives in `pyproject.toml`. A few conventions:

- Type hints on all function signatures in `app/`
- Docstrings on public functions and classes (NumPy style)
- Async all the way down — `async def` for any I/O in routes and tools
- No `print()` statements — use the logger: `from app.core.logging import logger`

---

## Questions?

Open a [Discussion](../../discussions) or drop a comment on an issue. This is a solo-maintained project so responses may take a day or two — but they will come!
