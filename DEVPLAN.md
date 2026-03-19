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

## M2 — Create GitHub repo + push ✅

- [x] Created `kiso-run/preset-basic` repo on GitHub (public)
- [x] `git init`, add remote, push
- [ ] Verify `kiso preset install basic` works end-to-end on VPS (needs Docker)

## M3 — Validate manifest against core ✅

- [x] `validate_preset_manifest()` returns no errors
- [x] All 4 tools exist in registry.json (websearch, browser, aider, docreader)
- [x] `load_preset()` correctly loads: name=basic, 4 tools, 3 behaviors
- **Note:** preset.toml uses `recipes = []` but core PresetManifest still has `skills` field (M773 rename not yet propagated to presets.py). No impact — field is empty. Core will be updated when recipe rename is fully complete.

## Known Issues

- browser tool requires Chromium system dep (installed via deps.sh, needs Docker)
- aider API key is provider-specific — no validation at install time
