# preset-basic

Starter kit for Kiso — installs the core tools for a general-purpose AI assistant.

## What's included

| Tool | Purpose |
|------|---------|
| **websearch** | Web search via Brave Search API |
| **browser** | Browser automation (navigate, screenshot, interact) |
| **aider** | AI-powered code editing |
| **docreader** | Read PDF, DOCX, XLSX, CSV, and plain text files |

## Behaviors

The preset configures three behavioral guidelines:

- **Document awareness**: When the user sends a file, use docreader first
- **Research strategy**: websearch for quick answers, browser for deep inspection
- **Code editing**: use aider for code changes, not exec tasks

## Install

```bash
kiso preset install basic
```

This will:
1. Install all four tools (clone repos, set up venvs, run deps.sh)
2. Inject the behavioral guidelines into the session knowledge
3. Prompt for required API keys (websearch, aider)

## Required API keys

| Tool | Env var | How to get |
|------|---------|-----------|
| websearch | `KISO_TOOL_WEBSEARCH_API_KEY` | [Brave Search API](https://brave.com/search/api/) |
| aider | `KISO_TOOL_AIDER_API_KEY` | Your LLM provider API key |

Set via `kiso env set <KEY> <VALUE>`.

## Remove

```bash
kiso preset remove basic
```

Removes the behavioral guidelines. Tools are kept (remove individually with `kiso tool remove <name>`).
