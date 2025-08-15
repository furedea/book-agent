# Book Agent Generator (`book-agent`)

> **Language**
> **[English Version](README_en.md)** / **日本語版 README** (このページ)

> [!Warning]
> テスト版なので大幅な変更の可能性があります．

**関連記事**
**[技術書知識を即戦力化！Sub Agent化から設計支援・レビューまでの最短ワークフロー](https://zenn.dev/furedea/articles/53b5117b389454)** - Zenn記事

# 概要

技術書や技術記事のメモ類からClaude CodeのSub Agent定義ファイルを対話的に自動生成するカスタムスラッシュコマンド．

## 主な機能

- 🧠 ナレッジの分析と構造化: 提供されたテキスト（技術書のハイライト，記事メモなど）の主題を分析し，「核となる原則」「主要なテクニック」「アンチパターン」といった構造化されたナレッジベースを自動生成．
- 🤖 Sub Agent定義の自動生成: Claude Codeが直接認識できる，Frontmatter（`name`, `description`等）を含む完全なSub Agent定義ファイル（`.md`）を作成．
- 🗣️ 対話的な生成プロセス: 生成されるエージェント名や内容を下書きとして提示し，ユーザーの承認や修正指示を受け付けながら，対話的に定義ファイルを完成させる（`-y`フラグによる自動承認も可能）．
- 📁 自動ファイル管理: 命名の競合を自動で回避し指定されたディレクトリ（`./.claude/agents/book-agent/`）にファイルを安全に保存．

## インストール & セットアップ

1. このリポジトリをクローンするかダウンロード．
2. プロジェクトの`.claude/commands/`ディレクトリ内にこのリポジトリの`book-agent`ディレクトリを丸ごとコピー．

```
    <あなたのプロジェクト>
    └── .claude/
        └── commands/
            └── book-agent/      <-- ココに配置
                └── book2agent.md
```

3. （推奨）[Zennの記事](https://zenn.dev/link/to/your/article)を参考に，ObsidianとKindle HighlightsやMCP Toolsプラグインをセットアップすると，よりスムーズなワークフローが実現できる．

## 使い方

このコマンドは[Obsidian](https://obsidian.md/)に集約したナレッジソース（技術書のハイライトや記事のメモ）をClaude Codeに連携して使用することを想定している．

### 基本的なワークフロー

1. ナレッジの準備: `Kindle Highlights`や`Web Clipper`といったObsidianプラグインを使い、Sub Agent化したい技術リソースをObsidianノートに集約．
2. コンテキストの連携: Obsidianの`MCP Tools`プラグインを使い、対象のノート内容をClaude Codeのコンテキストとして読み込む．
3. コマンドの実行: コンテキストが読み込まれた状態で、`/book-agent:book2agent`コマンドを実行し，対話形式でSub Agentを生成．

### コマンド実行例

#### 1. Obsidian + MCP連携（推奨）

1. /mcpコマンドでObsidianと接続しアクティブなノートをコンテキストに読み込む
>
> /mcp

2. 引数なしでコマンドを実行する
>
> /book-agent:book2agent {obsidianのpath}

---

#### 2. ファイルからの入力

ObsidianのノートなどをMarkdownファイルとして書き出し直接読み込ませることも可能．
>
> /book-agent:book2agent {path}

---

#### 3. 自動承認モード

生成プロセスでの対話的な確認をスキップし最初から最後まで自動で実行させたい場合は`-y`フラグを使用．
>
> /book-agent:book2agent -y {path}

## ライセンス

このプロジェクトは[MITライセンス](LICENSE)です．

## 貢献

バグ報告や機能改善の提案は，IssueやPull Requestにて歓迎します．
