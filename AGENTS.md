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
| Audio block | A container for audio within a section | — | "clip", "track" |
| Pause block | A block that inserts silence for a specified duration | pause, break block | "break" |
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
