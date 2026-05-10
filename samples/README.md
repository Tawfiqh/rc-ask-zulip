# Sample data

These fixtures let the app render with safe stub data instead of real Zulip
check-ins or saved conversations. Useful for screenshots, demos, and local
exploration without needing RC OAuth, Zulip credentials, or a running LLM.

Set both flags before starting the server:

```bash
DEV_AUTH_BYPASS=1 USE_SAMPLE_DATA=1 ./run.sh --no-ollama
```

When `USE_SAMPLE_DATA=1`, four endpoints are short-circuited to read these
files instead of hitting Zulip / the LLM / the local SQLite DB:

| Endpoint | Fixture |
|----------|---------|
| `GET /api/checkin-pair` | `checkin_sample.json` (wrapped under `grouped`) |
| `GET /conversations` | `conversations_list_sample.json` |
| `GET /conversation-data/{id}` | `conversation_sample.json` |
| `GET /ask?q=...` | `conversation_sample.json` |

Avatar images referenced from `checkin_sample.json` live in
`../static/sample/avatars/`. They are simple coloured-circle SVGs with
initials — no real photos.

The TUI in `Rc-Checkins-TUI/rcAskZulip` fetches the same
`/api/checkin-pair` endpoint, so it picks up the sample data automatically
once the server is running with these flags.
