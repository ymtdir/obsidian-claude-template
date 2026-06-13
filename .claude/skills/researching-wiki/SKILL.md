---
name: researching-wiki
description: When the user says they want to add something to the wiki, research the topic with web search and Claude's knowledge, and create one Zettelkasten-style note in 20_NOTES. Use /ingesting-inbox for ingesting INBOX material.
argument-hint: 'topic name'
---

Research a topic with web search and Claude's knowledge, and create one Zettelkasten-style note in 20_NOTES.

Argument: $ARGUMENTS (topic name)

## Steps

### 1. Research and organize

- Supplement and organize the topic
  1. First, Grep within `20_NOTES/` for related keywords to grasp the existing knowledge
     - Also search for synonyms of the topic, related technologies, and alternative services
  2. If something is missing, research with WebSearch
  3. Complement definitions and background with Claude's knowledge
  4. **If there is a clear error in the research results, correct it** (technical terms, concepts, version info, etc.)
- **Handling an existing note with the same name**
  - If the Grep in step 1-1 finds **an existing note on the same topic**, confirm with the user instead of creating a new one (do not create duplicates without permission)
  - Confirmation options: (1) update the existing note (add/correct), (2) create an independent sub-topic note from a different angle, (3) if it covers something different, separate them by naming (see "Topic ambiguity" below)
- **Check for topic ambiguity**
  - If the research reveals that the topic name refers to multiple different products, services, or concepts, confirm with the user
  - Example: "React" → React.js (library) and React Native (framework)
  - Example: "Surge" → Surge (network tool) and Surge.sh (hosting service)
  - The same applies when there are 3 or more candidates: present all candidates and let the user choose (not limited to 2 choices)
  - **Do not proceed to step 2 (note creation) until user confirmation is obtained**
- Following the principle of 1 note = 1 idea, if multiple topics are mixed in, propose splitting them

### 2. Create a note in 20_NOTES

- Use a filename that concisely expresses the topic (e.g. `Rustの所有権.md`)
  - **If the name is likely to collide with an existing note, use a distinguishable name**
  - Example: `Surge.sh.md`, `Surge（ネットワークツール）.md`
  - Supplement with the service name or technical category in parentheses as needed
- Create it following the format of `assets/template.md`
  - In the `## イメージで理解する` section, explain the concept with a familiar analogy
  - For **highly abstract topics** (concepts, mechanisms, theories; e.g. ownership, Reconciliation, functional programming), write it actively
  - For ones centered on **concrete products, services, or factual descriptions** (e.g. Surge, Docker Hub), it may be omitted
- Do not use properties (YAML frontmatter)
- Since the filename becomes the title, a `# heading` is unnecessary. Start body headings from `##`, and use `###` for sub-divisions under it
- Reuse the Grep results from step 1-1, and if there are related notes that hit, embed `[[wikilink]]` naturally into the body (do not re-run Grep)
- Do not collect links to related notes at the end; place them within the context

### 3. Post-processing

- Present the content of the created note to the user
