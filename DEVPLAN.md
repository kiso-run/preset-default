# preset-default — Development Plan

Default preset for Kiso. Installs all general-purpose tools and configures behavioral guidelines for a complete assistant.

## Architecture

```
preset.toml → kiso preset install → installs tools + injects behaviors
```

- **Manifest**: `preset.toml` declares tools, behaviors, and env var requirements
- **No code**: presets are pure configuration — no run.py, no pyproject.toml
- **Install flow**: `kiso preset install default` → core reads manifest → installs each tool → saves behaviors to session knowledge

## M1 — Initial manifest + docs ✅

- [x] `preset.toml` with 4 tools (websearch, browser, aider, docreader)
- [x] 3 behavioral guidelines (document awareness, research strategy, code editing)
- [x] README.md with install instructions, tool table, API key requirements
- [x] LICENSE (MIT)

## M2 — Create GitHub repo + push ✅

- [x] Created `kiso-run/preset-basic` repo on GitHub (public)
- [x] `git init`, add remote, push
- [ ] Verify `kiso preset install default` works end-to-end on VPS (needs Docker). *Manual integration test — requires a configured kiso instance + Docker; not suitable for autonomous execution. Run by maintainer with: `kiso instance create test`, `kiso instance use test`, `kiso preset install default`, then check that all 6 tools install and behaviors are loaded into the instance's session knowledge.*

## M3 — Validate manifest against core ✅

- [x] `validate_preset_manifest()` returns no errors
- [x] All 4 tools exist in registry.json
- [x] `load_preset()` correctly loads manifest
- **Note:** preset.toml uses `recipes = []` but core PresetManifest still has `skills` field (M773 rename not yet propagated to presets.py). No impact — field is empty.

## M4 — Rename basic → default + add transcriber, ocr

**Rename:**
- [x] Renamed `name` in preset.toml: `basic` → `default`, version 0.1.0 → 0.2.0
- [x] Updated description: "Default preset — all general-purpose tools for a complete assistant"
- [x] Updated README.md: title, tool table (6 tools), behaviors (6), install commands
- [x] Updated remote to `git@github.com:kiso-run/preset-default.git`
- [x] Push to `kiso-run/preset-default`
- [x] Core `registry.json` updated
- [x] Rename local directory `preset-basic` → `preset-default` (cosmetic, do manually)

**Add tools:**
- [x] Added `transcriber` to tools list
- [x] Added `ocr` to tools list

**Update behaviors:**
- [x] Added voice message → transcriber behavior
- [x] Added photo/image → ocr behavior
- [x] Added scanned PDF → ocr fallback behavior

**Validation:**
- [x] `validate_preset_manifest()` returns no errors
- [x] All 6 tools exist in registry.json (websearch, browser, aider, docreader, transcriber, ocr)
- [x] `load_preset()` loads: name=default, 6 tools, 6 behaviors

## Known Issues

- browser tool requires Chromium system dep (installed via deps.sh, needs Docker)
- aider API key is provider-specific — no validation at install time
- transcriber and ocr both use KISO_LLM_API_KEY (OpenRouter) — no extra keys needed
