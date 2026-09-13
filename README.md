# test-codex

Renovate の更新 PR に Codex Cloud の自動レビューが反応するか確認するリポジトリです。

## 実行

GitHub の Settings → Actions → General で **Allow GitHub Actions to create and approve pull requests** を有効にします。
Actions → Renovate → Run workflow、または次のコマンドで手動実行します。

```sh
gh workflow run renovate.yml --ref main
```

`manifests/nginx.yaml` の `nginx:1.26.0` を、検証用に 1.26 系の新しいパッチへ更新します。
この manifest は PR 検証用で、クラスタへのデプロイは行いません。
定期実行、自動マージは無効です。

## 確認する内容

- Renovate の実行ログと作成された更新 PR。
- PR 上の Codex のレビュー、コメント、リアクション。
- 手動メンションをせず、自動レビューが開始されるか。

認証には `GITHUB_TOKEN` を使うため、PR 作成者は `github-actions[bot]` です。
Renovate GitHub App の `renovate[bot]` や PAT による PR とは条件が異なります。
セキュリティレビューの実行有無は、通常のコードレビューと分けて確認します。
