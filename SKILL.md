---
name: new-research-project
description: >-
  Scaffold a new genealogical research project inside an Obsidian vault
  that uses Charted Roots (CR). Creates a Research Project index note plus
  a seeded Individual Research Note, both flat in the vault's shared
  Research folder (no per-project subfolder), using CR's cr_type
  frontmatter so the project shows up in existing Bases views immediately.
  Use this whenever the user wants to "start a new research project,"
  "research a new ancestor," "open a case file on" someone, or names a
  specific ancestor plus an open question (parentage, origin, identity, a
  conflicting record, immigration, etc.) with no existing project for them
  yet. Also use it for "help me dig into who X's parents were" when no
  project for X exists. Do not use for editing an existing project,
  creating a plain Person/Source/Event note (those have their own CR
  templates), or vaults that don't use Charted Roots.
license: CC-BY-NC-SA-4.0
metadata:
  version: "1.0.0"
  adapted_from: "Steve Little's `gra` skill in the Genealogy AI Starter Workspace (github.com/DigitalArchivst/Open-Genealogy/tree/main/skills/gra)"
  compatibility: "Obsidian vault with the Charted Roots plugin; Templates/GRA/ templates installed"
---

# New Research Project

Scaffold a new genealogy research project as a set of Charted Roots (CR)
notes, not as a duplicated folder of standalone files. This exists because
Steve Little's original Genealogy AI Starter Workspace expects each project
to carry its own copy of `AGENTS.md`, a source register, research logs, and
templates. In a Charted Roots vault, almost all of that is already handled
by shared, vault-wide structure — duplicating it per project would just
create drift between projects and make vault-wide search (Bases views)
incomplete. This skill creates only what's genuinely new per project: the
project's own identity and its links into the shared system.

## Before creating anything

Read `Templates/GRA/README.md` in the vault if it exists — it documents the
exact design this skill implements (why there's no per-project AGENTS.md,
where sources live, how project tagging works). If that file is missing,
this vault may not be set up for this workflow yet; tell the user and offer
to set up `Templates/GRA/` first (research-project templates, a shared
`Research/` folder, and a `projects` property on the Source templates)
before scaffolding a project into it.

## Step 1: Get the research question and subject

Never scaffold a project without a specific, focused research question. A
project titled after a person with no question ("research John Smith") is
not useful — GPS-aligned research answers one thing at a time (identity,
relationship, event, place, or activity). If the user hasn't given a
specific question yet, ask for it before proceeding: "What's the one
specific thing you want to find out about <person>?"

Also check whether a `People/` note for the subject already exists in the
vault (search by name). If it does, read its frontmatter — it's often a
GEDCOM import with useful (but uncited) facts worth carrying into the new
project's identity profile. If multiple people share the name and a similar
birth year, flag this explicitly rather than guessing which one the user
means — same-name disambiguation is a real methodological hazard here, not
a minor detail. Present the candidates and ask, or if the user's phrasing
already disambiguates (e.g. "b. 1760" vs. another with a different date),
proceed but still note the other candidate(s) as a related, unresolved
question inside the new project note rather than silently ignoring them.

## Step 2: Create the project's index note

Create `Research/<Descriptive Name> - Research Project.md` — flat, in the
shared `Research/` folder, the same way `Sources/`, `Places/`, `Events/`,
and `People/` are all flat with no per-item subfolder. There is no
`Projects/` folder in this design; don't create one. Use a disambiguating
name if more than one person shares the subject's name in the vault (e.g.
`John Patterson (b. 1760)` rather than bare `John Patterson`).

Base the note on `Templates/GRA/Research Project.md`, but don't just copy
the Templater placeholders verbatim — fill them in for real:

- `subject`: wikilink to the `People/` note if one exists, otherwise leave
  as a plain name pending a Person note.
- `status`: `open` for a brand-new project.
- `research_level`: `1` if nothing is known yet, `2` if the vault already
  has some uncited facts (typical for GEDCOM-imported people), higher only
  if real sourced research already exists.
- `related`: wikilinks to any same-name candidates flagged in Step 1.
- Fill in **Research question**, **Known facts** (pulled from the existing
  `People/` note if any, each row noting it's uncited if it is), **Scope
  and search plan** (suggest record types sized to the question's
  complexity — see the `gra` skill's GPS application guidance for how to
  size "simple" vs. "moderate" vs. "complex" research), and **Answer
  standard**.
- Leave the embedded `![[Charted Roots/Bases/research.base#By Project]]`
  and `![[Charted Roots/Bases/sources.base#By Project]]` embeds in place —
  they're how this project's linked research and sources surface without
  copying any of those notes onto the index note itself.

## Step 3: Seed an Individual Research Note

Create `Research/<Subject> - Identity Profile.md` from `Templates/GRA/
Individual Research Note.md`, with `project:` linking back to the new
project note. Populate the identity profile table from the existing
`People/` note's frontmatter if one exists (names, dates, places,
relationships) — mark every row as needing a citation unless one already
exists in `Sources/`. Note any same-name disambiguation issue from Step 1
here too, in its own section, so it isn't lost.

Do not populate the "Name and place variants" or "FAN cluster" tables with
invented entries just to fill space — a couple of well-reasoned starting
variants (period spelling conventions, common abbreviations) are useful;
a table padded with guesses is not.

## Step 4: Do not fabricate research activity

This is the most important rule in this skill. Steps 1-3 create the
*scaffolding* for a project — they do not perform research. Do not create
a `Research Log Entry` or `Research Journal` note describing a search that
didn't happen. It's fine (and honest) to create a `Research Journal` entry
documenting the scaffolding session itself ("today we set up the project
and identified an open disambiguation question"), because that genuinely
happened. It is not fine to invent a plausible-sounding search log entry
to make the project look further along than it is.

## Step 5: Report back

Tell the user what was created (paths), summarize the research question
and any disambiguation issue found, and suggest the first concrete next
step (usually: the first record type worth searching, per the scope and
search plan). Offer to open the `gra` or `family-history-planning` skill
if the user wants to move directly into analysis or a research plan.

## Reference

For the full rationale behind this project structure (why sources aren't
duplicated, why there's no per-project AGENTS.md, how CR's cr_type entity
types map to the original Genealogy AI Starter Workspace's files), see
`Templates/GRA/README.md` in the vault.
