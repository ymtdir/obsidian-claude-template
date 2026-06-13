---
name: writing-articles
description: Write a technical article. Fact-check by referencing 20_NOTES, follow a view-count-oriented structure template, and save it in 30_ARTICLES.
argument-hint: '[topic]'
---

Write a technical article and save it in `30_ARTICLES/`. Fact-check by referencing 20_NOTES, and write it following a view-count-oriented structure (title, what this article covers, conclusion-first).

Argument: `$ARGUMENTS` (article topic)

## Steps

### 1. Decide and research the topic

- Identify the topic from the argument
- Grep `20_NOTES/` for related notes (including synonyms and related technologies)
- Read the contents of the existing WIKI notes and use them as the foundation of the article
- Complement missing parts with WebSearch, prioritizing **primary sources** (official docs, RFCs, papers, etc.)
- Keep Claude's knowledge as a supplement only; do not write facts based on guesses

### 2. Fact-check

- Always back up the **technical facts, version info, API specs, and numbers** claimed in the article with primary sources
- If there is a discrepancy with an existing description in `20_NOTES/`, confirm which is correct with WebSearch before writing
- Do not include claims that could not be verified (or mark them explicitly as "needs verification")

### 3. Design the structure (to earn views)

Build the article with the following structure (keep a balance of **seriousness 7 : buzz factor 3**; overdoing it damages trust).

**⚠️ Not all sections are mandatory**. The below is just a general template; **select what to keep or drop** depending on the nature of the article. E.g. a 共感フック is unnatural in an article that does not deal with a known problem; for concept-explanation articles, a "gradual organization of concepts" fits better than "Step splitting"; an 早見表 is unnecessary for articles with no comparison/selection elements. **In principle the only strictly required ones are the 3: TL;DR, 結論, and まとめ**; drop the others when they do not fit the content:

- **タイトル** (filename): concrete + number + benefit (e.g. 「Rust の所有権を図解で 5 分で理解する」, 「7 つのアンチパターンで学ぶ React Hooks」). Do not over-bait, and include search keywords naturally
- **TL;DR** [Required]: present the conclusion up front within 3 lines. An essential element that lands even with skim readers
- **対象読者**: prerequisite knowledge, the post-read goal, reading time. Make readers feel it is "addressed to me"
- **共感フック** (「こんな経験ありませんか？」): verbalize the reader's troubles to prevent drop-off. **Strong in practical articles, but drop it for pure explanation/cheat-sheet articles**
- **結論** [Required]: complete it in one paragraph so even people who do not read the body get the answer
- **なぜそうなるのか**: a deep dive into the background and causes. Creates the "I see"
- **解決方法**: split into stages with `### Step 1` `### Step 2` `### Step 3`. Give a minimal working code example per Step. **Effective for tutorial/how-to articles. For concept-explanation articles, a parallel structure like "organize the concepts → code example → pitfalls" fits better**
- **アンチパターン** (やってはいけないこと): "sharing where you got stuck" gets shared strongly. Write it fact-based (to prevent flame wars)
- **早見表**: a save-worthy reference element such as a comparison table or checklist. **Powerful for articles with comparison/selection; drop it if there is none**
- **まとめ** [Required]: within 3 key points, **with numbers**, to make them memorable
- **次のステップ + 参考文献**: **only external primary sources** such as official docs, RFCs, and papers. `20_NOTES/` is a private internal vault note, so **do not include it** in the references of a publicly published article

### 4. Write following template.md

- Read `.claude/skills/writing-articles/assets/template.md` and write the body in that structure
- Write within the range of general Markdown (do not depend on the posting destination's platform-specific notation)
- Do not forget the language specifier on code blocks (` ```rust `, ` ```ts `, etc.)
- Place image references in `99_ASSETS/` and reference them with relative paths

### 5. Save in 30_ARTICLES

- The filename is a name that concisely expresses the article title (Japanese OK; identical to the `[[wikilink]]` notation)
- **Pre-check `30_ARTICLES/` with Glob before saving** to detect a collision with a file of the same name
- On collision, **Read the existing file to grasp its angle** and write the new article from an angle that avoids duplication
- Differentiate the filename **with a parenthetical note** (e.g. `Rust所有権（入門）.md`, `GraphQLスキーマ設計（N+1問題編）.md`)
- **Do not write frontmatter** (it is assumed to be added later via the posting destination's CLI/Web UI; this skill handles only the article body)
- Start headings from `##` and do not write a `# title` (the filename serves as the title)
- Do not add `[[wikilink]]` (links would break at the external publication destination)

### 6. Report

- Present the file path, title, and overview of the created article
- State explicitly which `20_NOTES/` notes were referenced for the fact-check
