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
- **LLM-friendly:** Self-contained pages, structured headings, explicit terminology, clean frontmatter metadata
- **Contextual plan/quota mentions:** Free tier limits mentioned where users encounter them (e.g. transcription page mentions 60 min limit), no standalone pricing page
- **Cross-linked:** Related pages linked rather than content duplicated

---

## 2. Navigation Structure

Mintlify `docs.json` tab and group layout:

```
Tab: "User Guide"
│
├── Group: "Getting Started"
│   ├── Welcome to Henshu
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
- Key concepts: Show → Episode → Section → Audio Block (the hierarchy, explained simply)
- Overview of the workflow: upload → edit → enhance → add music → generate
- Links to "Your First Episode" for hands-on walkthrough
- Serves as the canonical glossary for Henshu-specific terms

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
- Free tier upload quota context (5hr lifetime limit)

### Editing

#### Using the Audio Editor
- Editor layout overview (activity bar, sidebar, timeline)
- Working with sections (adding, reordering, renaming)
- Working with audio blocks (adding, types: audio vs break)
- Cuts and mutes on the waveform
- Playback and preview

#### Editing with Transcripts
- How to trigger transcription
- The transcript panel and how it syncs with the waveform
- Selecting text to create cuts/mutes (Descript-style)
- Free tier transcription quota context (60 min lifetime limit)

#### AI Audio Enhancement
- What enhancement does (noise reduction, leveling, etc.)
- How to trigger it (one-click)
- Before/after — what to expect
- Processing time expectations

#### Adding Background Music
- The BGM library (global library + show-linked tracks)
- Assigning BGM to a section
- Volume, ducking, fade in/out settings
- Play modes: once, loop, smart loop — explained

### Publishing

#### Generating Your Episode
- What "Generate" does (assembles sections, applies BGM, produces final file)
- What gets included vs. what doesn't
- Processing time expectations

#### Downloading & Sharing
- How to access the generated file
- Download options / format
- What to do next (upload to podcast host, share, etc.)

### Account

#### Account Setup
- Registration flow
- Email verification
- Password reset

#### Plans & Quotas
- Free plan: what's included, lifetime quotas explained
- Standard plan: what you unlock
- How to check remaining quota

#### Managing Your Subscription
- How to upgrade
- Stripe customer portal (manage payment, view invoices)
- Canceling / what happens when you cancel

---

## 4. Page Conventions

### Self-Contained Context Opener
Every page starts with 1-2 sentences describing what the page covers and where it fits in the Henshu workflow. No assumption that prior pages were read.

### Consistent Heading Structure
Each page follows:
- `# Page Title`
- `## Overview` (brief context)
- `## How to [do the thing]` (step-by-step instructions)
- `## Key Details` (settings, options, edge cases)
- `## Related` (cross-links to other pages)

### Explicit Terminology
First mention of a Henshu-specific term (e.g. "audio block", "section", "smart loop") includes a brief inline definition. The "Welcome" page serves as the canonical glossary.

### Screenshot Placeholders
Use `[screenshot: description of what to capture]` where visuals will be added later.

### Cross-Linking
When a page references content covered elsewhere (e.g. "free tier quota"), link to the relevant page rather than re-explaining.

### Frontmatter
Each `.mdx` page uses Mintlify frontmatter with `title`, `description`, and `sidebarTitle` for search engine and LLM metadata.

---

## 5. File Structure

```
docs/
├── docs.json                          # Mintlify config (updated navigation)
│
├── getting-started/
│   ├── welcome.mdx
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
