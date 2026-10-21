# Grok Skills Library

This repository contains a copy of the **Grok lyric writing (lw-*)** and **music composition / arrangement (mc-*)** skills.

These skills form a comprehensive system for writing lyrics and composing/arranging music, with strong support for Mandarin, Cantonese, Japanese, Korean, English, and various musical styles.

## Structure

Each skill lives in its own directory and typically contains:

- `SKILL.md` — the main skill definition and instructions
- `reference.md` (and variants) — supporting reference material
- Example YAML files, schemas, etc. where relevant

## Lyric Writing Skills (`lw-*`)

| Skill | Purpose |
|-------|---------|
| `lw-workflow` | Entry point & router for lyric writing |
| `lw-song-intent` | Gate questions before writing |
| `lw-structure` | Section structure, form, hooks |
| `lw-narrative` | Point of view, tense, withholding |
| `lw-imagery` | Concrete nouns & image systems |
| `lw-rhyme` | Rhyme types, schemes, stability |
| `lw-mandarin` | Mandarin tone, 十三辙, prosody |
| `lw-cantonese` | Cantonese tone-melody agreement |
| `lw-japanese` | Mora counting, pitch accent |
| `lw-korean` | Syllables, batchim, liaison |
| `lw-english` | Stress & prosody for English |
| `lw-chinese-style` | 中国风 / 古风 techniques |
| `lw-rap` | Rap rhyme density & techniques |
| `lw-musical-theatre` | Character-driven theatre lyrics |
| `lw-tone-check` | Mandarin dao-zi (倒字) detector |
| `lw-ai-tell-audit` | Pre-delivery AI-tell audit for lyrics |
| `lw-case-studies` | Case studies & dissections |
| `lw-suno-interface` | Compiling lyrics for generation backends |

## Music Composition & Arrangement Skills (`mc-*`)

| Skill | Purpose |
|-------|---------|
| `mc-workflow` | Entry point & router for composition/arrangement |
| `mc-form` | Song form & section design |
| `mc-melody` | Melody writing |
| `mc-harmony` | Functional & colour harmony |
| `mc-progressions` | Named progressions lookup |
| `mc-rhythm-groove` | Rhythm & groove |
| `mc-rhythm-section` | Drums, bass, programming |
| `mc-arrangement-arch` | Energy curve, layering as form |
| `mc-development` | Thematic development |
| `mc-texture-layering` | Spectrum budget & depth |
| `mc-orchestration` | Instrumentation decisions |
| `mc-counterpoint` | Independent lines |
| `mc-modulation` | Key changes |
| `mc-sound-design` | Synth / timbre intent |
| `mc-vocal-direction` | Vocal delivery & harmony |
| `mc-mix-intent` | Mix goals handoff |
| `mc-render-compile` | Compile ARR-SPEC to backends |
| `mc-symbolic-score` | ABC / MusicXML / MIDI output |
| `mc-ai-tell-audit` | Post-generation AI-tell audit |
| Style layers | `mc-style-jpop`, `mc-style-chinese-pop`, `mc-style-citypop-rnb`, `mc-style-edm`, `mc-style-hiphop`, `mc-style-jazz`, `mc-style-rock-band`, `mc-style-latin`, `mc-style-cinematic` |

## Other Skills

- `max-capability` — Maximum reasoning quality mode
- `monid` — Discovery of better tools / data sources
- `ultimate-productivity` — Productivity frameworks
- `yue2-music` — YuE2 music generation / cover / edit interface

## Notes

- These are the **user custom skills** from the Grok environment.
- The original system bundled skills (docx, pdf, xlsx, ffmpeg, etc.) are not included here.
- Full file contents (including all reference.md and example files) can be added on request.

Created automatically from the live skill library.
