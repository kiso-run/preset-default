# preset-basic — Development Plan

Starter preset for Kiso. Installs core tools (websearch, browser, aider, docreader) and configures behavioral guidelines for a general-purpose assistant.

## Architecture

```
preset.toml → kiso preset install → installs tools + injects behaviors
```

- **Manifest**: `preset.toml` declares tools, behaviors, and env var requirements
- **No code**: presets are pure configuration — no run.py, no pyproject.toml
- **Install flow**: `kiso preset install basic` → core reads manifest → installs each tool → saves behaviors to session knowledge

## M1 — Initial manifest + docs ✅

- [x] `preset.toml` with 4 tools (websearch, browser, aider, docreader)
- [x] 3 behavioral guidelines (document awareness, research strategy, code editing)
- [x] README.md with install instructions, tool table, API key requirements
- [x] LICENSE (MIT)

## M2 — Create GitHub repo + push

- [ ] Create `kiso-run/preset-basic` repo on GitHub (public)
- [ ] `git init`, add remote, push
- [ ] Verify `kiso preset install basic` works end-to-end on VPS

## M3 — Validate manifest against core

- [ ] Run `validate_preset_manifest()` on preset.toml (unit test or manual)
- [ ] Verify all 4 tools exist in registry.json
- [ ] Verify behaviors are injected after install
- [ ] Verify `kiso preset remove basic` cleans up behaviors

## Known Issues

- browser tool requires Chromium system dep (installed via deps.sh, needs Docker)
- aider API key is provider-specific — no validation at install time
