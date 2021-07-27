---
title: "Herokuのよく使うコマンド集"
emoji: "📝"
type: "tech" # tech: 技術記事 / idea: アイデア
topics: ["Heroku"]
published: true
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
