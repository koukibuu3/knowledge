---
title: "Herokuの開発メモ"
emoji: "📝"
type: "tech" # tech: 技術記事 / idea: アイデア
topics: ["Heroku"]
published: false
---

# コマンド集

- Heroku CLIのインストール

```sh
brew tap heroku/brew && brew install heroku 

# 以下だけでもいいかも
brew install heroku
```

- Herokuへログイン

```sh
heroku login

# ターミナルベースでログインする（毎回ログインしなくてよくなる）
heroku login --interactive
```

- DBコンテナへログイン

```sh
heroku pg:psql -a {アプリ名}
```

- DBのマイグレーション

```sh
heroku run php artisan migrate -a {アプリ名}

# マイグレーションをやり直す場合 危険
heroku run php artisan migrate:refresh --seed -a <アプリ名>
```

- バックアップの定期実行

```sh
heroku pg:backups schedule DATABASE_URL -a {アプリ名}
```

- バックアップデータの確認

```sh
heroku pg:backups -a {アプリ名}
```

- dumpデータの取得

```sh
heroku pg:backups:download {a100とかの番号} -a {アプリ名}
```

- ssh接続

```sh
heroku run bash -a {アプリ名}
```

- 環境変数設定

```sh
heroku config:set {変数名}={値} -a {アプリ名}
```

- リリースバージョンの確認

```sh
heroku releases -a {アプリ名}
```

- バージョンを戻す

```sh
heroku rollback {v10とか}
```



# その他設定

## Review Appsの設定（legacy）

1. REVIEW APPS > Enable Review Appsを押す
2. parent appにstagingのアプリを選択し`Create an app.json File`を押す
3. 後で直接編集すれば良いので、app.jsonの設定値を入力する画面はスルーでOK
4. 今回は下記の様なapp.jsonを用意する

```json
{
    "addons": [
      "heroku-postgresql"
    ],
    "buildpacks": [

    ],
    "description": "review app",
    "env": {
        /* staging環境の環境変数 */
    },
    "formation": {
    },
    "name": "<アプリ名>",
    "scripts": {
      "postdeploy": "php artisan migrate --force"
    },
    "stack": "heroku-18"
  }
```



## Procfileの生成

```
web: vendor/bin/heroku-php-apache2 public/
```

- アプリディレクトリ直下に上記Procfileを生成
- ProcfileはHerokuアプリの起動時に実行されるプロセスを記載する
- ここではApacheの使用の指定と、ドキュメントルートの設定を行う



## 環境変数の設定

以下の手順をstaging環境とproduction環境両方のアプリに対して行う

- DATABASE_URLの値を元に環境変数を設定

```sh
$ heroku config:get DATABASE_URL -a <アプリ名>
postgres://<ユーザ名>:<パスワード>@<ホスト名>:5432/<DB名>
```

- 設定内容の確認

```sh
$ heroku config -a <アプリ名>
=== <アプリ名> Config Vars
APP_KEY:       <APPキー>
DB_CONNECTION: <DB種類>
DB_DATABASE:   <DB名>
DB_HOST:       <ホスト名>
DB_PASSWORD:   <アプリ名>
DB_USERNAME:   <ユーザ名>
```



## CSVからPostgreSQLにデータを移行

```sh
heroku pg:psql -a <アプリ名>

# CSVファイルの内容を指定したテーブルに書き込む
=>\COPY <テーブル名> FROM '<csvファイル名>' CSV HEADER
# シーケンスを回す
=> SELECT setval('<シーケンス名>',(SELECT max(id) FROM <テーブル名>));
```
