---
title: "postgresコンテナを作る上でのメモ"
emoji: "📝"
type: "tech" # tech: 技術記事 / idea: アイデア
topics: ["Postgres", "Docker"]
published: true
---

# docker-compose.yml

```yml
    environment:
      POSTGRES_DB: $DB_DATABASE
      POSTGRES_USER: $DB_USERNAME
      POSTGRES_PASSWORD: $DB_PASSWORD
```

上記の指定をしておくと、起動時に指定したテーブルとユーザーが作られる

指定がない場合は、postgresユーザーが作られる



### コマンド

- データベースコンテナからデータベースへログイン

```sh
psql {$DB_DATABASE} -U {$DB_USERNAME}
```



- ローカルからデータベースへログイン

```sh
psql -h localhost -p 5432 -U {$DB_USERNAME}
```



※ 接続先DB名とユーザ名が同じとき、DB名は省略できる

