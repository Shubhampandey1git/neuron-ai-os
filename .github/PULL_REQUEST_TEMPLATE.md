## What does this PR do?

<!-- A clear one-paragraph description of the change and why it's needed. -->

## Type of change

- [ ] Bug fix (non-breaking change that fixes an issue)
- [ ] New feature (non-breaking change that adds functionality)
- [ ] Breaking change (fix or feature that changes existing behaviour)
- [ ] Documentation update
- [ ] Refactor / cleanup (no behaviour change)
- [ ] CI / tooling

## Related issues

Closes #<!-- issue number -->

## How was this tested?

<!-- Describe what you tested and how. "I ran pytest" is not enough — be specific. -->

## Checklist

- [ ] `pytest tests/unit/` passes locally
- [ ] `ruff check .` and `ruff format --check .` pass
- [ ] No Ollama or Whisper calls in unit tests (all mocked)
- [ ] New env variables added to `.env.example` and README config table
- [ ] Docstrings added for any new public functions or classes
- [ ] PR title follows conventional commit format (`feat:`, `fix:`, `docs:`, etc.)

## Screenshots / recordings (if UI change)

<!-- Drop a GIF or screenshot here if this touches the chat UI -->
