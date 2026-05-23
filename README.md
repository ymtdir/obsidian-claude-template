# Obsidian Claude Template

Claude Code で Obsidian Vault を**第二の脳**として運用するためのテンプレート。ブックマークしっぱなしの記事や読書メモを `00_INBOX/` に放り込み、AI に分解・整理・リンク付けさせる。質問すれば vault の蓄積から答える。

## できること

- **クリップ**: Web Clipper で記事を `00_INBOX/` に1クリック保存
- **取り込み**: `/ingesting-inbox` で記事を複数ノートに分解し `10_WIKI/` に配置。元記事は `90_ARCHIVES/` に退避
- **翻訳**: `/translating-articles` で海外記事を要約・翻訳して `40_TRANSLATIONS/` に保存
- **調査**: `/researching-wiki <トピック>` で Web検索しながらノート作成
- **問い合わせ**: 質問すると vault を参照してソース引用付きで回答（`asking-wiki` スキルが auto-invoke）
- **執筆**: `/writing-articles` で 10_WIKI を素材にしてバズ構造の技術記事を `50_ARTICLES/` に書き下ろし
- **リンク修繕**: `/relinking-wiki` で 10_WIKI のリンク切れ・張り忘れリンクを定期的に検出して張り直す（孤立ノート・矛盾も副次的に検出）

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

| フォルダ           | 役割                                          |
| ------------------ | --------------------------------------------- |
| `00_INBOX/`        | ソース素材の投げ入れ先                        |
| `10_WIKI/`         | ツェッテルカステン形式の知識ノート（主役）    |
| `20_DAILY/`        | デイリーノート                                |
| `30_DOCUMENTS/`    | 共有用ドキュメント                            |
| `40_TRANSLATIONS/` | 海外記事の翻訳・要約                          |
| `50_ARTICLES/`     | 技術記事（外部発信用）                        |
| `90_ARCHIVES/`     | `/ingesting-inbox` で取り込み済みのソース素材 |
| `99_ASSETS/`       | 画像などのアセット                            |

## 日常の運用ループ

```
┌─────────────┐   /ingesting-inbox   ┌─────────────┐   質問（asking-wiki）
│  00_INBOX   │ ────────►  │  10_WIKI    │ ────────────► 回答（ソース引用付き）
│ (raw素材)   │            │ (知識ノート)│
└─────────────┘            └─────────────┘
      │ 元ファイル                ▲
      └────►  90_ARCHIVES          │ /researching-wiki（Web検索から直接追加）
                                   │ /relinking-wiki（定期メンテ）
```

## コマンド／スキル一覧

| 名前                    | 種類            | 役割                                                                       |
| ----------------------- | --------------- | -------------------------------------------------------------------------- |
| `/researching-wiki`     | command + skill | Web検索とClaudeの知識でトピックを調査し、1ノートを作成                     |
| `/ingesting-inbox`      | command + skill | `00_INBOX/` の素材を分解して `10_WIKI/` に取り込み、元を `90_ARCHIVES/` へ |
| `/translating-articles` | command + skill | 海外記事を要約・翻訳して `40_TRANSLATIONS/` に保存                         |
| `/writing-articles`     | command + skill | 技術記事を執筆し `50_ARTICLES/` に保存                                     |
| `/relinking-wiki`       | command + skill | リンク切れ・張り忘れリンクを検出して張り直す（孤立ノート・矛盾も副次検出） |
| `asking-wiki`   | skill（auto）   | 質問時に自動発動。`10_WIKI/` を参照してソース引用付きで回答                |

## Web Clipper の連携

Chrome の [Obsidian Web Clipper](https://chromewebstore.google.com/detail/obsidian-web-clipper/cnjifjpddelmedmihgijeibhnjfabmlf) で記事を `00_INBOX/` に保存できるようにする。

1. 拡張機能を Chrome に追加
2. 紫の宝石アイコン → 歯車（設定）
3. **保管庫** に自分の vault 名を入力
4. **デフォルト** → **ノートの場所** を `00_INBOX` に変更

保存すれば `00_INBOX/` に記事が届く。あとは `/ingesting-inbox` で取り込む。

## Sync

テンプレートの更新を取り込む。

```bash
git fetch upstream
git merge upstream/main
git push origin main
```

下流で `CLAUDE.md` やスキルを編集している場合、マージ時にコンフリクトが発生することがある。その際は手動で解消してからコミットする。
