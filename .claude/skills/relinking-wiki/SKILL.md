---
name: relinking-wiki
description: Inspect and repair the links in 20_NOTES. Periodically detect and re-add missing references from old notes to new notes, and broken links. Orphan notes and contradictory descriptions are detected as a secondary function.
---

Inspect the links between notes in `20_NOTES/` and repair breaks and omissions. When a note for a concept that did not yet exist at the time an old note was written is added later, the reference often stays unlinked. This skill periodically detects and re-adds them.

## Main functions

### 1. Fix broken links

- List `20_NOTES/*.md` with Glob
- Extract `[[X]]`-form links from each note and list the ones where `X.md` does not exist in `20_NOTES/`
- If there is a similar filename, present it as a replacement candidate (**partial match or edit distance within 2; narrow the candidates to 1-3**)

### 2. Add missing links

Call the `zettelkasten-linker` agent **via the Agent tool with `subagent_type=zettelkasten-linker`** to obtain candidate note pairs that are related but not linked. This is the main procedure for catching missing references from old notes to newly added related notes.

## Secondary functions

### 3. Detect orphan notes

- **Judge only by the mutual links within `20_NOTES/`** (backlinks from other vault folders are out of scope)
- List notes that are not linked from anywhere

### 4. Detect contradictory descriptions

- **Identify notes covering the same concept**: against the filename list obtained in step 1, cluster them via 3 routes: **common keywords in titles + Grep of frequent words in the body + the by-product of step 2 (related pairs)**
- Within a cluster, detect places where definitions, numbers, or facts disagree between notes
- It need not be strict. Present suspicious pairs and leave the judgment to the user

## Applying fixes

Present the detection results in the following format, **all at once in a single message** (no paging needed):

```
## リンク切れ (N 件)
1. `note-a.md:12` `[[削除済みノート]]` → 候補: `[[代替ノート]]`
2. ...

## 張り忘れリンク候補 (K 件)
3. `[[A]]` ↔ `[[B]]`: 関連理由
...

## 孤立ノート (M 件)
4. `orphan-topic.md`
...

## 矛盾記述の候補 (L 件)
5. `X.md` vs `Y.md`: 食い違い内容
...
```

- Receive approval by **specifying item numbers** (e.g. `1-3, 5, 8-10`). Category-wide approval (e.g. 「リンク切れ全部」) is also allowed
- Apply fixes only to the approved items
- Insert links naturally into the context of the body (do not make an end-of-note list)
