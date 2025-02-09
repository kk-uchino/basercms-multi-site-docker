# basercms-multi-site-docker

## 概要

同時に複数の baserCMS の開発環境を起動することができる Docker です。

利用可能な PHP のバージョン: 5.6, 7.2, 7.4, 8.0, 8.1, 8.2, 8.3, 8.4  
利用可能な MySQL のバージョン: 5.7, 8.0, 8.4

## 環境構築

### リポジトリをクローンする

```
git clone https://github.com/kk-uchino/basercms-multi-site-docker.git
```

### vhosts.conf.example から vhosts.conf を作成する

```
cp apache/conf/httpd-vhosts.conf.example apache/conf/httpd-vhosts.conf
```

### Docker を起動する

```
docker compose up -d
```

## アクセス情報

### DB

| VERSION   | HOST    | PORT | USER | PASSWORD |
| --------- | ------- | ---- | ---- | -------- |
| MySQL 5.7 | mysql57 | 3306 | root | root     |
| MySQL 8.0 | mysql80 | 3306 | root | root     |
| MySQL 8.2 | mysql82 | 3306 | root | root     |

### phpMyAdmin

| URL                   |
| --------------------- |
| http://localhost:8080 |

### Mailpit

| PROTOCOL | PORT | URL                   |
| -------- | ---- | --------------------- |
| SMTP     | 1025 | -                     |
| HTTP     | 8025 | http://localhost:8025 |

## サイトを追加する

### VirtualHost を追加する

vhosts.conf を以下のように編集する。

( example.localhost を PHP8.2 で動作させるサンプル)

```
<VirtualHost *:443>
    DocumentRoot "/var/www/html/example"
    ServerName example.localhost

    # ログの出力先を指定する
    ErrorLog /usr/local/apache2/logs/example.localhost_error.log
    CustomLog /usr/local/apache2/logs/example.localhost_access.log combined

    # PHPのバージョンを指定する
    <FilesMatch \.php$>
        SetHandler "proxy:fcgi://php82-fpm:9000"
    </FilesMatch>
</VirtualHost>
```

### Apache を再起動する

```
docker exec basercms-multi-site-apache httpd -k restart
```

## Visual Studio Code でデバッグする

プロジェクトを VSCode で開き、.vscode/launch.json を下記の内容で作成してください。  
`{PROJECT_DIR}` は、プロジェクトのディレクトリ名に書き換えてください。

```
{
    "version": "0.2.0",
    "configurations": [
        {
            "name": "Listen for Xdebug",
            "type": "php",
            "request": "launch",
            "port": 9003,
            "pathMappings": {
                "/var/www/html/{PROJECT_DIR}": "${workspaceRoot}"
            }
        }
    ]
}
```
