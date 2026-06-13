---
name: asking-wiki
description: When the user asks something, consult 20_NOTES first and answer with source citations. A read-only skill for leveraging the knowledge accumulated in the vault.
---

When the user asks a question, answer by prioritizing the knowledge accumulated in the vault.

## Trigger

- The user's utterance is a question (e.g. 「〜とは？」「〜について教えて」「〜どうだっけ？」)
- And the question concerns a topic likely to be accumulated in the vault (technology, concepts, past learnings, etc.)

## When not to trigger

- **Questions about the repository/vault structure**: anything about "operational meta information" such as the configuration under `.claude/`, the vault folder structure (the role of `20_NOTES/` etc.), or the contents of CLAUDE.md
- **Coding work requests**: requests to implement, fix, or refactor
- **Command execution requests**: requests to launch skills such as `/ingesting-inbox` or `/researching-wiki`
- **Explicit suppression**: when the user explicitly says 「wikiを見ずに」 or 「一般論で」
- **Topics clearly unrelated to the vault**: weather, current events, small talk, etc. (not subjects of technology/learning)

## Steps

### 1. Search 20_NOTES

- Extract keywords from the question and search `20_NOTES/` using **both Glob for filename search and Grep for content search**
- Also search with synonyms, related technologies, and abbreviations (not only Japanese but also the English equivalents of the same concept)
- Narrow the hit candidates to 3-5. Priority order: **filename match > number of Grep hits > direct relevance to the question**

### 2. Read related notes

- Read the candidate notes and extract the descriptions relevant to the question
- As a rule, follow `[[wikilink]]`s within a note only **up to the direct link targets (one hop)**. Go further only when the main note is a stub and lacks information

### 3. Answer with source citations

- **Embed `[[note name]]` naturally into the context** of the answer body (do not collect them at the end; same policy as the note-creation rules in CLAUDE.md)
- When the relevant descriptions span multiple notes, cite each of them
- If there is no information in the vault, state so explicitly, check whether there is unprocessed material in `00_INBOX/`, and suggest `/ingesting-inbox`
- If there is no material in `00_INBOX/` either, state explicitly that there is nothing accumulated in the vault, and confirm with the user whether it is OK to answer in general terms (do not fill the gap with general knowledge on your own)
