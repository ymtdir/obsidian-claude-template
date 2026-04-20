# Obsidian Vault — Claude Code ルール

日本語で応答すること。

## Vault 構造

| フォルダ        | 役割                                                               | ファイル命名規則         | リンク戦略                               |
| --------------- | ------------------------------------------------------------------ | ------------------------ | ---------------------------------------- |
| `00_INBOX/`     | クリップ記事・読書メモなどソース素材の投げ入れ先。未整理のまま置く | 自由（内容がわかる名前） | 不要                                     |
| `10_WIKI/`      | 調査・学習ノート。フォルダ分けせずフラットに保存する               | トピックを端的に表す名前 | ノート間を `[[wikilink]]` で積極的に接続 |
| `20_DAILY/`     | デイリーノート。`/daily` でAIが添削＋まとめを生成                  | `YYYY-MM-DD.md`          | 学び・気づきから `10_WIKI/` へリンク     |
| `30_DOCUMENTS/` | 共有用ドキュメント・記事執筆用。外部出力するためリンク付け不要     | 自由                     | リンクを挿入しない                       |
| `70_PERSONAL/`  | ユーザー周辺のパーソナル情報。git 管理外                           | 用途を表す名前           | 不要                                     |
| `80_SECURE/`    | API キー・認証情報などの機密。git 管理外                           | 自由                     | 不要                                     |
| `90_ARCHIVES/`  | `/inbox` で取り込み済みのソース素材を退避する場所                  | 元ファイル名そのまま     | 不要                                     |
| `98_TEMPLATES/` | Obsidian のテンプレートファイル置き場                              | 用途を表す名前           | 不要                                     |
| `99_ASSETS/`    | 画像などのアセット                                                 | —                        | —                                        |

## ツェッテルカステン原則

- **1ノート = 1アイデア**: `10_WIKI/` の各ノートは単一のトピックを扱う
- **リンクで接続**: ノート間は `[[wikilink]]` で接続する。タグやフォルダではなくリンクが構造を作る
- **自律性**: 各ノートは単独で読んで意味が通じるように書く

## ノート作成ルール

- Obsidian のプロパティ（YAML frontmatter）は使わない
- ファイル名がタイトルになるので `10_WIKI/` では `# 見出し` は不要。見出しは `##` から使い、その下の区分けに `###` を使う
- 関連ノートへの `[[wikilink]]` は本文の文脈中に自然に埋め込む（末尾の一覧にまとめない）

## 個人情報の参照

ユーザーへの回答は `70_PERSONAL/` 配下のパーソナル情報（ユーザー自身・人間関係など）を踏まえて行う。質問・相談・雑談いずれでも該当しそうな話題が出たら Grep / Read で該当ノートを確認すること。人生相談や意思決定の文脈では積極的に参照する。`70_PERSONAL/` は git 管理外なので、記載内容をコミットや公開出力に混ぜないこと。

## 運用コマンド／スキル

運用手順の詳細は各スキル側に寄せる。このファイルは vault の "地図" のみを定義する。

- `/daily` → [.claude/skills/daily/SKILL.md](.claude/skills/daily/SKILL.md)
- `/wiki` → [.claude/skills/wiki/SKILL.md](.claude/skills/wiki/SKILL.md)
- `/inbox` → [.claude/skills/inbox/SKILL.md](.claude/skills/inbox/SKILL.md)
- `/translate` → [.claude/skills/translate/SKILL.md](.claude/skills/translate/SKILL.md)
- `/check` → [.claude/commands/check.md](.claude/commands/check.md)
- `ask`（auto-invoke）→ [.claude/skills/ask/SKILL.md](.claude/skills/ask/SKILL.md)
