# preset-default

Default preset for Kiso — installs general-purpose tools for a complete AI assistant.

## What's included

| Tool | Purpose |
|------|---------|
| **browser** | Browser automation (navigate, screenshot, interact) |
| **aider** | AI-powered code editing |
| **docreader** | Read PDF, DOCX, XLSX, CSV, and plain text files |
| **transcriber** | Transcribe voice messages and audio files to text |
| **ocr** | Extract text from photos, screenshots, receipts, whiteboards |

## Behaviors

The preset configures five behavioral guidelines:

- **Document awareness**: When the user sends a file, use docreader first
- **Code editing**: use aider for code changes, not exec tasks
- **Voice messages**: use transcriber to convert audio to text before proceeding
- **Image text**: use ocr to extract text from photos, or describe for visual content
- **Scanned PDFs**: when docreader finds no text, convert pages to images and use ocr

## Install

```bash
kiso preset install default
```

This will:
1. Install all five tools (clone repos, set up venvs, run deps.sh)
2. Inject the behavioral guidelines into the session knowledge

## API keys

All tools use `KISO_LLM_API_KEY` (OpenRouter) by default — the same key kiso already has. No extra configuration needed.

To use a different LLM provider for aider (e.g., Claude for code editing):
```bash
kiso env set KISO_TOOL_AIDER_API_KEY sk-your-key
```

## Remove

```bash
kiso preset remove default
```

Removes the behavioral guidelines. Tools are kept (remove individually with `kiso tool remove <name>`).
