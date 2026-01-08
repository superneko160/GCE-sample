# Laravel GCE Setup

## `.env` ファイルを手動でアップロード

### DBパスワード変更

`.env` ファイルのDBパスワードを設定

```
DB_PASSWORD=xxxxxxx
```

### ファイル所有者＋権限変更

```sh
sudo chown www-data:www-data .env
sudo chmod 600 .env
```

## ログファイル等の所有者＋権限変更

```sh
sudo chown -R www-data:www-data /var/www/html/storage /var/www/html/bootstrap/cache
sudo chmod -R 775 /var/www/html/storage /var/www/html/bootstrap/cache
```

## PHP拡張機能のインストール

```sh
sudo apt-get install -y php8.2-common php8.2-cli php8.2-gd php8.2-curl php8.2-mbstring php8.2-zip php8.2-bcmath php8.2-xml php8.2-mysql
```

## マイグレーション実行

`mysql -u root -p` でログインしてからDB作成

```sql
CREATE DATABASE sampledb CHARACTER SET utf8mb4 COLLATE utf8mb4_unicode_ci;
```

`quit` でターミナルに戻ってからマイグレーションを実行

```sh
php artisan migrate
```

ドライバがない場合、PHPのバージョンに合わせたドライバをインストール

```sh
sudo apt-get install php8.2-mysql -y
```

## ドキュメントルートの変更

Apacheの場合、Apacheの設定ファイル（通常は /etc/apache2/sites-available/000-default.conf など）を編集

- 修正前: `/var/www/html`
- 修正後: `/var/www/html/public`

```conf
<VirtualHost *:80>
    ServerAdmin webmaster@localhost
    # ここを /public に変更
    DocumentRoot /var/www/html/public

    <Directory /var/www/html/public>
        Options Indexes FollowSymLinks
        AllowOverride All
        Require all granted
    </Directory>

    ErrorLog ${APACHE_LOG_DIR}/error.log
    CustomLog ${APACHE_LOG_DIR}/access.log combined
</VirtualHost>
```

> [!IMPORTANT] 修正後、Laravelのルート（URL）を綺麗にするために `sudo a2enmod rewrite` を実行して mod_rewrite を有効にし、Apacheを再起動 `sudo systemctl restart apache2` する
