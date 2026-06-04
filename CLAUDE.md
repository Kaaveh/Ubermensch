# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## What this repository is

Ubermensch (ابرانسان) is a **multilingual, content-only repository** — a science/philosophy guide to holistic health (body, brain, mind) covering biomarkers, nutrition, sleep, mindfulness, and stress management. There is no application code, no build system, no tests. Contributions are Markdown chapters and supporting images.

**English at the repo root is canonical.** Other languages live in flat per-language subdirectories (`fa/` today; `de/`, `fr/`, `ko/`, `ja/` planned). When source content changes, the English version is the source of truth; translations should be updated to match.

## Repository structure

- `README.md` — English landing page; the **"Chapters" section is the canonical index** of published chapters and must be updated whenever a chapter is added or renamed.
- `<chapter-slug>.md` — each chapter lives as a single English Markdown file at the repo root (e.g. `measurement-importance.md`, `uv-index.md`). Filenames are lowercase-kebab-case English regardless of which translation you're reading.
- `<lang>/` — one subdirectory per non-English language, mirroring the root file structure exactly (`<lang>/README.md`, `<lang>/measurement-importance.md`, …). Currently only `fa/` (Persian) exists.
- `asset/` — all images, shared by every language. Naming convention is `<chapter-slug>-<topic>.<ext>` (e.g. `measurement-baseline.png`, `uv-earth.png`) so an image's owning chapter is obvious from its name.

## Translation conventions

- **Filename parity.** A translation file's basename mirrors its English counterpart exactly — `fa/uv-index.md`, not `fa/uv-index-fa.md`. Makes missing translations easy to spot via `ls`.
- **Image paths depend on file depth.** Files at the repo root reference `asset/foo.png`. Files under `<lang>/` reference `../asset/foo.png`. `asset/` is never duplicated per language.
- **Language switcher header.** Every Markdown file's first content line is a one-line nav, with the current language in **bold** and the others as links. Templates:
  - At root (EN): `🌐 **English** · [فارسی](fa/<same-filename>.md)`
  - In `fa/`: `🌐 [English](../<same-filename>.md) · **فارسی**`
  - When a new language is added (e.g. `de/`), append it to this header in every file across every language.
- **Tone parity.** Translations preserve the conversational, first-person, slightly playful voice of the canonical English (e.g. "the world is a tradeoff! 🤭"). Don't formalize.
- **Mixed-script terms.** Technical terms (Resting heart rate, WHO, UVA/UVB/UVC, DNA, etc.) stay in Latin script in every language. In Persian, English loanwords transliterated in Persian script (e.g. «بایومارکر», «بیس‌لاین», «ایندیکیتور») are also expected — don't rewrite them into formal Persian equivalents.
- **Image references and breaks.** Append `</br>` after an image line when a line break is wanted before the next paragraph — this matches the existing pattern across both languages.
- **Headings.** Chapters open with an `#` H1 title (often prefixed with a topic emoji like `🧪`), then `##` for sections, `###` for numbered sub-steps. Headings are translated; emoji are not.

## New chapter checklist

1. Create the English chapter file at repo root: `<slug>.md`. Start it with the EN language-switcher header.
2. Put any images in `asset/` using the `<slug>-*` naming convention.
3. Add a bullet under `# Chapters` in the root `README.md` linking to `./<slug>.md`.
4. For each existing `<lang>/`, either add a translated copy (`<lang>/<slug>.md` with the appropriate language-switcher header and `../asset/` image paths) and update the chapter index in `<lang>/README.md`, **or** open an issue tagging the translator. Don't leave a stale translation index pointing at a missing file.

## Adding a new language

1. Create `<lang>/` at repo root (e.g. `de/`).
2. Copy each root `.md` file into `<lang>/`, rewriting `asset/` references to `../asset/`.
3. Translate the body content; keep the language switcher header pointing to all sibling languages.
4. Append the new language link to the language-switcher header in **every** existing Markdown file across every language so navigation stays symmetric.

## Workflow

- Changes ship via PRs to `main` (see recent history: each chapter or revision lands as its own PR, e.g. "Uv index", "Add measurement section"). Keep one chapter — or one language's translation pass — per PR where practical.
- The only tooling configured is VS Code's built-in Markdown validation (`.vscode/settings.json`). There are no linters, formatters, or CI checks to run locally.
