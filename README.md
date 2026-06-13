# Obsidian Claude Template

Claude Code で Obsidian Vault を使い、仕事のメモや参考資料を効率的に整理・保管するテンプレート。`00_INBOX/` に素材を放り込み、AI に分解・整理させて `20_NOTES/` に蓄積する。

## できること

- **クリップ**: Web Clipper で記事を `00_INBOX/` に1クリック保存
- **取り込み**: `/ingesting-inbox` で記事を複数ノートに分解し `20_NOTES/` に配置。元記事は `90_ARCHIVES/` に退避
- **執筆**: `/writing-articles` で 20_NOTES を素材にしてバズ構造の技術記事を `30_ARTICLES/` に書き下ろし

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

| フォルダ       | 役割                                          |
| -------------- | --------------------------------------------- |
| `00_INBOX/`    | ソース素材の投げ入れ先                        |
| `10_DAILY/`    | デイリーノート                                |
| `20_NOTES/`    | ツェッテルカステン形式の知識ノート（主役）    |
| `30_ARTICLES/` | 技術記事（外部発信用）                        |
| `90_ARCHIVES/` | `/ingesting-inbox` で取り込み済みのソース素材 |
| `99_ASSETS/`   | 画像などのアセット                            |

## 日常の運用ループ

```
┌─────────────┐   /ingesting-inbox   ┌─────────────┐
│  00_INBOX   │ ────────►  │  20_NOTES   │
│ (raw素材)   │            │ (メモ)      │
└─────────────┘            └─────────────┘
      │ 元ファイル
      └────►  90_ARCHIVES
```

## コマンド／スキル一覧

| 名前                | 種類            | 役割                                                                        |
| ------------------- | --------------- | --------------------------------------------------------------------------- |
| `/ingesting-inbox`  | command + skill | `00_INBOX/` の素材を分解して `20_NOTES/` に取り込み、元を `90_ARCHIVES/` へ |
| `/writing-articles` | command + skill | 技術記事を執筆し `30_ARTICLES/` に保存                                      |

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
