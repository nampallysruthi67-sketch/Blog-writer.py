# AI Blog Writer

Outline first, then draft — with the response streaming token by token over Server-Sent Events.

**2 of 10** — part of a GenAI project series. FastAPI backend, vanilla JS frontend.

## What it demonstrates

- Streaming responses (SSE) instead of waiting on one blocking call
- Two-stage prompting: the model plans an outline, then writes against it
- Prompt parameters (tone, length, audience) wired to real generation config

## Run it

```bash
python -m venv .venv
source .venv/bin/activate        # Windows: .venv\Scripts\activate
pip install -r requirements.txt
cp .env.example .env             # Windows: copy .env.example .env
# add your key to .env  (skip if this project needs no key)
uvicorn main:app --reload
```

Open http://127.0.0.1:8000

## Keys

| Key | Where to get it | Where it goes |
|---|---|---|
| `GEMINI_API_KEY` | https://aistudio.google.com/apikey (free) | `.env` |

## Stack

FastAPI · google-genai · SSE

## How it works

`/api/outline` returns a JSON outline. `/api/draft` takes that outline back and streams the post as SSE chunks, which the browser appends as they arrive. Two stages beat one prompt because the model commits to a structure before it starts writing, so long posts do not wander.

---
MIT
