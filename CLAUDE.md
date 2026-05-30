# CLAUDE.md

このファイルは Claude Code がリポジトリを開いたときに自動的に読み込まれます。

## プロジェクト概要

- **プロジェクト名**: <プロジェクト名>
- **目的**: <このリポジトリが何をするか 1〜2 文で>
- **オーナー / メインの連絡先**: <名前または GitHub handle>

## 技術スタック

- **言語**: <例: TypeScript 5.x / Python 3.12>
- **ランタイム / フレームワーク**: <例: Node.js 20, React 18>
- **パッケージマネージャ**: <例: pnpm 9 / uv>
- **テストフレームワーク**: <例: Vitest / pytest>
- **主要な依存関係**: <例: zod, drizzle-orm, fastapi>

## ディレクトリ構成（概要）

```
<project-root>/
├── src/          # ソースコード
├── tests/        # テスト
├── docs/         # ドキュメント
└── scripts/      # ユーティリティスクリプト
```

詳細なアーキテクチャは `@docs/architecture.md` を参照。

## よく使うコマンド

```bash
# 依存関係インストール
<例: pnpm install>

# 開発サーバー起動
<例: pnpm dev>

# テスト実行
<例: pnpm test>

# リント / フォーマット
<例: pnpm lint && pnpm format>

# ビルド
<例: pnpm build>
```

## コーディング規約

- コメントは「なぜ」を書く。「何を」はコードが語る。
- 関数は単一責務。100 行を超えたら分割を検討する。
- エラーは握りつぶさない。必ず呼び出し元へ伝播させるか、ログを残す。
- 型は明示する（`any` は原則禁止）。
- <プロジェクト固有の規約があれば追加>

## ブランチ・PR 規約

- `main` は常にデプロイ可能な状態を維持する。
- ブランチ名: `<type>/<short-description>` （例: `feat/user-auth`, `fix/null-check`）
- PR タイトル: Conventional Commits 形式 (`feat:`, `fix:`, `chore:` など)
- レビュー前に CI がグリーンであること。

## 追加ルール（import）

- API 設計規約 → `@.claude/rules/api.md`
- テスト規約 → `@.claude/rules/testing.md`
