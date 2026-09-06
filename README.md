# Anthropic MCP — course workspace

Notes and code from Anthropic's MCP courses. Each course is a top-level folder;
each lesson inside it is a self-contained [uv](https://github.com/astral-sh/uv)
project with its own `pyproject.toml` / `uv.lock` and, when it needs secrets,
its own `.env`.

```
.
├── Intro to MCP/                       # Course 1 — MCP chat CLI (local Ollama via LiteLLM proxy)
└── MCP Advanced Topics/                 # Course 2
    ├── Sampling Walkthrough/            # server asks the client to call an LLM
    ├── Notifications Walkthrough/       # logging + progress notifications over STDIO
    ├── Roots Walkthrough/               # chat CLI with filesystem roots + video conversion
    └── StreamableHTTP Transport/        # MCP server over Streamable HTTP
```

## Config & secrets

There is **one** `.gitignore`, at the repo root — it covers every lesson.
Each lesson keeps its **own** `.env`; nothing is shared. Where a lesson needs
one, copy its `.env.example` to `.env` next to the code and fill it in.
`load_dotenv()` finds the lesson-local `.env` first.

| Lesson | `.env` needed? |
| --- | --- |
| `Intro to MCP/` | Yes — `CLAUDE_MODEL`, dummy `ANTHROPIC_API_KEY`, `ANTHROPIC_BASE_URL=http://localhost:4000`, `USE_UV` (local Ollama via LiteLLM proxy). |
| `MCP Advanced Topics/Sampling Walkthrough/` | Yes — real `ANTHROPIC_API_KEY`. |
| `MCP Advanced Topics/Roots Walkthrough/` | Yes — real `ANTHROPIC_API_KEY` + `CLAUDE_MODEL`. Needs FFmpeg for video conversion. |
| `MCP Advanced Topics/Notifications Walkthrough/` | No — no LLM calls. |
| `MCP Advanced Topics/StreamableHTTP Transport/` | No — no LLM calls. |

No real secret is tracked by git (`.env` is ignored; `.env.example` is not).

## Running a lesson

```bash
cd "MCP Advanced Topics/Roots Walkthrough"       # pick a lesson
cp .env.example .env && $EDITOR .env             # only if the table says so
uv sync
uv run main.py                                    # or: uv run client.py
```
