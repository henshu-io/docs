# Henshu User Manual — Documentation Design

**Date:** 2026-03-30
**Status:** Approved
**Author:** Kensuke Koshijima + Claude

---

## 1. Overview

User-facing documentation for Henshu.io, a podcast creation platform with AI-powered audio editing tools. Built with Mintlify, hosted in the `docs` repo.

### Audience

- **Primary:** End users / podcasters using the Henshu web app
- **Secondary:** LLMs reading the docs for support, context, or integration purposes

### Scope (v1)

- Feature-complete but concise — one page per major feature area
- Covers the web app, account lifecycle, and generated output
- Task-based organization (structured around "how do I...?" questions)
- Screenshots deferred — content-first with `[screenshot: description]` placeholders

### Design Principles

- **Task-based structure:** Pages organized by what the user is trying to do, not by feature taxonomy
- **LLM-friendly:** Self-contained pages, structured headings, explicit terminology, clean frontmatter with `keywords` field, synonym/alias handling (see Section 4)
- **Canonical source rule:** Each fact has exactly one canonical page. Other pages use a short callout + link. The canonical page for quotas/limits is "Plans & Quotas." The canonical page for terminology is "Concepts & Terminology."
- **Cross-linked:** Related pages linked rather than content duplicated
- **Troubleshooting coverage:** Every task page includes a "Common Issues" section for failure states and recovery

---

## 2. Navigation Structure

Mintlify `docs.json` tab and group layout:

```
Tab: "User Guide"
│
├── Group: "Getting Started"
│   ├── Welcome to Henshu
│   ├── Concepts & Terminology
│   └── Your First Episode
│
├── Group: "Creating & Organizing"
│   ├── Creating a Show
│   ├── Creating an Episode
│   └── Uploading Audio
│
├── Group: "Editing"
│   ├── Using the Audio Editor
│   ├── Editing with Transcripts
│   ├── AI Audio Enhancement
│   └── Adding Background Music
│
├── Group: "Publishing"
│   ├── Generating Your Episode
│   └── Downloading & Sharing
│
└── Group: "Account"
    ├── Account Setup
    ├── Plans & Quotas
    └── Managing Your Subscription
```

**Rationale:** Groups follow the workflow phases (organize → edit → publish → account). Users with a question navigate to the relevant phase and find the answer.

---

## 3. Page Content Outlines

### Getting Started

#### Welcome to Henshu
- What Henshu is (audio editing + podcast creation platform with AI tools)
- High-level overview of the workflow: upload → edit → enhance → add music → generate
- Links to "Concepts & Terminology" for key terms and "Your First Episode" for hands-on walkthrough

#### Concepts & Terminology
- **Page archetype: concept** — this is the canonical glossary for all Henshu-specific terms
- Key concepts with definitions and stable anchors:
  - Show, Episode, Section, Audio Block, Segment
  - BGM (background music), Ducking, Smart Loop
  - Enhancement, Transcription, Text-based editing
  - Generate / Episode generation
- The hierarchy explained: Show → Episode → Section → Audio Block → Segment → Audio File
- Each term includes "also known as" aliases where applicable (e.g. "BGM" = "background music", "generate" = "export/finalize your episode")

#### Your First Episode
- End-to-end linear walkthrough with cross-links to deeper pages:
  1. Create your show
  2. Create a new episode
  3. Upload your audio files
  4. Arrange sections and audio blocks
  5. (Optional) Transcribe and do text-based edits
  6. (Optional) Enhance audio with AI
  7. (Optional) Add background music
  8. Generate your episode
  9. Download the final file
- Each step: 2-3 sentences + link to the full feature page

### Creating & Organizing

#### Creating a Show
- What a show is (container for episodes, like a podcast series)
- How to create one from the dashboard
- Show settings

#### Creating an Episode
- What an episode is and its internal structure (sections, audio blocks)
- Creating from scratch vs. from template (when templates ship)
- Episode statuses (editing, generated)

#### Uploading Audio
- Supported file formats
- Upload flow (drag & drop, file picker)
- What happens after upload (canonicalization, waveform generation)
- Quota callout: short note + link to Plans & Quotas (canonical source)
- **Common Issues:** upload stuck/failed, unsupported format, quota exceeded

### Editing

#### Using the Audio Editor
- Editor layout overview (activity bar, sidebar, timeline)
- Working with sections (adding, reordering, renaming)
- Working with audio blocks (adding, types: audio vs break)
- Cuts and mutes on the waveform
- Playback and preview
- **Common Issues:** audio not playing, waveform not loading, unexpected silence in preview

#### Editing with Transcripts
- How to trigger transcription
- The transcript panel and how it syncs with the waveform
- Selecting text to create cuts/mutes (Descript-style)
- Quota callout: short note + link to Plans & Quotas (canonical source)
- **Common Issues:** transcription taking too long, inaccurate transcript, quota exceeded, sync issues between transcript and waveform

#### AI Audio Enhancement
- What enhancement does (noise reduction, leveling, etc.)
- How to trigger it (one-click)
- Before/after — what to expect
- Processing time expectations
- **Common Issues:** enhancement taking too long, result sounds worse than expected, enhancement failed

#### Adding Background Music
- The BGM library (global library + show-linked tracks)
- Assigning BGM to a section
- Volume, ducking, fade in/out settings
- Play modes: once, loop, smart loop — explained
- **Common Issues:** BGM too loud/quiet, music not looping as expected, ducking not working

### Publishing

#### Generating Your Episode
- What "Generate" does (assembles sections, applies BGM, produces final file)
- What gets included vs. what doesn't
- Processing time expectations
- **Common Issues:** generation stuck/failed, missing audio in output, BGM not applied

#### Downloading & Sharing
- How to access the generated file
- Download options / format
- What to do next (upload to podcast host, share, etc.)
- **Common Issues:** download link not working, file format questions

### Account

#### Account Setup
- Registration flow
- Email verification
- Password reset

#### Plans & Quotas
- **Page archetype: account/billing** — this is the canonical source for all quota/limit information
- Free plan: what's included, lifetime quotas (5hr upload, 60 min transcription), how quotas work (monotonic — deleting files doesn't reclaim quota)
- Standard plan: what you unlock (unlimited upload, unlimited transcription)
- How to check your remaining quota in the app
- All other pages that mention limits use a short callout + link here

#### Managing Your Subscription
- How to upgrade
- Stripe customer portal (manage payment, view invoices)
- Canceling / what happens when you cancel

---

## 4. Page Conventions

### Self-Contained Context Opener
Every page starts with 1-2 sentences describing what the page covers and where it fits in the Henshu workflow. No assumption that prior pages were read.

### Page Archetypes
Pages use one of three heading structures depending on content type:

**Task pages** (most pages — Creating a Show, Uploading Audio, etc.):
- `# Page Title`
- `## Overview` (brief context + where this fits in the workflow)
- `## How to [do the thing]` (step-by-step instructions)
- `## Key Details` (settings, options, edge cases)
- `## Common Issues` (troubleshooting, failure states, recovery)
- `## Related` (cross-links to other pages)

**Concept pages** (Concepts & Terminology, Welcome):
- `# Page Title`
- `## Overview`
- Concept sections with stable anchors (e.g. `## Shows`, `## Episodes`)
- `## Related`

**Account/billing pages** (Plans & Quotas, Managing Your Subscription, Account Setup):
- `# Page Title`
- `## Overview`
- Content sections relevant to the topic (e.g. `## Free Plan`, `## Standard Plan`, `## How to Upgrade`)
- `## FAQ` (common billing/account questions)
- `## Related`

### Explicit Terminology & Aliases
First mention of a Henshu-specific term (e.g. "audio block", "section", "smart loop") includes a brief inline definition. The "Concepts & Terminology" page is the canonical glossary.

**Synonym handling:** Where users or LLMs might search using different terms, include "also known as" lines and natural-language aliases:
- BGM = background music
- Generate = export, finalize, render
- Enhancement = audio cleanup, noise reduction, mastering
- Transcription = transcript
- Cuts/mutes = edits, trims

**Question-shaped headings:** Where a section answers a specific user question, prefer question form for H2/H3 (e.g. "## How do I add background music to a section?" rather than "## Adding BGM"). This improves LLM retrieval for natural-language queries.

### Screenshot Placeholders
Use `[screenshot: description of what to capture]` where visuals will be added later.

### Cross-Linking
When a page references content covered elsewhere (e.g. "free tier quota"), link to the relevant page rather than re-explaining.

### Frontmatter
Each `.mdx` page uses Mintlify frontmatter with:
- `title` — page title
- `description` — 1-2 sentence summary (used by search engines and LLMs)
- `sidebarTitle` — short label for navigation
- `keywords` — list of synonyms and related terms for LLM/search retrieval

Example:
```yaml
---
title: "Adding Background Music"
description: "How to add background music (BGM) to your podcast sections in Henshu, including volume control, ducking, and smart looping."
sidebarTitle: "Background Music"
keywords: ["BGM", "background music", "music", "ducking", "smart loop", "fade", "volume"]
---
```

---

## 5. File Structure

All content pages and `docs.json` live at the repo root (not in a `docs/` subdirectory). This matches the existing Mintlify repo layout.

```
/ (repo root)
├── docs.json                          # Mintlify config (updated navigation)
│
├── getting-started/
│   ├── welcome.mdx
│   ├── concepts.mdx
│   └── first-episode.mdx
│
├── creating/
│   ├── shows.mdx
│   ├── episodes.mdx
│   └── uploading-audio.mdx
│
├── editing/
│   ├── audio-editor.mdx
│   ├── transcripts.mdx
│   ├── ai-enhancement.mdx
│   └── background-music.mdx
│
├── publishing/
│   ├── generating.mdx
│   └── downloading.mdx
│
└── account/
    ├── setup.mdx
    ├── plans-and-quotas.mdx
    └── subscription.mdx
```

---

## 6. Implementation Notes

- **Mintlify config:** Replace the starter kit `docs.json` navigation with the structure above. Update theme colors to match Henshu brand (violet primary).
- **Existing starter content:** Remove all placeholder pages (essentials/, ai-tools/, api-reference/, etc.)
- **Brand alignment:** Use Henshu brand colors from `docs/HENSHU_BRAND.md` — violet-500 primary, clean/minimal aesthetic
- **Images:** Replace Mintlify starter logos with Henshu logos
- **LLM optimization:** Mintlify's built-in MCP/contextual features (already enabled in docs.json) complement the per-page self-containment strategy
- **AGENTS.md:** Replace the starter kit AGENTS.md with Henshu-specific guidance — terminology rules, content boundaries, writing tone, and canonical source references
