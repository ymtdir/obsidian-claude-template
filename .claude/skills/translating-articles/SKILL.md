---
name: translating-articles
description: Summarize and translate foreign-article clips in 00_INBOX, and save them in 40_TRANSLATIONS as 1 article = 1 note. Always append the original article URL at the end.
argument-hint: '[filename.md]'
---

Summarize and translate foreign-language (non-Japanese) article clips dropped into `00_INBOX/` into Japanese as 1 article = 1 note, and save them in `40_TRANSLATIONS/`. Always record the original article URL at the end. Do not touch the source material.

## Steps

### 1. Identify the target file(s)

- If a filename is given as an argument, target only `00_INBOX/<filename>`
- If no argument is given, list all `.md` files directly under `00_INBOX/` and process them one by one in order
- If there is no target, tell the user the INBOX is empty and finish

### 2. Read the source and identify the original article URL

- Read the file body with Read
- Automatically extract the original article URL from the body
  - Look for URLs starting with `http://` / `https://`, Markdown links, and heading/label lines such as `Source:` / `URL:` / `原文:`
  - If there are multiple candidates, prefer the URL that appears to be the article itself (the source noted at the start of the file, the URL appearing highest, etc.)
- If it cannot be found or determined, confirm the URL with the user before starting processing
- If the user answers "URL unknown" or "proceed without a URL", **abort processing** (do not save a note without a URL; this skill's policy mandates that the original article URL be stated)

### 3. Summarize and translate

- Grasp the article's main claims, points, and conclusions
- Summarize in Japanese. Prioritize readability over a word-for-word translation
- Basically follow the original article's chapter structure (heading structure)
  - Translate generic words in chapter headings (e.g. `Introduction` / `Summary` / `概述` / `最佳实践`) into Japanese (「はじめに」「まとめ」, etc.)
  - Keep **technical terms and proper nouns** in headings (`Virtual DOM`, `Fiber`, `goroutine`, `QUIC`, etc.) in the original language
- Keep proper nouns, technical terms, code identifiers, product names, and library names in the original language
- Keep code blocks as is; translate only the comments or explanatory text into Japanese if needed

### 4. Create a note in 40_TRANSLATIONS

- The filename is the Japanese translation of the original article title (e.g. `How React Works.md` → `Reactの仕組み.md`)
  - **The subtitle may be compressed** (the main title alone is OK; handle the subtitle in a heading at the start of the body)
  - **Replace OS reserved characters** (`/`, `:`, `?`, `*`, `|`, `\`) with `-` or `_` (e.g. `HTTP/3` → `HTTP-3`)
  - Use **full-width `：`** as the standard separator
- If it collides with an existing file, add a parenthetical note (e.g. `Reactの仕組み（2024年版）.md`)
- Do not use properties (YAML frontmatter)
- Since the filename becomes the title, a `# heading` is unnecessary. Start body headings from `##`, and use `###` for sub-divisions under it
- Do not add `[[wikilink]]` (`40_TRANSLATIONS/` has a no-linking policy)
- **Add a `## 出典` section at the end of the body and always record the original article URL**
  - Format: list it in Markdown link form (e.g. `- [title](URL)`)
  - **Use the original article's original title** (the pre-translation title) as the link text. The Japanese translated title is handled on the filename side; the source prioritizes faithfulness to the original
  - If the author, site name, or publication date is known, add them as list items on the following lines (e.g. `- 著者: name`, `- サイト: name`, `- 公開日: YYYY-MM-DD`)

### 5. Report

- Present the name of the created `40_TRANSLATIONS/` note
