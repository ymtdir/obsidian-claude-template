---
name: inbox
description: 00_INBOX のソース素材を 10_WIKI に分解・取り込みする。処理後は 90_ARCHIVES へ退避。
argument-hint: '[ファイル名.md]（省略時は INBOX 全件）'
---

`.claude/skills/inbox/SKILL.md` の手順に従って実行してください。

引数としてファイル名が渡された場合は、`00_INBOX/<ファイル名>` のみを対象にしてください。
引数がない場合は `00_INBOX/` 直下の全ファイルを対象にしてください。
