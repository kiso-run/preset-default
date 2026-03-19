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
- [ ] Verify `kiso preset install default` works end-to-end on VPS (needs Docker)

## M3 — Validate manifest against core ✅

- [x] `validate_preset_manifest()` returns no errors
- [x] All 4 tools exist in registry.json
- [x] `load_preset()` correctly loads manifest
- **Note:** preset.toml uses `recipes = []` but core PresetManifest still has `skills` field (M773 rename not yet propagated to presets.py). No impact — field is empty.

## M4 — Rename basic → default + add transcriber, ocr

**Rename:**
- [ ] Rename `name` in preset.toml: `basic` → `default`
- [ ] Update description: "Default preset — all general-purpose tools for a complete assistant"
- [ ] Update README.md title, install commands, description
- [ ] Update remote: `git remote set-url origin git@github.com:kiso-run/preset-default.git`
- [ ] Push to new repo `kiso-run/preset-default`
- [ ] Update core `registry.json`: rename `basic` → `default`, update description
- [ ] Rename local directory `preset-basic` → `preset-default`

**Add tools:**
- [ ] Add `transcriber` to tools list (voice messages → text via Gemini)
- [ ] Add `ocr` to tools list (image → text via Gemini vision)

**Update behaviors:**
- [ ] Add behavior: "When the user sends a voice message or audio file, use transcriber to convert it to text before proceeding."
- [ ] Add behavior: "When the user sends a photo or image, use ocr to extract text if the image contains text, or describe to understand visual content."
- [ ] Update docreader behavior to mention OCR fallback: "When docreader reports no extractable text in a PDF (scanned document), convert pages to images and use ocr."

**Validation:**
- [ ] `validate_preset_manifest()` returns no errors
- [ ] All 6 tools exist in registry.json
- [ ] Push to `kiso-run/preset-default`

## Known Issues

- browser tool requires Chromium system dep (installed via deps.sh, needs Docker)
- aider API key is provider-specific — no validation at install time
- transcriber and ocr both use KISO_LLM_API_KEY (OpenRouter) — no extra keys needed
