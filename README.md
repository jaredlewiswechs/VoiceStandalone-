# Newton Voice Interface (Standalone)

If you're seeing:

- `500: INTERNAL_SERVER_ERROR`
- `Code: FUNCTION_INVOCATION_FAILED`

that means Vercel couldn't boot the Python function for this deployment.

## Run locally (fastest way to unblock)

```bash
python -m pip install -r requirements.txt
uvicorn app:app --host 0.0.0.0 --port 8000
```

Then open:

- App UI: `http://localhost:8000/`
- API docs: `http://localhost:8000/docs`
- Health check: `http://localhost:8000/health`

## Quick API smoke test

```bash
curl -sS http://127.0.0.1:8000/health
curl -sS -X POST http://127.0.0.1:8000/voice/ask \
  -H 'content-type: application/json' \
  -d '{"query":"build me a calculator"}'
```

## Vercel debugging tip

This repo includes an import guard in `api/index.py`.
If startup fails in Vercel, opening `/` or `/health` should return a JSON payload with the import exception type/message and traceback, instead of a generic crash page.
