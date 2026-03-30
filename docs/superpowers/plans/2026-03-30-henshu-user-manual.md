# Henshu User Manual Implementation Plan

> **For agentic workers:** Execute this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking. Each task should be committed independently. Verify with `mint dev` between tasks.

**Goal:** Build the complete Henshu.io user manual — 15 MDX pages covering onboarding, audio editing, publishing, and account management.

**Architecture:** Mintlify documentation site with task-based page organization. Pages are self-contained MDX files with YAML frontmatter, organized into 5 navigation groups. Cross-links connect related pages. The `docs.json` config defines navigation, branding, and theme.

**Tech Stack:** Mintlify, MDX, docs.json configuration

**Spec:** `docs/superpowers/specs/2026-03-30-henshu-user-manual-design.md`

**Reference material (in the henshu_io repo at `~/Documents/Codes/henshu_io/`):**
- `CLAUDE.md` — product overview, architecture, data model
- `.claude/rules/billing.md` — subscription/quota details
- `.claude/rules/audio-engine.md` — audio editing/playback details
- `.claude/rules/transcription.md` — transcription/text-based editing details
- `.claude/rules/bgm.md` — background music system details
- `docs/HENSHU_BRAND.md` — brand colors and design system

---

## File Structure

All files at repo root (not in a `docs/` subdirectory).

**Modify:**
- `docs.json` — Replace starter navigation with Henshu structure, update branding
- `AGENTS.md` — Replace starter template with Henshu-specific content guidance

**Delete (starter kit content):**
- `index.mdx`, `quickstart.mdx`, `development.mdx`
- `essentials/` (entire directory)
- `ai-tools/` (entire directory)
- `api-reference/` (entire directory)
- `snippets/snippet-intro.mdx`
- `images/checks-passed.png`, `images/hero-dark.png`, `images/hero-light.png`

**Create:**
- `getting-started/welcome.mdx`
- `getting-started/concepts.mdx`
- `getting-started/first-episode.mdx`
- `creating/shows.mdx`
- `creating/episodes.mdx`
- `creating/uploading-audio.mdx`
- `editing/audio-editor.mdx`
- `editing/transcripts.mdx`
- `editing/ai-enhancement.mdx`
- `editing/background-music.mdx`
- `publishing/generating.mdx`
- `publishing/downloading.mdx`
- `account/setup.mdx`
- `account/plans-and-quotas.mdx`
- `account/subscription.mdx`

---

## Task 1: Clean Up Starter Content and Update Config

**Files:**
- Modify: `docs.json`
- Modify: `AGENTS.md`
- Delete: `index.mdx`, `quickstart.mdx`, `development.mdx`
- Delete: `essentials/` directory
- Delete: `ai-tools/` directory
- Delete: `api-reference/` directory
- Delete: `snippets/snippet-intro.mdx`
- Delete: `images/checks-passed.png`, `images/hero-dark.png`, `images/hero-light.png`

- [ ] **Step 0: Verify clean working tree**

```bash
git status
```

Expected: no uncommitted changes to tracked files. If there are uncommitted changes, stash or commit them before proceeding. Untracked files (like `.claude/`, `.agents/`) are fine.

- [ ] **Step 1: Delete all starter content files**

```bash
rm index.mdx quickstart.mdx development.mdx
rm -rf essentials/ ai-tools/ api-reference/
rm snippets/snippet-intro.mdx
rm images/checks-passed.png images/hero-dark.png images/hero-light.png
```

- [ ] **Step 2: Replace docs.json with Henshu config**

Overwrite `docs.json` with:

```json
{
  "$schema": "https://mintlify.com/docs.json",
  "theme": "mint",
  "name": "Henshu",
  "colors": {
    "primary": "#8B5CF6",
    "light": "#A78BFA",
    "dark": "#7C3AED"
  },
  "favicon": "/favicon.svg",
  "navigation": {
    "tabs": [
      {
        "tab": "User Guide",
        "groups": [
          {
            "group": "Getting Started",
            "pages": [
              "getting-started/welcome",
              "getting-started/concepts",
              "getting-started/first-episode"
            ]
          },
          {
            "group": "Creating & Organizing",
            "pages": [
              "creating/shows",
              "creating/episodes",
              "creating/uploading-audio"
            ]
          },
          {
            "group": "Editing",
            "pages": [
              "editing/audio-editor",
              "editing/transcripts",
              "editing/ai-enhancement",
              "editing/background-music"
            ]
          },
          {
            "group": "Publishing",
            "pages": [
              "publishing/generating",
              "publishing/downloading"
            ]
          },
          {
            "group": "Account",
            "pages": [
              "account/setup",
              "account/plans-and-quotas",
              "account/subscription"
            ]
          }
        ]
      }
    ],
    "global": {
      "anchors": [
        {
          "anchor": "Henshu App",
          "href": "https://app.henshu.io",
          "icon": "microphone"
        },
        {
          "anchor": "Website",
          "href": "https://henshu.io",
          "icon": "globe"
        }
      ]
    }
  },
  "logo": {
    "light": "/logo/light.svg",
    "dark": "/logo/dark.svg"
  },
  "navbar": {
    "links": [
      {
        "label": "Support",
        "href": "mailto:support@henshu.io"
      }
    ],
    "primary": {
      "type": "button",
      "label": "Open Henshu",
      "href": "https://app.henshu.io"
    }
  },
  "contextual": {
    "options": [
      "copy",
      "view",
      "chatgpt",
      "claude",
      "perplexity",
      "mcp",
      "cursor",
      "vscode"
    ]
  },
  "footer": {
    "socials": {
      "x": "https://x.com/henshu_io"
    }
  }
}
```

**Notes on values:**
- Colors are Tailwind violet-500 (`#8B5CF6`), violet-400 (`#A78BFA`), violet-600 (`#7C3AED`) — matching the Henshu brand
- Social links and support email — verify these are correct with the user; use placeholders for now
- The `contextual` options are kept from the starter kit — they enable Mintlify's built-in LLM context features

- [ ] **Step 2b: Replace logo files**

Copy Henshu logos from the marketing site or brand assets into `logo/light.svg` and `logo/dark.svg`, replacing the Mintlify starter logos. Also replace `favicon.svg` with the Henshu favicon.

If Henshu logo SVGs are not available locally, ask the user where to find them. Do not proceed with Mintlify placeholder logos in the final site.

- [ ] **Step 3: Replace AGENTS.md with Henshu-specific guidance**

Overwrite `AGENTS.md` with:

```markdown
# Henshu Documentation Project

## About

User-facing documentation for [Henshu.io](https://henshu.io), a podcast creation platform with AI-powered audio editing tools. Built on [Mintlify](https://mintlify.com).

## Commands

- `mint dev` — preview locally at localhost:3000
- `mint validate` — validate docs.json config and page structure
- `mint broken-links` — check for broken links

## Terminology

Use these terms consistently across all pages:

| Preferred term | Definition | Aliases (include for LLM retrieval) | Never use |
|---------------|-----------|--------------------------------------|-----------|
| Show | A podcast series container | — | "project", "workspace" |
| Episode | A single podcast episode within a show | — | "recording", "session" |
| Section | A structural division of an episode (e.g., intro, interview, outro) | — | "chapter", "part" |
| Audio block | A container for audio within a section. Types: AUDIO or BREAK | — | "clip", "track" |
| Segment | A reference to a portion of an audio file within a block | — | "slice", "region" |
| BGM | Background music assigned to a section. Spell out "background music" on first use, then "BGM" | background music | — |
| Enhancement | AI-powered audio cleanup (noise reduction, leveling) | audio cleanup, noise reduction, mastering | — |
| Transcription | AI-generated text transcript of an audio file | transcript | "caption", "subtitle" |
| Text-based editing | Creating cuts/mutes by selecting text in a transcript | — | "transcript editing" |
| Generate | Assemble an episode into a final audio file | export, finalize, render | "compile" |
| Smart loop | BGM play mode that crossfades at configured cue points | — | "seamless loop" |
| Ducking | Automatically lowering BGM volume when voice is detected | — | "sidechain" |

**How to use aliases:** Use the preferred term in running text. Include aliases in page `keywords` frontmatter and in "also known as" lines on the Concepts page, so LLMs and search can find pages using either term.

## Style Rules

- Use active voice and second person ("you")
- One idea per sentence
- Sentence case for headings
- Bold for UI elements: Click **Settings**
- Code formatting for file names and paths
- Include `[screenshot: description]` placeholders where visuals would help
- Question-shaped headings where users would search that way (e.g., "## How do I add background music?")

## Page Archetypes

- **Task pages:** Overview → How to → Key Details → Common Issues → Related
- **Concept pages:** Overview → Term sections with stable anchors → Related
- **Account/billing pages:** Overview → Content sections → FAQ → Related

## Canonical Sources

- **Quotas and plan limits:** `account/plans-and-quotas.mdx` is the single source. Other pages use a short callout + link.
- **Terminology definitions:** `getting-started/concepts.mdx` is the canonical glossary. Other pages define terms inline on first use and link to concepts page.

## Content Boundaries

- Document only user-facing features in the Henshu web app
- Do NOT document: internal admin features, backend API details, infrastructure
- Do NOT include actual pricing amounts — link to the marketing site for current pricing
- Do NOT assume the user has read any other page — each page must be self-contained
```

- [ ] **Step 4: Create directory structure**

```bash
mkdir -p getting-started creating editing publishing account
```

- [ ] **Step 5: Commit**

```bash
git add docs.json AGENTS.md getting-started/ creating/ editing/ publishing/ account/
git add index.mdx quickstart.mdx development.mdx essentials/ ai-tools/ api-reference/ snippets/snippet-intro.mdx images/checks-passed.png images/hero-dark.png images/hero-light.png
git commit -m "chore: remove starter content and configure Henshu docs

Replace Mintlify starter kit with Henshu brand config, navigation
structure, and content guidelines. All placeholder content removed."
```

Note: The second `git add` stages the deletions. Verify with `git status` before committing that only expected files are staged.

---

## Task 2: Getting Started Pages

**Files:**
- Create: `getting-started/welcome.mdx`
- Create: `getting-started/concepts.mdx`
- Create: `getting-started/first-episode.mdx`

- [ ] **Step 1: Create getting-started/welcome.mdx**

```mdx
---
title: "Welcome to Henshu"
description: "Henshu is a podcast creation platform with AI-powered audio editing tools. Learn what Henshu does and how to get started."
sidebarTitle: "Welcome"
keywords: ["henshu", "podcast", "audio editing", "getting started", "overview"]
---

# Welcome to Henshu

## Overview

Henshu is a podcast creation platform that helps you edit audio, enhance it with AI, add background music, and generate polished podcast episodes — all in your browser. This page introduces what Henshu does and how the workflow fits together.

## What can you do with Henshu?

Henshu gives you everything you need to go from raw audio recordings to a finished podcast episode:

- **Edit audio visually** — Cut, mute, and rearrange audio using a waveform editor
- **Edit by reading text** — Transcribe your audio and make edits by selecting text, similar to editing a document
- **Enhance with AI** — Clean up audio with one-click AI enhancement (noise reduction, volume leveling)
- **Add background music** — Choose from a music library with smart looping, volume ducking, and fade controls
- **Generate your episode** — Assemble everything into a single, polished audio file ready to publish

## How Henshu works

The typical workflow in Henshu follows these steps:

1. **Create a show** — A show is your podcast series (e.g., "My Weekly Podcast")
2. **Create an episode** — Each episode lives inside a show
3. **Upload your audio** — Drag and drop your recordings into the episode
4. **Edit** — Use the waveform editor or transcript to cut, mute, and arrange your audio
5. **Enhance and add music** — Optionally improve audio quality and add background music
6. **Generate** — Henshu assembles your episode into a final audio file
7. **Download and share** — Get your finished file and publish it wherever you host your podcast

## Next steps

<CardGroup cols={2}>
  <Card title="Key concepts" icon="book" href="/getting-started/concepts">
    Learn the terminology used throughout Henshu — shows, episodes, sections, audio blocks, and more.
  </Card>
  <Card title="Create your first episode" icon="rocket" href="/getting-started/first-episode">
    Follow a step-by-step walkthrough from creating a show to downloading your finished episode.
  </Card>
</CardGroup>

## Related

- [Concepts & Terminology](/getting-started/concepts) — definitions of all Henshu-specific terms
- [Your First Episode](/getting-started/first-episode) — step-by-step walkthrough
- [Plans & Quotas](/account/plans-and-quotas) — understand your plan's limits
```

- [ ] **Step 2: Create getting-started/concepts.mdx**

```mdx
---
title: "Concepts & Terminology"
description: "Key concepts and terminology used in Henshu — shows, episodes, sections, audio blocks, segments, BGM, enhancement, transcription, and more."
sidebarTitle: "Concepts"
keywords: ["concepts", "terminology", "glossary", "show", "episode", "section", "audio block", "segment", "BGM", "background music", "enhancement", "transcription", "generate", "export"]
---

# Concepts & Terminology

This page defines the key concepts and terms used throughout Henshu. If you encounter an unfamiliar term anywhere in the docs, you'll find its definition here.

## The Episode Hierarchy

Henshu organizes your podcast content in a hierarchy. Understanding this structure helps you work effectively in the editor.

```
Show → Episode → Section → Audio Block → Segment → Audio File
```

### Shows

A **show** is your podcast series — the top-level container for all your episodes. Think of it as "My Interview Podcast" or "Weekly Tech News." You create shows from the dashboard, and each show has its own settings and background music library.

### Episodes

An **episode** is a single installment of your show. Each episode contains one or more sections that you arrange and edit to create your final podcast file. Episodes have a status: **editing** (in progress) or **generated** (final file created).

### Sections

A **section** is a structural division within an episode — for example, "Intro," "Interview," or "Outro." Sections let you organize your episode into logical parts. Each section can have its own [background music (BGM)](/editing/background-music) assignment with independent volume, ducking, and fade settings.

### Audio Blocks

An **audio block** is a container within a section that holds audio content. There are two types:

- **Audio blocks** — contain your voice recordings or other audio files
- **Break blocks** — represent silence or pauses with a set duration

Audio blocks within a section play **sequentially** — one after another in the timeline.

### Segments

A **segment** is a reference to a specific portion of an audio file within an audio block. Segments define which part of the original recording to play, including any [cuts or mutes](#cuts-and-mutes) you've made. Multiple segments within the same audio block play **in parallel** (layered together).

### Audio Files

An **audio file** is your original uploaded recording. When you upload a file to Henshu, it gets processed into a standard format and a waveform is generated for visual editing. One audio file can be referenced by multiple segments across different episodes.

## Editing Concepts

### Cuts and Mutes

Also known as: edits, trims

- A **cut** removes a portion of audio from playback — the audio before and after the cut plays seamlessly
- A **mute** silences a portion of audio — the duration is preserved but the sound is replaced with silence

You can create cuts and mutes either by selecting regions on the [waveform editor](/editing/audio-editor) or by selecting text in the [transcript](/editing/transcripts).

### Transcription

Also known as: transcript

**Transcription** is the process of converting your audio file into text using AI. Once transcribed, you can read your recording as text and make edits by selecting words — this is called [text-based editing](/editing/transcripts). Henshu uses AI-powered transcription with word-level timestamps so that text selections map precisely to audio regions.

### Enhancement

Also known as: audio cleanup, noise reduction

**Enhancement** is Henshu's one-click [AI audio processing](/editing/ai-enhancement) that improves your recording quality. It includes noise reduction and volume leveling. Enhanced audio files are marked with a gold badge in the editor.

## Music Concepts

### BGM (Background Music)

**BGM** stands for background music. Henshu provides a [music library](/editing/background-music) that you can browse and assign to individual sections of your episode. Each section can have its own BGM track with independent settings.

### Ducking

**Ducking** automatically lowers the background music volume when voice audio is playing, then brings it back up during pauses. This ensures your voice is always clearly audible over the music.

### Smart Loop

A **smart loop** is a BGM play mode that uses configured cue points to create seamless music loops with crossfade transitions. Unlike a basic loop (which restarts from the beginning), a smart loop crossfades at natural transition points in the music for a more polished sound.

BGM play modes:
- **Once** — play the track once and stop
- **Loop** — repeat from the beginning when the track ends
- **Smart loop** — crossfade loop using configured cue points

## Publishing Concepts

### Generate (Episode Generation)

Also known as: export, finalize, render

**Generating** an episode is the process of assembling all your sections, audio blocks, BGM, and edits into a single final audio file. This is the last step before you download and publish your podcast. See [Generating Your Episode](/publishing/generating) for details.

## Related

- [Your First Episode](/getting-started/first-episode) — walkthrough of the full workflow
- [Plans & Quotas](/account/plans-and-quotas) — upload and transcription limits
```

- [ ] **Step 3: Create getting-started/first-episode.mdx**

```mdx
---
title: "Your First Episode"
description: "Step-by-step walkthrough to create your first podcast episode in Henshu — from creating a show to downloading the finished file."
sidebarTitle: "First Episode"
keywords: ["first episode", "tutorial", "walkthrough", "getting started", "onboarding", "how to", "create podcast"]
---

# Your First Episode

This guide walks you through creating a podcast episode from start to finish. By the end, you'll have a polished audio file ready to publish.

## Overview

You'll go through these steps:

1. Create a show
2. Create an episode
3. Upload your audio
4. Arrange your content
5. (Optional) Transcribe and edit with text
6. (Optional) Enhance your audio with AI
7. (Optional) Add background music
8. Generate your episode
9. Download the final file

## Step 1: Create a show

A show is your podcast series — the container for all your episodes.

1. From the **Dashboard**, click **Create Show**
2. Enter a name for your show (e.g., "My Podcast")
3. Your new show appears on the dashboard

[screenshot: Dashboard with Create Show button highlighted]

For more details, see [Creating a Show](/creating/shows).

## Step 2: Create an episode

1. Click on your show to open it
2. Click **Create Episode**
3. Enter a title for your episode
4. You'll be taken to the episode editor

[screenshot: New episode dialog]

For more details, see [Creating an Episode](/creating/episodes).

## Step 3: Upload your audio

1. In the editor, click **Upload** or drag and drop your audio files into the episode
2. Henshu processes your files — you'll see a waveform appear once processing is complete
3. Your files are placed into audio blocks within the first section

[screenshot: Drag and drop upload area in the editor]

For more details, see [Uploading Audio](/creating/uploading-audio).

## Step 4: Arrange your content

Use sections and audio blocks to structure your episode:

- **Add sections** to divide your episode into parts (e.g., Intro, Main Content, Outro)
- **Drag audio blocks** between sections to reorganize
- **Add break blocks** to insert pauses between audio
- **Cut or mute** unwanted parts by selecting regions on the waveform

[screenshot: Editor with multiple sections and audio blocks]

For more details, see [Using the Audio Editor](/editing/audio-editor).

## Step 5: Transcribe and edit with text (optional)

If you want to edit by reading your audio as text:

1. Select an audio file and click **Transcribe**
2. Wait for the AI transcription to complete
3. Read the transcript and select any words you want to cut or mute
4. The waveform updates automatically to reflect your text selections

[screenshot: Transcript panel with text selected for cutting]

For more details, see [Editing with Transcripts](/editing/transcripts).

## Step 6: Enhance your audio with AI (optional)

To improve your audio quality with AI:

1. Select an audio file in the editor
2. Click **Enhance**
3. Wait for processing to complete — the file will show a gold badge when enhanced

Enhancement applies noise reduction and volume leveling to your recording.

[screenshot: Audio file with enhance button and gold badge]

For more details, see [AI Audio Enhancement](/editing/ai-enhancement).

## Step 7: Add background music (optional)

To add music to a section:

1. Select a section in the editor
2. Open the BGM panel and browse the music library
3. Click a track to assign it to the section
4. Adjust volume, ducking, and fade settings as needed

[screenshot: BGM panel with track assigned to a section]

For more details, see [Adding Background Music](/editing/background-music).

## Step 8: Generate your episode

When you're happy with your edits:

1. Click **Generate Episode**
2. Henshu assembles all your sections, audio blocks, edits, and background music into a single file
3. Wait for processing to complete

[screenshot: Generate Episode button]

For more details, see [Generating Your Episode](/publishing/generating).

## Step 9: Download the final file

Once generation is complete:

1. Click **Download** to get your finished audio file
2. Upload it to your podcast hosting platform, or share it directly

[screenshot: Download button on generated episode]

For more details, see [Downloading & Sharing](/publishing/downloading).

## Key Details

- Steps 5–7 (transcription, enhancement, BGM) are optional — you can generate an episode with just raw uploaded audio
- You can return to any step and make changes after generating — then re-generate to get an updated file
- Each step links to a detailed feature page for deeper guidance

## Common Issues

**I'm not sure what order to do things in**
Follow the steps on this page in order. The only truly required steps are: create a show, create an episode, upload audio, and generate. Everything else is optional enhancement.

**My episode sounds different from what I expected**
Preview your episode in the editor before generating. The preview plays your episode as it will sound in the final file, including cuts, mutes, and background music.

## Related

- [Using the Audio Editor](/editing/audio-editor) — master the waveform editor
- [Editing with Transcripts](/editing/transcripts) — text-based editing workflow
- [Adding Background Music](/editing/background-music) — music library and settings
- [Plans & Quotas](/account/plans-and-quotas) — understand your plan's limits
```

- [ ] **Step 4: Verify pages render**

```bash
mint dev
```

Open http://localhost:3000 and verify:
- Welcome page loads as the landing page
- Concepts page renders with all term anchors
- First Episode walkthrough renders with all cross-links
- Navigation sidebar shows "Getting Started" group with all three pages

- [ ] **Step 5: Commit**

```bash
git add getting-started/
git commit -m "docs: add Getting Started pages

Add Welcome, Concepts & Terminology, and Your First Episode pages.
Concepts page serves as the canonical glossary with stable anchors."
```

---

## Task 3: Creating & Organizing Pages

**Files:**
- Create: `creating/shows.mdx`
- Create: `creating/episodes.mdx`
- Create: `creating/uploading-audio.mdx`

- [ ] **Step 1: Create creating/shows.mdx**

```mdx
---
title: "Creating a Show"
description: "How to create and configure a show (podcast series) in Henshu. A show is the top-level container for your episodes."
sidebarTitle: "Shows"
keywords: ["show", "podcast", "series", "create show", "dashboard", "settings"]
---

# Creating a Show

A [show](/getting-started/concepts#shows) is your podcast series in Henshu — the top-level container that holds all your episodes. Before you can create episodes, you need at least one show.

## Overview

Shows live on your **Dashboard**. Each show has its own episodes, settings, and background music library. Most podcasters have one show, but you can create multiple shows if you produce more than one podcast.

## How do I create a show?

1. Go to your **Dashboard**
2. Click **Create Show**
3. Enter a name for your show (e.g., "My Interview Podcast")
4. Your new show appears on the dashboard

[screenshot: Dashboard with Create Show button and show card]

## How do I open a show?

Click on a show card in the dashboard to open it. You'll see all episodes belonging to that show and can create new ones.

## Key Details

- Each show has its own [BGM library](/editing/background-music) — music tracks you link to a show are available across all its episodes
- Episodes belong to exactly one show and cannot be moved between shows
- Show names can be changed after creation

## Common Issues

**I want to rename my show**
Click on the show name in the dashboard or show settings to edit it.

**I accidentally created the wrong show**
You can delete a show if it has no episodes, or rename it to match your needs.

## Related

- [Creating an Episode](/creating/episodes) — create episodes within your show
- [Adding Background Music](/editing/background-music) — manage your show's music library
- [Concepts & Terminology](/getting-started/concepts#shows) — definition of "show"
```

- [ ] **Step 2: Create creating/episodes.mdx**

```mdx
---
title: "Creating an Episode"
description: "How to create a new podcast episode in Henshu, understand its structure (sections and audio blocks), and manage episode status."
sidebarTitle: "Episodes"
keywords: ["episode", "create episode", "sections", "audio blocks", "structure", "new episode", "template"]
---

# Creating an Episode

An [episode](/getting-started/concepts#episodes) is a single installment of your podcast. Each episode is organized into [sections](/getting-started/concepts#sections) and [audio blocks](/getting-started/concepts#audio-blocks) that you arrange in the editor.

## Overview

Episodes live inside a [show](/creating/shows). When you create a new episode, it starts with a single empty section. You then upload audio, add more sections, and structure your episode before generating the final file.

## How do I create an episode?

1. Open your show from the **Dashboard**
2. Click **Create Episode**
3. Enter a title for your episode
4. Click **Create** — you'll be taken to the episode editor

[screenshot: Create Episode dialog with title field]

The new episode starts with one empty section called "Section 1." From here, you can [upload audio](/creating/uploading-audio) and start editing.

## How is an episode structured?

An episode is organized as a hierarchy:

```
Episode
├── Section 1 (e.g., "Intro")
│   ├── Audio Block (your intro recording)
│   └── Break Block (2 seconds of silence)
├── Section 2 (e.g., "Interview")
│   └── Audio Block (interview recording)
└── Section 3 (e.g., "Outro")
    └── Audio Block (outro recording)
```

- **Sections** are the top-level divisions (intro, main content, outro, etc.)
- **Audio blocks** contain your recordings — they play sequentially within a section
- **Break blocks** insert silence for a specified duration
- Each section can have its own [background music](/editing/background-music)

## What are episode statuses?

| Status | Meaning |
|--------|---------|
| **Editing** | The episode is in progress — you can upload, edit, and rearrange content |
| **Generated** | A final audio file has been created — you can download and share it |

You can continue editing an episode after generating it, and generate again with your changes.

## Common Issues

**I can't find my episode**
Make sure you're looking inside the correct show. Episodes belong to a specific show and only appear when that show is open.

**I want to start over with a blank episode**
You can delete all sections and audio blocks within an episode, or create a new episode entirely.

## Related

- [Creating a Show](/creating/shows) — shows are the container for episodes
- [Uploading Audio](/creating/uploading-audio) — add audio files to your episode
- [Using the Audio Editor](/editing/audio-editor) — edit your episode's content
- [Concepts & Terminology](/getting-started/concepts#episodes) — definition of "episode"
```

- [ ] **Step 3: Create creating/uploading-audio.mdx**

```mdx
---
title: "Uploading Audio"
description: "How to upload audio files to your Henshu episode — supported formats, the upload process, and what happens after upload."
sidebarTitle: "Uploading Audio"
keywords: ["upload", "audio", "recording", "file", "drag and drop", "format", "wav", "mp3", "processing", "waveform", "quota"]
---

# Uploading Audio

Upload your audio recordings to an episode to start editing. Henshu processes uploaded files automatically — converting them to a standard format and generating a waveform for visual editing.

## Overview

You upload audio files from within the episode editor. Files can be added via drag-and-drop or a file picker. After upload, Henshu processes each file in the background: it converts the audio to a standard format (for consistent editing) and generates a waveform visualization.

## How do I upload audio?

1. Open an episode in the editor
2. Either **drag and drop** audio files into the editor, or click the **Upload** button and select files from your computer
3. Your files begin uploading — you'll see a progress indicator
4. Once uploaded, Henshu processes each file (this takes a few seconds)
5. A waveform appears when processing is complete, and the file is ready to edit

[screenshot: Upload area in the editor with drag-and-drop zone]

You can upload multiple files at once. Large files are automatically handled with multipart upload.

## What happens after upload?

When you upload a file, Henshu:

1. **Uploads** the file to cloud storage
2. **Converts** it to a standard audio format (48kHz, mono) for consistent editing
3. **Generates a waveform** so you can see the audio visually in the editor
4. **Creates an audio block** containing your file in the current section

You can start editing as soon as the waveform appears.

## Supported formats

Henshu accepts common audio formats including WAV, MP3, M4A, AAC, FLAC, and OGG. Files are converted to a standard format during processing, so the original format doesn't affect editing quality.

## Key Details

- Uploaded files are placed into the currently selected section as new audio blocks
- You can upload while other files are still processing
- Original files are preserved — processing creates a working copy

<Note>
  **Free plan limit:** Your account has a lifetime upload quota. To check your remaining quota or learn about plan limits, see [Plans & Quotas](/account/plans-and-quotas).
</Note>

## Common Issues

**Upload seems stuck or isn't progressing**
Check your internet connection. Very large files take longer to upload. If the upload fails, try again — Henshu will resume from where it left off for large files.

**"Quota exceeded" error**
You've reached your plan's upload limit. See [Plans & Quotas](/account/plans-and-quotas) for details on your plan's limits and how to upgrade.

**My file format isn't accepted**
Make sure your file is a supported audio format (WAV, MP3, M4A, AAC, FLAC, OGG). Video files and non-audio formats are not supported.

**Waveform isn't appearing after upload**
Processing can take a few seconds depending on file size. If the waveform doesn't appear after a minute, try refreshing the page. Your file is safely stored and processing will continue.

## Related

- [Using the Audio Editor](/editing/audio-editor) — edit your uploaded audio
- [Creating an Episode](/creating/episodes) — set up an episode before uploading
- [Plans & Quotas](/account/plans-and-quotas) — upload limits for your plan
```

- [ ] **Step 4: Verify pages render**

```bash
mint dev
```

Open http://localhost:3000 and verify the "Creating & Organizing" group renders with all three pages and cross-links work.

- [ ] **Step 5: Commit**

```bash
git add creating/
git commit -m "docs: add Creating & Organizing pages

Add Shows, Episodes, and Uploading Audio pages covering
show/episode creation and the upload workflow."
```

---

## Task 4: Editing Pages

**Files:**
- Create: `editing/audio-editor.mdx`
- Create: `editing/transcripts.mdx`
- Create: `editing/ai-enhancement.mdx`
- Create: `editing/background-music.mdx`

- [ ] **Step 1: Create editing/audio-editor.mdx**

```mdx
---
title: "Using the Audio Editor"
description: "How to use Henshu's audio editor — navigate the editor layout, work with sections and audio blocks, make cuts and mutes, and preview your episode."
sidebarTitle: "Audio Editor"
keywords: ["editor", "waveform", "audio editor", "cut", "mute", "section", "audio block", "break", "timeline", "preview", "playback", "trim", "edit"]
---

# Using the Audio Editor

The audio editor is where you arrange, cut, and preview your podcast episode. It provides a waveform-based interface for visual editing, with sections and audio blocks organized in a timeline.

## Overview

When you open an episode, you enter the editor. The editor shows your episode's structure — [sections](/getting-started/concepts#sections) containing [audio blocks](/getting-started/concepts#audio-blocks) — with waveform visualizations for each audio file. You can rearrange content, make cuts and mutes, and preview your episode before generating the final file.

## Editor Layout

The editor consists of several areas:

- **Activity Bar** — the left-hand sidebar with navigation icons
- **Sidebar** — shows episode details and section list
- **Main Area** — the waveform timeline where you edit audio
- **Playback Controls** — play, pause, and seek through your episode

[screenshot: Full editor layout with areas labeled]

## How do I work with sections?

Sections divide your episode into logical parts (intro, main content, outro, etc.).

**Adding a section:**
1. Click **Add Section** below the existing sections
2. The new section appears at the end of the episode
3. Click the section title to rename it

**Reordering sections:**
Drag sections to rearrange the order they play in your episode.

**Renaming a section:**
Click on the section title to edit it inline.

[screenshot: Section list with Add Section button]

## How do I work with audio blocks?

Audio blocks hold your audio content within a section.

**Adding an audio block:**
- Upload a new file (see [Uploading Audio](/creating/uploading-audio))
- Or click **Add Audio Block** within a section

**Adding a break block:**
Click **Add Break** to insert a silence block. Set the duration for how long the pause should be.

**Reordering blocks:**
Drag audio blocks to rearrange them within a section. Blocks play sequentially in order.

[screenshot: Section with audio blocks and a break block]

## How do I cut or mute audio?

Select a region on the waveform to apply edits:

**Making a cut:**
1. Click and drag on the waveform to select a region
2. Click **Cut** (or use the keyboard shortcut)
3. The selected region is removed — audio before and after plays seamlessly

**Making a mute:**
1. Click and drag on the waveform to select a region
2. Click **Mute** (or use the keyboard shortcut)
3. The selected region is silenced — the duration is preserved but no sound plays

You can undo cuts and mutes at any time. For an alternative editing approach, see [Editing with Transcripts](/editing/transcripts).

[screenshot: Waveform with a selected region showing cut/mute options]

## How do I preview my episode?

Use the playback controls to preview your episode:

- **Play/Pause** — start or stop playback
- **Seek** — click anywhere on the timeline to jump to that position
- The playback respects all your edits (cuts, mutes) and plays sections and blocks in order

The preview plays your episode as it will sound after generation, including any [background music](/editing/background-music) you've assigned.

## Common Issues

**Audio isn't playing when I press play**
Make sure your browser tab isn't muted. Check that you have audio blocks with content in at least one section.

**Waveform isn't loading**
The waveform generates after upload. If it's still missing after a minute, try refreshing the page. The audio file itself is safely stored.

**I hear unexpected silence between sections**
Check for empty audio blocks or break blocks with long durations. Also check that audio blocks are in the correct order within each section.

**I accidentally made a cut — how do I undo?**
Use undo (Ctrl/Cmd+Z) to reverse your last edit.

## Related

- [Uploading Audio](/creating/uploading-audio) — get audio into your episode
- [Editing with Transcripts](/editing/transcripts) — text-based alternative to waveform editing
- [AI Audio Enhancement](/editing/ai-enhancement) — improve audio quality
- [Generating Your Episode](/publishing/generating) — create the final file from your edits
- [Concepts & Terminology](/getting-started/concepts#cuts-and-mutes) — definitions of cuts and mutes
```

- [ ] **Step 2: Create editing/transcripts.mdx**

```mdx
---
title: "Editing with Transcripts"
description: "How to transcribe audio in Henshu and use text-based editing to make cuts and mutes by selecting words in the transcript."
sidebarTitle: "Transcripts"
keywords: ["transcription", "transcript", "text-based editing", "text editing", "speech to text", "cut", "mute", "select text", "descript", "quota"]
---

# Editing with Transcripts

Henshu can [transcribe](/getting-started/concepts#transcription) your audio files into text using AI, letting you edit audio by selecting words — like editing a document. Cuts and mutes created from transcript selections sync with the waveform editor.

## Overview

Text-based editing is an alternative to editing directly on the waveform. After transcribing an audio file, you see the full text of what was spoken. To remove something, just select the words in the transcript — Henshu creates the corresponding cut or mute on the audio automatically. Changes sync bidirectionally: edits made on the waveform are also reflected in the transcript.

## How do I transcribe an audio file?

1. In the editor, select the audio file you want to transcribe
2. Click **Transcribe**
3. Wait for the AI transcription to complete — this typically takes a fraction of the audio's duration
4. The transcript panel appears with the full text of your audio

[screenshot: Audio file with Transcribe button]

Transcription uses AI-powered speech recognition with word-level timestamps, so each word maps precisely to a moment in the audio.

## How do I edit using the transcript?

Once an audio file is transcribed:

1. Open the transcript panel
2. Read through the text and find the section you want to edit
3. **Select words** by clicking and dragging across the text
4. Choose **Cut** (remove the audio) or **Mute** (silence the audio)
5. The waveform updates automatically to reflect your edit

[screenshot: Transcript panel with text selected and cut/mute options visible]

The transcript highlights edited regions so you can see what's been cut or muted.

## How does transcript editing sync with the waveform?

Edits sync bidirectionally:

- **Transcript → Waveform:** Selecting and cutting words in the transcript creates the corresponding cut on the waveform
- **Waveform → Transcript:** Making a cut or mute on the waveform highlights the affected words in the transcript

This means you can switch between waveform and transcript editing freely — both views always show the same edits.

<Note>
  **Free plan limit:** Transcription has a lifetime usage quota. To check your remaining quota or learn about plan limits, see [Plans & Quotas](/account/plans-and-quotas).
</Note>

## Common Issues

**Transcription is taking a long time**
Longer audio files take more time to transcribe. A 30-minute recording typically takes a few minutes. If it seems stuck for more than 10 minutes, try refreshing the page — the transcription continues in the background.

**The transcript has errors or inaccurate words**
AI transcription isn't perfect, especially with unusual names, technical jargon, or heavy accents. The transcript is a tool for navigating and editing your audio — small text inaccuracies don't affect the audio output. Focus on using the transcript to locate the sections you want to edit.

**"Quota exceeded" error when trying to transcribe**
You've reached your plan's transcription limit. See [Plans & Quotas](/account/plans-and-quotas) for details on limits and upgrading.

**My edits in the transcript aren't showing on the waveform (or vice versa)**
Try refreshing the page. Both views should always stay in sync. If the issue persists after refresh, the transcription data may need to reload.

## Related

- [Using the Audio Editor](/editing/audio-editor) — waveform-based editing
- [AI Audio Enhancement](/editing/ai-enhancement) — improve audio quality before or after editing
- [Plans & Quotas](/account/plans-and-quotas) — transcription limits for your plan
- [Concepts & Terminology](/getting-started/concepts#transcription) — definition of transcription and text-based editing
```

- [ ] **Step 3: Create editing/ai-enhancement.mdx**

```mdx
---
title: "AI Audio Enhancement"
description: "How to use Henshu's AI-powered audio enhancement to automatically clean up your recordings with noise reduction and volume leveling."
sidebarTitle: "AI Enhancement"
keywords: ["enhancement", "enhance", "AI", "noise reduction", "volume leveling", "audio cleanup", "mastering", "audio quality", "one-click"]
---

# AI Audio Enhancement

Henshu's AI [enhancement](/getting-started/concepts#enhancement) automatically cleans up your audio recordings with noise reduction and volume leveling — improving quality with a single click.

## Overview

Raw podcast recordings often have background noise, inconsistent volume levels, or other quality issues. Enhancement processes your audio through an AI pipeline that addresses these problems automatically. The result is a cleaner, more professional-sounding recording.

## How do I enhance an audio file?

1. In the editor, select the audio file you want to enhance
2. Click **Enhance**
3. Wait for processing to complete — the file will show a gold badge when done

[screenshot: Audio file with Enhance button, and another file showing the gold "Enhanced" badge]

Enhancement runs in the background. You can continue editing while it processes.

## What does enhancement do?

Enhancement applies two main improvements:

- **Noise reduction** — removes background noise, hum, and environmental sounds
- **Volume leveling** — normalizes audio levels so quiet and loud parts are more consistent

The enhanced version replaces the working copy used for editing and generation. Your original upload is always preserved.

## Key Details

- Enhancement is a one-click operation — no manual settings to configure
- Processing time depends on file length; most files complete within a minute
- Enhanced files show a gold badge in the editor so you can tell them apart
- You can enhance a file before or after making cuts and mutes — the enhancement applies to the audio itself, not to your edits
- Enhancement is available for individual audio files, not entire episodes at once

## Common Issues

**Enhancement is taking a long time**
Longer audio files take more processing time. Files over 30 minutes may take several minutes. The processing happens in the cloud, so you can continue editing other files while waiting.

**The enhanced audio doesn't sound as good as expected**
Enhancement works best on voice recordings. If your audio has very heavy distortion or extreme noise, the AI may not be able to fully clean it up. In most cases, enhancement significantly improves standard podcast recordings.

**Enhancement failed**
If enhancement fails, try again. If it continues to fail, the audio file may have an issue that prevents processing. You can continue editing with the unenhanced version.

## Related

- [Using the Audio Editor](/editing/audio-editor) — edit your audio before or after enhancement
- [Uploading Audio](/creating/uploading-audio) — upload files to enhance
- [Generating Your Episode](/publishing/generating) — enhanced audio is used in the final output
- [Concepts & Terminology](/getting-started/concepts#enhancement) — definition of enhancement
```

- [ ] **Step 4: Create editing/background-music.mdx**

```mdx
---
title: "Adding Background Music"
description: "How to add background music (BGM) to your podcast sections in Henshu, including volume control, ducking, fade settings, and smart looping."
sidebarTitle: "Background Music"
keywords: ["BGM", "background music", "music", "ducking", "smart loop", "fade", "volume", "loop", "library", "audio", "section"]
---

# Adding Background Music

Henshu's [BGM](/getting-started/concepts#bgm-background-music) (background music) system lets you add music to individual sections of your episode, with controls for volume, [ducking](/getting-started/concepts#ducking), fades, and [looping](/getting-started/concepts#smart-loop).

## Overview

Background music is assigned per [section](/getting-started/concepts#sections), not per episode. This means your intro can have upbeat music, your interview section can have subtle ambient music, and your outro can have different music entirely. The music library is linked to your [show](/creating/shows), so tracks you add are available across all episodes in that show.

## How do I add background music to a section?

1. In the editor, select the section you want to add music to
2. Open the **BGM panel** from the sidebar
3. Browse the music library — you'll see tracks available for your show
4. Click a track to assign it to the section
5. The music is now linked to that section and will play underneath your voice audio

[screenshot: BGM panel showing music library and a track assigned to a section]

## How do I adjust BGM settings?

Once a track is assigned to a section, you can configure:

### Volume

Set the music volume relative to your voice audio:
- **Normal** — standard background level
- **Louder** — music is more prominent
- **Quieter** — music sits further back behind voice

### Ducking

When **ducking** is enabled, the music volume automatically dips when voice audio is playing, then rises during pauses. This ensures your voice is always clearly audible over the music without manual volume adjustments.

### Fade In / Fade Out

Set the duration (in seconds) for the music to fade in at the start of the section and fade out at the end. This creates smooth transitions instead of abrupt starts and stops.

### Play Mode

Choose how the music behaves when the section is longer than the track:

| Mode | Behavior |
|------|----------|
| **Once** | Play the track once and stop — silence for the rest of the section |
| **Loop** | Restart from the beginning when the track ends |
| **Smart Loop** | Crossfade at configured cue points for seamless, natural-sounding loops |

[Smart loop](/getting-started/concepts#smart-loop) produces the most polished result for sections that are longer than the music track.

[screenshot: BGM settings panel showing volume, ducking, fade, and play mode controls]

## How do I remove BGM from a section?

To remove background music from a section, open the BGM panel for that section and click **Remove** (or deselect the current track). The section will play without any background music.

## Key Details

- BGM is per-section, not per-episode — different sections can have different music
- The music library is per-show — add tracks once and use them across episodes
- BGM settings (volume, ducking, fades, play mode) are independent for each section
- Background music is mixed into the final file when you [generate your episode](/publishing/generating)
- BGM does not appear as a waveform in the main editor — it plays during preview and is included in the generated output

## Common Issues

**Music is too loud and drowning out my voice**
Enable **ducking** to automatically lower the music when voice is playing. You can also set the volume to **Quieter** for a more subtle background level.

**Music isn't looping as expected**
Check the **play mode** setting. If set to "Once," the music stops after one play. Switch to "Loop" or "Smart Loop" for continuous music throughout the section.

**Ducking doesn't seem to be working**
Ducking activates when voice audio is detected. If your section has mostly silence or very quiet speech, ducking may not trigger noticeably. Make sure ducking is toggled on in the BGM settings for that section.

**I don't see any music in the library**
The BGM library is linked to your show. Browse the available tracks in the library panel. If you're looking for a specific track, it may need to be added to your show's library first.

## Related

- [Using the Audio Editor](/editing/audio-editor) — the editor where you assign BGM
- [Creating a Show](/creating/shows) — shows have their own BGM libraries
- [Generating Your Episode](/publishing/generating) — BGM is mixed into the final output
- [Concepts & Terminology](/getting-started/concepts#bgm-background-music) — definitions of BGM, ducking, and smart loop
```

- [ ] **Step 5: Verify pages render**

```bash
mint dev
```

Open http://localhost:3000 and verify the "Editing" group renders with all four pages, cross-links work, and Note callouts render correctly.

- [ ] **Step 6: Commit**

```bash
git add editing/
git commit -m "docs: add Editing pages

Add Audio Editor, Transcripts, AI Enhancement, and Background Music
pages covering all editing features with troubleshooting sections."
```

---

## Task 5: Publishing Pages

**Files:**
- Create: `publishing/generating.mdx`
- Create: `publishing/downloading.mdx`

- [ ] **Step 1: Create publishing/generating.mdx**

```mdx
---
title: "Generating Your Episode"
description: "How to generate your podcast episode in Henshu — assembling sections, audio blocks, edits, and background music into a final audio file."
sidebarTitle: "Generating"
keywords: ["generate", "export", "render", "finalize", "assemble", "episode", "output", "processing", "final file"]
---

# Generating Your Episode

[Generating](/getting-started/concepts#generate-episode-generation) is the final step — Henshu assembles all your sections, audio blocks, edits, and background music into a single polished audio file.

## Overview

When you generate an episode, Henshu takes everything you've arranged in the editor and produces a final output file. This includes:

- All sections in order
- All audio blocks with your cuts and mutes applied
- Break blocks rendered as silence
- Background music mixed in per section (with volume, ducking, and fade settings applied)
- Enhanced audio used where available

The result is a single audio file ready for publishing.

## How do I generate my episode?

1. Make sure your episode is arranged the way you want — check sections, audio blocks, and BGM assignments
2. Click **Generate Episode**
3. Wait for processing to complete — you'll see a progress indicator

[screenshot: Generate Episode button in the editor]

Processing time depends on your episode's total duration and complexity (number of sections, BGM tracks, etc.). Most episodes generate within a few minutes.

## What gets included in the generated file?

| Included | Not included |
|----------|-------------|
| All sections in their current order | Deleted audio (cuts are applied) |
| All audio blocks within each section | Muted regions (silence replaces the audio) |
| Break blocks (rendered as silence) | Unused audio files not placed in blocks |
| Background music with all settings | |
| AI-enhanced audio (if enhanced) | |

## Key Details

- Generation runs in the cloud — you can close the browser and come back later
- You can re-generate after making changes; the previous generated file is replaced
- Generation time depends on episode duration and complexity (sections, BGM, enhancements)
- Only audio placed in audio blocks within sections is included — files sitting in the upload area but not placed in a block are excluded

## Common Issues

**Generation seems stuck or is taking a long time**
Longer episodes with multiple sections and BGM tracks take more processing time. If generation seems stuck for more than 15 minutes, try refreshing the page. The generation process continues in the cloud even if you close the browser.

**Missing audio in the generated file**
Check that your audio files are placed in audio blocks within sections. Audio files that are uploaded but not placed in any audio block won't be included in the generated output.

**Background music isn't in the generated file**
Verify that BGM is assigned to the section(s) in the BGM panel. Also check that the play mode, volume, and fade settings are configured. Preview your episode before generating to confirm the music sounds right.

## Related

- [Downloading & Sharing](/publishing/downloading) — get your generated file
- [Using the Audio Editor](/editing/audio-editor) — arrange your episode before generating
- [Adding Background Music](/editing/background-music) — BGM settings affect the generated output
- [Concepts & Terminology](/getting-started/concepts#generate-episode-generation) — definition of generation
```

- [ ] **Step 2: Create publishing/downloading.mdx**

```mdx
---
title: "Downloading & Sharing"
description: "How to download your generated podcast episode from Henshu and share it with your audience."
sidebarTitle: "Downloading"
keywords: ["download", "share", "export", "publish", "podcast host", "file", "generated episode", "output"]
---

# Downloading & Sharing

After [generating your episode](/publishing/generating), you can download the final audio file and share it with your audience.

## Overview

Once generation is complete, your finished podcast episode is available as a downloadable audio file. You can then upload it to your podcast hosting platform, share it directly, or use it however you like.

## How do I download my generated episode?

1. After generation completes, the episode status changes to **Generated**
2. Click **Download** to save the audio file to your computer

[screenshot: Download button on a generated episode]

## What format is the downloaded file?

The generated file is a standard audio format suitable for podcast distribution. You can upload it directly to any podcast hosting platform.

## What can I do with the file?

Once downloaded, you can:

- **Upload to a podcast host** — services like Spotify for Podcasters, Apple Podcasts Connect, Buzzsprout, Podbean, Anchor, etc.
- **Share directly** — send the file to collaborators or post it on social media
- **Archive** — keep a local copy of your finished episodes

Henshu handles the editing and production — distribution is up to you and your podcast host.

## Key Details

- You can re-download a previous generation at any time — the file stays available until you generate a new version
- The generated file is a standard podcast-ready audio format compatible with all major hosting platforms
- Henshu handles editing and production — distribution is up to you and your podcast host

## Common Issues

**Download link isn't working**
Try refreshing the page. If the download still doesn't start, the generated file may still be processing. Wait for the episode status to show **Generated** before attempting to download.

**I need a different file format**
Henshu generates a standard podcast-ready audio format. If you need a specific format for your hosting platform, use a free audio converter tool after downloading.

## Related

- [Generating Your Episode](/publishing/generating) — create the final file before downloading
- [Your First Episode](/getting-started/first-episode) — full walkthrough including download
```

- [ ] **Step 3: Verify pages render**

```bash
mint dev
```

Verify the "Publishing" group renders with both pages.

- [ ] **Step 4: Commit**

```bash
git add publishing/
git commit -m "docs: add Publishing pages

Add Generating and Downloading & Sharing pages covering
episode generation and output distribution."
```

---

## Task 6: Account Pages

**Files:**
- Create: `account/setup.mdx`
- Create: `account/plans-and-quotas.mdx`
- Create: `account/subscription.mdx`

- [ ] **Step 1: Create account/setup.mdx**

```mdx
---
title: "Account Setup"
description: "How to create your Henshu account, verify your email, and reset your password."
sidebarTitle: "Account Setup"
keywords: ["account", "sign up", "register", "email verification", "password reset", "login", "authentication"]
---

# Account Setup

Create your Henshu account to start editing podcasts. This page covers registration, email verification, and password recovery.

## Overview

Henshu uses email-based authentication. You sign up with your email address and a password, verify your email, and you're ready to start creating shows and episodes.

## How do I create an account?

1. Go to [app.henshu.io](https://app.henshu.io)
2. Click **Sign Up**
3. Enter your email address and choose a password
4. Click **Create Account**
5. Check your email for a verification link

[screenshot: Sign up page]

## How do I verify my email?

After signing up, Henshu sends a verification email to the address you registered with.

1. Check your inbox for an email from Henshu
2. Click the verification link in the email
3. Your account is now verified and fully active

If you don't see the email, check your spam folder.

## How do I reset my password?

If you've forgotten your password:

1. Go to the login page at [app.henshu.io](https://app.henshu.io)
2. Click **Forgot Password**
3. Enter your email address
4. Check your email for a password reset link
5. Click the link and set a new password

## FAQ

**I didn't receive the verification email**
Check your spam/junk folder. If it's not there, try signing up again or contact support.

**Can I change my email address?**
Contact support to update the email address associated with your account.

**Can I delete my account?**
Contact support to request account deletion.

## Related

- [Plans & Quotas](/account/plans-and-quotas) — understand what's included in your plan
- [Managing Your Subscription](/account/subscription) — upgrade or manage billing
- [Your First Episode](/getting-started/first-episode) — get started after creating your account
```

- [ ] **Step 2: Create account/plans-and-quotas.mdx**

This is the **canonical source** for all quota and plan limit information. All other pages link here.

```mdx
---
title: "Plans & Quotas"
description: "Henshu plan details and usage quotas — what's included in the Free and Standard plans, how quotas work, and how to check your remaining usage."
sidebarTitle: "Plans & Quotas"
keywords: ["plan", "pricing", "quota", "free plan", "standard plan", "limit", "upload limit", "transcription limit", "usage", "storage", "upgrade"]
---

# Plans & Quotas

Henshu offers a Free plan and a Standard plan. This page explains what's included in each and how usage quotas work.

## Overview

All Henshu accounts start on the **Free plan**, which lets you explore the full editor with generous usage quotas. The **Standard plan** removes all limits for unlimited podcast production. For current pricing, visit [henshu.io](https://henshu.io).

## Free Plan

The Free plan gives you access to all of Henshu's features with lifetime usage quotas:

| Feature | Free Plan Limit |
|---------|----------------|
| **Upload quota** | 5 hours (300 minutes) lifetime |
| **Transcription quota** | 60 minutes lifetime |
| Shows | Unlimited |
| Episodes | Unlimited |
| Audio editing (cuts, mutes) | Unlimited |
| AI audio enhancement | Unlimited |
| Background music | Full library access |
| Episode generation | Unlimited |

The Free plan is a great way to try Henshu and produce your first episodes.

## Standard Plan

The Standard plan removes all usage limits:

| Feature | Standard Plan |
|---------|--------------|
| **Upload quota** | Unlimited |
| **Transcription quota** | Unlimited |
| Everything else | Same as Free — all features included |

To upgrade, see [Managing Your Subscription](/account/subscription).

## How do quotas work?

Quotas on the Free plan are **lifetime limits** — they track your total usage across all time, not per month.

### Upload quota

Your upload quota is measured by the total duration of audio you've uploaded. Each audio file's duration counts toward the quota when it finishes processing.

**Important:** Upload quota is monotonic — deleting episodes or audio files does **not** reclaim quota. Once duration is counted, it stays counted.

### Transcription quota

Your transcription quota is measured by the total duration of audio you've transcribed. Each transcription request counts the audio file's duration toward the quota.

**Important:** Like upload quota, transcription quota is monotonic — deleting transcribed files does not reclaim quota.

## How do I check my remaining quota?

You can see your current usage and remaining quota in your account settings within the app.

[screenshot: Quota usage display in account settings]

## What happens when I hit a quota limit?

- **Upload quota exceeded:** You won't be able to upload new audio files. Existing files and episodes are unaffected — you can still edit, enhance, generate, and download.
- **Transcription quota exceeded:** You won't be able to start new transcriptions. Existing transcriptions remain available for text-based editing.

In both cases, upgrading to the Standard plan immediately removes the limits.

## FAQ

**Do quotas reset each month?**
No. Free plan quotas are lifetime limits, not monthly. Once you use your quota, it stays used. Upgrading to Standard gives you unlimited usage going forward.

**If I delete an episode, do I get my quota back?**
No. Quotas are monotonic — they only count up. Deleting files or episodes does not reduce your usage count.

**Does enhancing audio use my upload quota?**
No. Enhancement processes an already-uploaded file. It does not count toward your upload quota.

**Does background music count toward my upload quota?**
No. BGM comes from Henshu's music library and doesn't affect your upload quota.

## Related

- [Managing Your Subscription](/account/subscription) — how to upgrade to Standard
- [Uploading Audio](/creating/uploading-audio) — where you'll encounter upload quota limits
- [Editing with Transcripts](/editing/transcripts) — where you'll encounter transcription quota limits
```

- [ ] **Step 3: Create account/subscription.mdx**

```mdx
---
title: "Managing Your Subscription"
description: "How to upgrade your Henshu plan, manage billing through the Stripe customer portal, view invoices, and cancel your subscription."
sidebarTitle: "Subscription"
keywords: ["subscription", "upgrade", "billing", "payment", "Stripe", "invoice", "cancel", "plan", "manage"]
---

# Managing Your Subscription

Manage your Henshu subscription — upgrade to Standard, view invoices, update payment methods, and cancel if needed. Billing is handled securely through Stripe.

## Overview

Henshu uses [Stripe](https://stripe.com) for secure payment processing. When you upgrade or manage your subscription, you interact with Stripe's hosted checkout and customer portal. Henshu never stores your payment information directly.

## How do I upgrade to the Standard plan?

1. Go to your account settings in the app
2. Click **Upgrade** (or **Subscribe**)
3. You'll be redirected to Stripe's checkout page
4. Enter your payment details and confirm
5. You'll be redirected back to Henshu with your plan active immediately

[screenshot: Upgrade button in account settings]

After upgrading, all quota limits are removed and you have unlimited upload and transcription.

## How do I manage my billing?

To update your payment method, view invoices, or make other billing changes:

1. Go to your account settings
2. Click **Manage Subscription** (or **Billing Portal**)
3. You'll be redirected to Stripe's customer portal where you can:
   - Update your credit card or payment method
   - View and download past invoices
   - See your next billing date

[screenshot: Manage Subscription button in account settings]

## How do I cancel my subscription?

1. Go to your account settings
2. Click **Manage Subscription** to open the Stripe customer portal
3. Click **Cancel Plan** in the portal

**What happens when you cancel:**
- Your Standard plan stays active until the end of the current billing period
- After it expires, your account reverts to the Free plan
- All your shows, episodes, and content remain intact
- You'll be subject to Free plan quota limits for new uploads and transcriptions going forward
- You can re-subscribe at any time to restore unlimited access

## FAQ

**Is my payment information secure?**
Yes. Henshu uses Stripe for payment processing. Your card details are handled entirely by Stripe and never touch Henshu's servers.

**Can I get a refund?**
Contact support at support@henshu.io to discuss refund requests.

**Will I lose my data if I cancel?**
No. All your shows, episodes, and content remain intact. You revert to the Free plan with its quota limits.

**Can I switch between monthly and annual billing?**
See the Stripe customer portal for available billing options.

## Related

- [Plans & Quotas](/account/plans-and-quotas) — understand what each plan includes
- [Account Setup](/account/setup) — create your account
```

- [ ] **Step 4: Verify pages render**

```bash
mint dev
```

Verify the "Account" group renders with all three pages and the Note callouts on other pages link correctly to plans-and-quotas.

- [ ] **Step 5: Commit**

```bash
git add account/
git commit -m "docs: add Account pages

Add Account Setup, Plans & Quotas (canonical quota source),
and Managing Your Subscription pages."
```

---

## Task 7: Cross-Link Verification and Final Cleanup

**Files:**
- Verify: all `.mdx` files for broken cross-links
- Modify: any files with broken links

- [ ] **Step 1: Run Mintlify validation and broken link checker**

```bash
mint validate
mint broken-links
```

Fix any validation errors or broken links reported. Common issues to check:
- All `href` paths in `<Card>` components match actual file paths (without `.mdx` extension)
- All markdown links like `[text](/path)` point to valid pages
- Anchor links like `#section-name` match actual heading slugs in the target page

- [ ] **Step 2: Verify full navigation**

```bash
mint dev
```

Open http://localhost:3000 and manually verify:
- All 15 pages load without errors
- Navigation sidebar shows all 5 groups with correct pages
- "User Guide" tab is the active tab
- Global anchors (Henshu App, Website) appear in the nav
- Top-right button says "Open Henshu"
- Cross-links between pages work (click through several)
- Note callouts on upload and transcription pages render correctly
- CardGroup on the Welcome page renders correctly

- [ ] **Step 3: Fix any issues found**

Apply fixes to any broken links, rendering issues, or navigation problems found in steps 1-2.

- [ ] **Step 4: Commit if any fixes were needed**

Stage only the specific files that were fixed, then commit:

```bash
git add <fixed-files>
git commit -m "docs: fix broken links and rendering issues"
```

Only create this commit if changes were made. Use `git diff` to verify only intended changes are staged.

- [ ] **Step 5: Final verification**

Verify all milestones are met:

```bash
git log --oneline -10
```

**Expected milestones** (each should have at least one commit):
- [ ] Starter content removed and docs.json + AGENTS.md configured
- [ ] Getting Started pages exist (3 files in `getting-started/`)
- [ ] Creating & Organizing pages exist (3 files in `creating/`)
- [ ] Editing pages exist (4 files in `editing/`)
- [ ] Publishing pages exist (2 files in `publishing/`)
- [ ] Account pages exist (3 files in `account/`)
- [ ] `mint validate` and `mint broken-links` pass with no errors

The exact number of commits may vary (fix commits, combined tasks, etc.). What matters is that all 15 pages are committed, the config is correct, and validation passes.
