# GCE-sample

Deploy to GCE(Google Compute Engine) using Cloud Build.

## Setup

Cloud Buildでトリガーを作成。作成時、GitHubのリポジトリを紐づける

### トリガー作成時に、「特定のブランチ（main）のみデプロイを実行する」ように制御

1. Google Cloud Console の [Cloud Build > トリガー] に移動
2. 対象のトリガーを選択（または作成）
3. 「イベント」 で ブランチにプッシュする を選択
4. 「ソース」 の 「ブランチ」 欄に `^main$` と入力（正規表現でmainのみに限定）

### IAM

以下のロールをIAMに追加

- Cloud Build 編集者
- Compute インスタンス管理者 (v1)
- サービス アカウント ユーザー

### Permission

```sh
# 1. 公開ディレクトリの所有者を自分（ログイン中のユーザ）に変更
sudo chown -R $USER:$USER /var/www/html/
# 2. 書き込み権限を付与
sudo chmod -R 755 /var/www/html/
```

