# Anthropic MCP — course workspace

Notes and code from Anthropic's MCP courses. Each course is a top-level folder;
each lesson inside it is a self-contained [uv](https://github.com/astral-sh/uv)
project with its own `pyproject.toml` / `uv.lock` / `.env`.

```
.
├── Intro to MCP/                  # Course 1 — MCP chat CLI (local Ollama via LiteLLM proxy)
│   ├── .env                       # git-ignored
│   └── .env.example
└── MCP Advanced Topics/            # Course 2
    └── Sampling Walkthrough/       # server asks the client to call an LLM
        ├── .env                    # git-ignored
        └── .env.example
```

## Environment / secrets

Each lesson keeps its **own** `.env` — nothing is shared. Copy the
`.env.example` next to the code you want to run and fill it in.

| Lesson | Needs |
| --- | --- |
| `Intro to MCP/` | `CLAUDE_MODEL`, dummy `ANTHROPIC_API_KEY`, `ANTHROPIC_BASE_URL=http://localhost:4000`, `USE_UV` — runs a local Ollama model through a LiteLLM proxy. |
| `MCP Advanced Topics/Sampling Walkthrough/` | a real `ANTHROPIC_API_KEY` — calls the Anthropic API directly. |

No real secret is tracked by git (`.env` is ignored; `.env.example` is not).

## Running a lesson

```bash
cd "MCP Advanced Topics/Sampling Walkthrough"   # or "Intro to MCP"
cp .env.example .env && $EDITOR .env
uv sync
uv run client.py                                # Intro to MCP: uv run main.py
```
