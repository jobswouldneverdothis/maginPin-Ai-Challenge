# magicpin AI Challenge

This project implements a FastAPI-based merchant assistant for the magicpin AI Challenge. It receives merchant/category/trigger context from a judge harness, decides when to send WhatsApp-style messages, and responds to merchant/customer replies.

## Features

- FastAPI HTTP API with health and metadata endpoints
- Context ingestion for category, merchant, trigger, and customer data
- Trigger-driven outbound message generation
- Reply handling for auto-replies, hostility, and intent transitions
- Gemini integration with a safe fallback response path

## Project structure

- `bot.py` — main FastAPI app and business logic
- `judge_simulator.py` — evaluation harness used to test the bot
- `dataset/` — category, merchant, trigger, and customer seed data
- `requirements.txt` — Python dependencies
- `.env` — local environment variables

## Local setup

```bash
cd /Users/rudra/Desktop/sem-VI/maginPin-Ai-Challenge
source .venv/bin/activate
export GEMINI_API_KEY="your_valid_key_here"
export GEMINI_MODEL="gemini-2.0-flash"
uvicorn bot:app --host 0.0.0.0 --port 8080
```

## Health check

```bash
curl http://localhost:8080/v1/healthz
```

## Run the judge

```bash
cd /Users/rudra/Desktop/sem-VI/maginPin-Ai-Challenge
BOT_URL=http://localhost:8080 python3 judge_simulator.py
```

## Notes

- If port 8080 is already in use, stop the previous process before starting the app.
- The judge is the main end-to-end validation step for this challenge.
- The app uses a Gemini API call when a valid key is available; otherwise it falls back to safe default logic.
