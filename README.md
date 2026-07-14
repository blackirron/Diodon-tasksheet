# Diodon

Forked from the sprint's base FastAPI template.

**What it does:** a dual-tab capture tool — Clipboard (yellow) and Tasksheet
(blue). Paste/type into the shared capture box, select the part you want
(or leave the whole box selected), and send it to either list with one
click. Items can be moved between the two lists, checked off (tasksheet),
copied (clipboard), or deleted. Persists in your browser via localStorage.

**Why it exists:** a fast scratch space for grabbing snippets while
working, without deciding up front whether something's a note or a task.

**Live demo:** [link once deployed]

**Note:** this app does NOT use any LLM — no API key needed at all.
Everything runs client-side; the backend just serves the page.

---

## Running locally

```bash
# 1. Create and activate a virtual environment
python -m venv venv
source venv/bin/activate      # Windows: venv\Scripts\activate

# 2. Install dependencies
pip install -r requirements.txt

# 3. Set up your environment variables
cp .env.example .env
# then edit .env and paste your real ANTHROPIC_API_KEY

# 4. Run the dev server (auto-reloads on code changes)
uvicorn app.main:app --reload
```

Visit `http://localhost:8000/docs` — FastAPI auto-generates an interactive
API tester here. This is the fastest way to try your endpoints without
building a frontend first.

## Running with Docker

```bash
docker build -t my-app .
docker run -p 8000:8000 --env-file .env my-app
```

## Project structure

```
app/
├── core/       config + auth
├── routers/    HTTP endpoints (thin — no logic)
├── services/   actual logic (Claude API calls, etc.)
└── main.py     wires it together
```

## Adding a new feature to this app

1. Create `app/services/your_feature.py` — the actual logic
2. Create `app/routers/your_feature.py` — request/response models + thin endpoint (copy `chat.py`'s pattern)
3. Register it in `app/main.py`: `app.include_router(your_feature.router)`

## Deployment

Deployed on: [Railway / Render / Fly.io — fill in]

Environment variables to set on the platform dashboard:
- `LLM_PROVIDER` (`groq` by default — free, no card required)
- `GROQ_API_KEY` (get one free at https://console.groq.com/keys)
- `API_AUTH_TOKEN`
- `ENVIRONMENT=production`
- `ALLOWED_ORIGINS` (your frontend's real URL)
