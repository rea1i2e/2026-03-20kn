# GitHub Actions を使ったデプロイ

テンプレート（t2025-10-01vite）の GitHub Actions ワークフローを使う場合の手順。

---

## 仕組み

- `main` / `master` へのプッシュ → テスト環境へ自動FTPデプロイ
- PR作成・更新 → テスト環境へ自動FTPデプロイ
- GitHub Actions画面から手動実行（`deploy_to_production: true`） → 本番環境へFTPデプロイ

ビルド（`npm run build`）→ `dist/` を FTP転送 の順で動く。

---

## 初回セットアップ

1. `cp env.deploy.example .env.deploy` で `.env.deploy` を作成
2. `.env.deploy` に値を記入

| 変数名 | 内容 |
|---|---|
| `FTP_SERVER` | FTPサーバーのホスト名 |
| `FTP_USERNAME` | FTPユーザー名 |
| `FTP_PASSWORD` | FTPパスワード |
| `TEST_URL` | テスト環境のURL（通知用） |
| `DISCORD_WEBHOOK` | Discord通知用WebhookURL（任意） |

3. `gh auth login` で GitHub CLI 認証
4. `./scripts/setup-secrets.sh` を実行してSecretsを登録

---

## 本番デプロイ

GitHub Actions 画面 → 「Run workflow」→ `deploy_to_production: true` にチェックして実行。

> 注意: 現状のワークフローはテスト環境・本番環境で同じFTP認証情報（`FTP_SERVER` 等）を使っている。
> 本番を別サーバーにする場合は `FTP_SERVER_PROD` 等の別Secretsを追加してワークフローを修正する。

---

## デプロイの確認

- GitHub リポジトリの「Actions」タブでログを確認
- 成功・失敗は Discord に通知される（Webhook設定時）
