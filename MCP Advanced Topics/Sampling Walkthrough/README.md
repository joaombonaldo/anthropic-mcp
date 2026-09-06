# MCP Logging and Progress Demo

## Setup

Needs a real `ANTHROPIC_API_KEY`. Copy `.env.example` to `.env` in this folder
and fill it in — `client.py` calls `load_dotenv()` and picks it up.

Install dependencies using uv:

```bash
uv sync
```

## Running the Project

Run the MCP client:

```bash
uv run client.py
```
