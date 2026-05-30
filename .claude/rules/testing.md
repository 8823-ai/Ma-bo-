# テスト規約

## 基本方針

- テストは **仕様のドキュメント** として書く。実装の詳細ではなく振る舞いを検証する。
- 1 テスト = 1 アサーション（論理的に）。複数アサーションは意味のまとまりがある場合のみ。
- テストが壊れたら、まずテストを直さずにプロダクションコードを修正する。

## ディレクトリ構成

```
tests/
├── unit/        # 単体テスト（外部依存なし）
├── integration/ # 統合テスト（DB・外部サービス）
└── e2e/         # E2E テスト
```

テストファイルはソースと同階層に置く場合は `*.test.ts` / `*.spec.ts` で命名する。

## テスト命名

```
<対象>_<状況>_<期待結果>
```

例:

```ts
it("createUser_withDuplicateEmail_throwsConflictError", ...)
it("calculateTax_whenRateIsZero_returnsOriginalPrice", ...)
```

## AAA パターン

```ts
it("...", () => {
  // Arrange
  const user = buildUser({ role: "admin" });

  // Act
  const result = canDeletePost(user, post);

  // Assert
  expect(result).toBe(true);
});
```

## モック・スタブ

- 外部 I/O（HTTP, DB, FS）は必ずモックする。
- モックは **テストファイル内** に閉じ込める（グローバルモックは原則禁止）。
- `jest.spyOn` よりも依存性注入を優先する。

## フィクスチャ / ファクトリ

- テストデータは `tests/factories/` にファクトリ関数として定義する。
- デフォルト値を持たせ、必要なフィールドだけオーバーライドする。

```ts
export const buildUser = (overrides = {}): User => ({
  id: "user-1",
  email: "test@example.com",
  role: "member",
  ...overrides,
});
```

## カバレッジ

- ライン / ブランチカバレッジの目標: <例: 80%>
- カバレッジを上げるためだけのテストは書かない。意味のあるケースを優先する。

## CI での実行

```bash
# ユニットテストのみ（高速）
<例: pnpm test:unit>

# 全テスト（CI 用）
<例: pnpm test:ci>
```

CI では必ず全テストがグリーンであることを確認してからマージする。
