# ⚡ Reabot6 — Personal AI Engineering Partner

> *"Your codebase. Your voice. Your rules."*

**Reabot6** is a personal AI assistant built for developers — specifically built for *you*. It runs on your own machine, connects to your codebase, understands your code patterns, speaks to you in your voice, and gets smarter every time you work together.

This is not a chatbot. It's a coding partner that lives in your VSCode, listens for your voice, plans with you, writes with you, refactors with you — and remembers everything.

Forked from [OpenClaw](https://github.com/openclaw/openclaw) (MIT) and built into something personal.

---

## What Reabot6 does

- **Understands your codebase** — indexes your project files and builds context around how you write
- **Speaks and listens** — say "Reabot6" and it wakes up, responds in voice, only to you
- **Writes and refactors code** — edits files, leaves comments, cleans up functions, with your permission
- **Plans with you** — break down features, map out architecture, think through approaches together
- **Remembers everything** — memory layer persists across sessions, it knows your history
- **Gets smarter over time** — every session generates training data, fine-tuning loop runs on your schedule
- **Runs in VSCode** — lives right where you work, not in a separate window

---

## How it thinks

Reabot6 uses a single model with a smart intent router — one load into memory, multiple modes of thinking:

```
You speak or type
       ↓
Intent Router (detects what you need)
       ↓
┌──────────────┬──────────────┬──────────────┬──────────────┐
│  CONVERSATION│   PLANNING   │  CODE SOLVE  │  REFACTORING │
│  Talk it out │ Map features │  Fix + build │ Clean + docs │
└──────────────┴──────────────┴──────────────┴──────────────┘
       ↓
Memory layer (reads + writes your history)
       ↓
Action (edits file / speaks response / plans in VSCode)
```

---

## Stack

| Layer | Tool | Notes |
|---|---|---|
| Base framework | OpenClaw (forked) | Gateway, tools, file access |
| AI brain | Groq free tier → Llama 3.1 70B | Fast, free, swappable |
| Voice input | Whisper (local) | Runs on CPU fine |
| Wake word | Porcupine (custom "Reabot6") | Passive listener, near-zero CPU |
| Speaker ID | Resemblyzer | Only your voice triggers it |
| Voice output | Kokoro TTS | Local, sounds human |
| Memory | ChromaDB + SQLite | Persists across sessions |
| IDE layer | VSCode Extension (custom) | File access, inline suggestions |
| Fine-tuning | LoRA via Unsloth on Colab | Free, improves over time |

---

## Getting started

**Requirements:** Node.js 22+ and Git on Windows/macOS/Linux.

```bash
# Clone your fork
git clone https://github.com/YOUR_USERNAME/reabot6.git
cd reabot6

# Install dependencies
npm install -g pnpm
pnpm install

# First-time setup
pnpm openclaw setup

# Run Reabot6
pnpm gateway:watch
```

On first run, the setup wizard walks you through connecting your model provider (Groq recommended — free and fast), setting up your workspace, and writing your `SOUL.md`.

---

## Personality — SOUL.md

Reabot6's personality lives in `~/.openclaw/workspace/SOUL.md`. This is not a system prompt — it's baked into every interaction. Edit it to define how Reabot6 talks to you, what it prioritises, how direct it is, what it calls you.

---

## Project structure

```
reabot6/
├── src/                  # Core runtime (gateway, agent, tools)
├── extensions/
│   └── vscode/           # VSCode extension — file access + inline UI
├── skills/
│   ├── wake-word/        # Porcupine wake word listener
│   ├── voice-id/         # Speaker verification (your voice only)
│   ├── tts/              # Kokoro text-to-speech output
│   ├── memory/           # ChromaDB + SQLite memory layer
│   └── codebase/         # Project file indexer
├── src/router/           # Intent router — conversation / plan / solve / refactor
└── workspace/
    └── SOUL.md           # Reabot6's personality — rewrite this
```

---

## Build phases

**Phase 1** — Fork, rename, run. Get OpenClaw running as Reabot6 locally.

**Phase 2** — Personality + model. Write `SOUL.md`, connect Groq, make it feel like Reabot6.

**Phase 3** — VSCode + codebase. Build the extension, index your project, give it file access.

**Phase 4** — Voice + wake word. Add Whisper, Porcupine, speaker verification, TTS.

**Phase 5** — Memory + training loop. Persist history, generate training data, run LoRA fine-tuning.

---

## Fine-tuning

Every coding session logs interactions. Every few weeks, run a fine-tuning pass:

```bash
# Collect session data
pnpm reabot6 training:collect

# Push to Colab for LoRA fine-tuning (free GPU)
# Download adapter, merge into base model
# Deploy updated weights — Reabot6 is now smarter
```

Over time, the model has seen your code, your decisions, your preferences. No product on the market gives you this.

---

## Security

- All file access is local — nothing leaves your machine except model inference calls
- Speaker verification means only your voice can trigger Reabot6
- Model calls go to your own Groq key (or your own hosted model when ready)
- Full audit trail of every action Reabot6 takes on your files

---

## Vision

Reabot6 is not a product. It's a relationship. The longer you work together, the better it understands you — your style, your projects, your thinking. That's not something you can buy. You build it.

---

## License

MIT — forked from [OpenClaw](https://github.com/openclaw/openclaw) by Peter Steinberger and contributors.
Built into Reabot6 by you.
