# API 設計規約

## エンドポイント命名

- リソースは **複数形の名詞** を使う: `/users`, `/orders`
- アクションは HTTP メソッドで表現する（動詞をパスに含めない）
- バージョニング: `/api/v1/...`

```
GET    /api/v1/users          # 一覧
GET    /api/v1/users/:id      # 単件取得
POST   /api/v1/users          # 作成
PATCH  /api/v1/users/:id      # 部分更新
DELETE /api/v1/users/:id      # 削除
```

## リクエスト / レスポンス形式

- Content-Type: `application/json`
- 日時は **ISO 8601 UTC** (`2024-01-15T09:30:00Z`)
- 空値は `null`（未定義フィールドは省略しない）

### 成功レスポンス

```json
{
  "data": { ... },
  "meta": { "page": 1, "total": 42 }
}
```

### エラーレスポンス

```json
{
  "error": {
    "code": "VALIDATION_ERROR",
    "message": "Human-readable message",
    "details": [ { "field": "email", "issue": "invalid format" } ]
  }
}
```

## HTTP ステータスコード

| 状況 | コード |
|------|--------|
| 作成成功 | 201 |
| 削除成功（ボディなし） | 204 |
| バリデーションエラー | 422 |
| 認証エラー | 401 |
| 認可エラー | 403 |
| リソース不在 | 404 |
| サーバーエラー | 500 |

## 認証

- Bearer トークン: `Authorization: Bearer <token>`
- トークンは **リクエストボディ / URL に含めない**
- <プロジェクト固有の認証方式があれば追記>

## レート制限

- デフォルト: <例: 1000 req/min per IP>
- ヘッダーで残量を返す: `X-RateLimit-Remaining`, `X-RateLimit-Reset`

## バージョン管理・後方互換性

- 破壊的変更は新バージョン (`v2`) に昇格させる。
- 旧バージョンは <例: 6 か月> 間サポートし、Deprecation ヘッダーを付与する。
