---
name: grok-skills
description: Top-level entry point for the Grok lyric writing (lw-*) and music composition/arrangement (mc-*) skills library. Use this when starting any lyric or music task, when unsure which skill to load, or when you need the overall architecture of the two libraries.
---

# Grok Skills Library

This repository contains two tightly coupled libraries:

1. **Lyric Writing Library** (`lw-*`) — everything related to writing the words
2. **Music Composition & Arrangement Library** (`mc-*`) — everything related to writing the music and the arrangement

They share a common philosophy: **force explicit decisions before generation**, then audit the result for machine fingerprints.

## Quick Start — Which Workflow to Load First

| You want to… | Load this first |
|--------------|-----------------|
| Write or fix **lyrics** | `lw-workflow` |
| Compose / arrange a **track** (or generate one) | `mc-workflow` |
| Both (song with lyrics + music) | Start with `lw-workflow` or `mc-workflow` depending on which side is driving, then cross over |
| Just check if a lyric sounds AI-written | `lw-ai-tell-audit` |
| Just check if a generated track sounds AI-written | `mc-ai-tell-audit` |

**Always load the corresponding `*-workflow` skill first** for any non-trivial task. It contains the stage table, the routing table, the SPEC gate rules, and the boundary table that prevents two skills from claiming the same decision.

## Library Map

### Lyric Writing (`lw-*`)

| Skill | Responsibility |
|-------|----------------|
| `lw-workflow` | Entry point, router, LYR-SPEC, LYR-LINT |
| `lw-song-intent` | Five questions before writing a single line |
| `lw-structure` | Sections, form, title placement, asymmetry |
| `lw-narrative` | POV, tense, withholding |
| `lw-imagery` | Concrete nouns, image systems, forbidden abstracts |
| `lw-rhyme` | Rhyme stability scale, schemes, surprise |
| `lw-mandarin` | 十三辙, tone, singability |
| `lw-cantonese` | Nine tones, tone-melody agreement |
| `lw-japanese` | Mora, pitch accent, 符割り |
| `lw-korean` | Syllables, 받침, liaison |
| `lw-english` | Stress-to-beat alignment |
| `lw-chinese-style` | 中国风 / 古风 vocabulary & devices |
| `lw-rap` | Rhyme density, multisyllable, punchlines |
| `lw-musical-theatre` | Character diction, Sondheim principles |
| `lw-tone-check` | Mandarin 倒字 detector |
| `lw-ai-tell-audit` | Pre-delivery AI-tell audit (8 symptoms) |
| `lw-case-studies` | Real lyric dissections |
| `lw-suno-interface` | Compile finished lyric for generation backends |

### Music Composition & Arrangement (`mc-*`)

| Skill | Responsibility |
|-------|----------------|
| `mc-workflow` | Entry point, router, ARR-SPEC, stage table S0–S7 |
| `mc-form` | Song form, section design |
| `mc-melody` | Melodic line, range, leaps, phrasing |
| `mc-harmony` | Functional harmony + colour techniques |
| `mc-progressions` | Named progressions lookup |
| `mc-rhythm-groove` | Beat feel, syncopation, groove ingredients |
| `mc-rhythm-section` | Drums, bass, quantization, style patterns |
| `mc-arrangement-arch` | Energy curve, subtractive arranging, layering as form |
| `mc-development` | Motif / theme development operations |
| `mc-texture-layering` | Spectrum budget, depth layers, masking |
| `mc-orchestration` | Instrument choice, blend, register |
| `mc-counterpoint` | Independent second lines |
| `mc-modulation` | Key changes |
| `mc-sound-design` | Synth / timbre intent checklist |
| `mc-vocal-direction` | Delivery vocabulary, harmony types |
| `mc-mix-intent` | Mix goals without prescribing EQ/settings |
| `mc-render-compile` | Compile ARR-SPEC → Suno / YuE2 / MiniMax / etc. |
| `mc-symbolic-score` | ABC / MusicXML / MIDI output |
| `mc-ai-tell-audit` | Post-generation AI-tell audit (14 symptoms) |
| Style layers | `mc-style-jpop`, `mc-style-chinese-pop`, `mc-style-citypop-rnb`, `mc-style-edm`, `mc-style-hiphop`, `mc-style-jazz`, `mc-style-rock-band`, `mc-style-latin`, `mc-style-cinematic` |

### Supporting Skills

- `max-capability` — Force maximum reasoning quality
- `monid` — Discover better external tools / data sources
- `ultimate-productivity` — Productivity systems
- `yue2-music` — YuE2 generation, cover, transcription, editing interface

## Core Design Principles Shared by Both Libraries

1. **Gate before generation** — force explicit choices (LYR-SPEC / ARR-SPEC) so the model is not inventing identity.
2. **Audit after generation** — separate “did it follow the spec?” from “does it still smell like a machine?”
3. **Boundary tables** — every decision belongs to exactly one skill.
4. **Asymmetry and withholding** — perfect symmetry and complete emotional arcs are strong AI fingerprints.
5. **Concrete over abstract** — especially in lyrics; abstract nouns are the most direct AI tell.

## How to Use This Repo

- Clone it and point your agent / skill loader at the directories.
- Or copy individual skill folders into your own skills directory.
- The original live environment keeps the skills under `/home/workdir/.grok/skills/`.

When in doubt, open `lw-workflow/SKILL.md` or `mc-workflow/SKILL.md` and follow the routing table.
