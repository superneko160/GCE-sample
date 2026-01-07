# GCE-sample

Deploy to GCE(Google Compute Engine) using Cloud Build.

## Setup

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

