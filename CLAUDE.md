# Obsidian Vault — Claude Code Rules

Respond in Japanese.

## Vault structure

| Folder             | Role                                                                                       | Filename convention                               | Link strategy                              |
| ------------------ | ------------------------------------------------------------------------------------------ | ------------------------------------------------- | ------------------------------------------ |
| `00_INBOX/`        | Drop zone for source material such as clipped articles and reading notes. Left unorganized | Free (a name that conveys the content)            | Not needed                                 |
| `10_WIKI/`         | Research/learning notes. Stored flat without subfolders                                    | A name that concisely expresses the topic         | Actively connect notes with `[[wikilink]]` |
| `20_DAILY/`        | Daily notes                                                                                | `YYYY-MM-DD.md`                                   | Link from learnings/insights to `10_WIKI/` |
| `30_DOCUMENTS/`    | General-purpose shared documents. No linking needed since they are output externally       | Free                                              | Do not insert links                        |
| `40_TRANSLATIONS/` | (No longer in use)                                                                         | —                                                 | —                                          |
| `50_ARTICLES/`     | Technical articles written with `/writing-articles`. Past articles accumulate too          | A name that concisely expresses the article title | Do not insert links                        |
| `90_ARCHIVES/`     | Place to move source material already ingested by `/ingesting-inbox`                       | The original filename as is                       | Not needed                                 |
| `99_ASSETS/`       | Assets such as images                                                                      | —                                                 | —                                          |

## Zettelkasten principles

- **1 note = 1 idea**: each note in `10_WIKI/` covers a single topic
- **Connect with links**: connect notes with `[[wikilink]]`. Links — not tags or folders — create the structure
- **Autonomy**: write each note so it makes sense when read on its own

## Note creation rules

- Do not use Obsidian properties (YAML frontmatter)
- Since the filename becomes the title, a `# heading` is unnecessary in `10_WIKI/`. Start headings from `##`, and use `###` for sub-divisions under it
- Embed `[[wikilink]]`s to related notes naturally into the context of the body (do not collect them in an end-of-note list)

## Referencing personal information

Base answers to the user on personal information stored outside the main wiki (the user themselves, their relationships, etc.). Whenever a potentially relevant topic comes up — in a question, a consultation, or small talk — check the corresponding note with Grep / Read. Reference it actively in the context of life advice and decision-making.

## Operational commands / skills

Keep the details of operational procedures within each skill. This file defines only the "map" of the vault.

- `/researching-wiki` → [.claude/skills/researching-wiki/SKILL.md](.claude/skills/researching-wiki/SKILL.md)
- `/ingesting-inbox` → [.claude/skills/ingesting-inbox/SKILL.md](.claude/skills/ingesting-inbox/SKILL.md)
- `/writing-articles` → [.claude/skills/writing-articles/SKILL.md](.claude/skills/writing-articles/SKILL.md)
- `/relinking-wiki` → [.claude/skills/relinking-wiki/SKILL.md](.claude/skills/relinking-wiki/SKILL.md)
- `asking-wiki` (auto-invoke) → [.claude/skills/asking-wiki/SKILL.md](.claude/skills/asking-wiki/SKILL.md)
