# Obsidian Claude Template

Claude Code で Obsidian Vault を**第二の脳**として運用するためのテンプレート。ブックマークしっぱなしの記事や読書メモを `00_INBOX/` に放り込み、AI に分解・整理・リンク付けさせる。質問すれば vault の蓄積から答える。

## できること

- **クリップ**: Web Clipper で記事を `00_INBOX/` に1クリック保存
- **取り込み**: `/inbox` で記事を複数ノートに分解し `10_WIKI/` に配置。元記事は `90_ARCHIVES/` に退避
- **調査**: `/wiki <トピック>` で Web検索しながらノート作成
- **問い合わせ**: 質問すると vault を参照してソース引用付きで回答（`ask` スキルが auto-invoke）
- **点検**: `/check` でリンク切れ・孤立ノート・張り忘れリンク・矛盾を検出
- **日次ふりかえり**: `/daily` でデイリーノートの PDCA を添削＋まとめ生成

## Setup

1. GitHub で空の private リポジトリを作成する（README や .gitignore は追加しない）
2. クローンしてテンプレートをセットアップする

```bash
git clone https://github.com/<your-username>/<your-repo>.git
cd <your-repo>

git remote add upstream https://github.com/ymtdir/obsidian-claude-template.git
git fetch upstream
git merge upstream/main --allow-unrelated-histories
git push origin main
```

3. Obsidian を開き「Open folder as vault」でクローンしたフォルダを選択する

## Vault 構造

| フォルダ        | 役割                                       |
| --------------- | ------------------------------------------ |
| `00_INBOX/`     | ソース素材の投げ入れ先                     |
| `10_WIKI/`      | ツェッテルカステン形式の知識ノート（主役） |
| `20_DAILY/`     | デイリーノート                             |
| `30_DOCUMENTS/` | 共有用ドキュメント・記事執筆用             |
| `90_ARCHIVES/`  | `/inbox` で取り込み済みのソース素材        |
| `98_TEMPLATES/` | Obsidian テンプレート                      |
| `99_ASSETS/`    | 画像などのアセット                         |

## 日常の運用ループ

```
┌─────────────┐   /inbox   ┌─────────────┐   質問（ask）
│  00_INBOX   │ ────────►  │  10_WIKI    │ ────────────► 回答（ソース引用付き）
│ (raw素材)   │            │ (知識ノート)│
└─────────────┘            └─────────────┘
      │ 元ファイル                ▲
      └────►  90_ARCHIVES          │ /wiki（Web検索から直接追加）
                                   │ /check（定期メンテ）
```

## コマンド／スキル一覧

| 名前     | 種類            | 役割                                                                       |
| -------- | --------------- | -------------------------------------------------------------------------- |
| `/daily` | command + skill | デイリーノートを添削し、まとめ（Act）を生成                                |
| `/wiki`  | command + skill | Web検索とClaudeの知識でトピックを調査し、1ノートを作成                     |
| `/inbox` | command + skill | `00_INBOX/` の素材を分解して `10_WIKI/` に取り込み、元を `90_ARCHIVES/` へ |
| `/check` | command         | リンク切れ・孤立ノート・張り忘れリンク・矛盾を検出し、承認後に修正         |
| `ask`    | skill（auto）   | 質問時に自動発動。`10_WIKI/` を参照してソース引用付きで回答                |

## Web Clipper の連携

Chrome の [Obsidian Web Clipper](https://chromewebstore.google.com/detail/obsidian-web-clipper/cnjifjpddelmedmihgijeibhnjfabmlf) で記事を `00_INBOX/` に保存できるようにする。

1. 拡張機能を Chrome に追加
2. 紫の宝石アイコン → 歯車（設定）
3. **保管庫** に自分の vault 名を入力
4. **デフォルト** → **ノートの場所** を `00_INBOX` に変更

保存すれば `00_INBOX/` に記事が届く。あとは `/inbox` で取り込む。

## デイリーノートの PDCA ワークフロー

| セクション     | PDCA  | 記入者   | 内容                                                                 |
| -------------- | ----- | -------- | -------------------------------------------------------------------- |
| **今日の目標** | Plan  | ユーザー | 朝に今日やるタスクを箇条書きで記入                                   |
| **今日の成果** | Do    | ユーザー | 夜に実際にやったことを自由形式で記入                                 |
| **ふりかえり** | Check | ユーザー | 目標・成果を照らし合わせ、できたこと・できなかったこと・反省点を記入 |
| **まとめ**     | Act   | AI       | `/daily` 実行時にAIが添削後の内容を読み、コーチのようにコメント      |

## Sync

テンプレートの更新を取り込む。

```bash
git fetch upstream
git merge upstream/main
git push origin main
```

下流で `CLAUDE.md` やスキルを編集している場合、マージ時にコンフリクトが発生することがある。その際は手動で解消してからコミットする。
