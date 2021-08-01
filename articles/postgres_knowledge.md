---
title: "postgresコンテナを作る上でのメモ"
emoji: "📝"
type: "tech" # tech: 技術記事 / idea: アイデア
topics: ["Postgres", "Docker"]
published: false
---



docker-compose.yml

```yml
    environment:
      POSTGRES_DB: $DB_DATABASE
      POSTGRES_USER: $DB_USERNAME
      POSTGRES_PASSWORD: $DB_PASSWORD
```

上記の指定をしておくと、初回imageビルド時に指定したテーブルとユーザーが作られる
