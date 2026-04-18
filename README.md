# ai-diary
Personal AI-powered Telegram diary. n8n pipeline: RSS → Claude → Telegram
## Architecture
Schedule → 2 RSS → Merge → Filter (24h) → Aggregate → Claude Haiku → Telegram
## Stack

- **n8n** — pipeline orchestrator (Docker on Mac mini)
- **Claude Haiku 4.5** via OpenRouter — best-article selection + post generation
- **Telegram Bot API** — publishing
- **RSS sources**: TechCrunch, The Verge AI

## How it works

1. n8n pulls RSS from 2 sources on schedule
2. Merge combines the streams (~30 articles)
3. Filter keeps only articles from the last 24 hours
4. Aggregate packs them into a single array
5. Claude Haiku 4.5 receives the array, picks ONE best article based on criteria (industry impact, novelty) and writes a short Russian post with an emoji tag
6. Telegram Bot publishes to a private channel

## Prompt

See `workflow.json` — Basic LLM Chain node.

## Cost

~$1/month on OpenRouter (Claude Haiku).

## Status

🚧 Work in progress. Next steps:
- [ ] Human-in-the-loop approval via Telegram buttons
- [ ] Schedule Trigger (automated run)
- [ ] More RSS sources (markets, sports science)
- [ ] Duplicate detection
