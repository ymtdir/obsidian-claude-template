---
name: ingesting-inbox
description: Read source material in 00_INBOX and break it into multiple notes in 20_NOTES following Zettelkasten principles. After processing, move the source to 90_ARCHIVES.
argument-hint: '[filename.md]'
---

Take clipped articles, reading notes, and other source material dropped into `00_INBOX/`, break each source into multiple topics (1 source = multiple topics), and ingest them into `20_NOTES/`.

## Steps

### 1. Identify the target file(s)

- If a filename is given as an argument, target only `00_INBOX/<filename>`
- If no argument is given, list all `.md` files directly under `00_INBOX/` and process them one by one in order
- If there is no target, tell the user the INBOX is empty and finish

### 2. Read and decompose the source

- Read the source and identify topics for each major concept, person, technology, and example
- If the source is in English (or any language other than Japanese), translate both the note names and the body into Japanese when ingesting. Proper nouns, technical terms, and code identifiers may be kept in the original language
- Following the principle of 1 note = 1 idea, split into a granularity that can be read independently. **Granularity guideline**: 1 note = the unit that answers "one question". Paired concepts (e.g. shared reference vs. mutable reference) are in principle merged into 1 note; independent concepts go into separate notes
- For each candidate, Grep `20_NOTES/` and record it as a "merge candidate" when the **title matches exactly** or **the major concepts of the body largely overlap with an existing note** (if there are none, treat all as new)
- When merging, as a rule dissolve the content into an existing section; add a `## 追記` section only when it does not fit the existing structure
- Present the following to the user in **a single approval prompt** and obtain approval:
  - The decomposition plan (the list of planned note names)
  - The treatment of each note ("create new" or "merge into existing `X.md` as an addition")
  - A body summary is optional (it may be omitted when there are many notes)
- When processing multiple files, run a **per-file loop of approval → note creation → archive** (not all at once)
- If approval is denied, receive correction instructions, rebuild the decomposition plan, and present it again (re-approval loop)
- In non-interactive environments (such as subagent execution), skip the approval step, state the decisions clearly in the report, and proceed

### 3. Create notes in 20_NOTES

- Follow the format of `.claude/skills/researching-wiki/assets/template.md` (`## イメージで理解する` and `## まとめ` may be omitted; use `###` headings as a sub-division under `##`)
- The filename is a name that concisely expresses the topic (half-width spaces allowed; identical to the `[[wikilink]]` notation). When it collides with an existing note in `20_NOTES/`, add a parenthetical note (e.g. `Surge（ネットワークツール）.md`). Archive collisions (step 4) use a different rule (date suffix)
- Do not use properties (YAML frontmatter)
- Start headings from `##`
- Embed `[[wikilink]]` naturally into the context of the body (do not make an end-of-note list)
- Grep within `20_NOTES/`, and if there are related notes, create bidirectional links. **When multiple notes are created in the same batch, also link those notes to each other**

### 4. Archive the source file

- When ingestion is complete, move the original `00_INBOX/<file>` to `90_ARCHIVES/`
- **Keep the original filename** (the archive keeps the original name, independently of the note being made Japanese at creation time even for English articles)
- If a file with the same name exists in `90_ARCHIVES/`, add a date suffix `-YYYY-MM-DD` **before the extension** (e.g. `article.md` → `article-2026-04-22.md`)
- If it still collides even with the date suffix, add a **sequential number `-N`** (e.g. `article-2026-04-22-2.md`, `-3`, ...)

### 5. Report

- Present the list of newly created notes, the list of merged notes, and the list of archived source files
