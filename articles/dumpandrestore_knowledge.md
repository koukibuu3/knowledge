---
title: "dumpファイルのリストア方法"
emoji: "📝"
type: "tech" # tech: 技術記事 / idea: アイデア
topics: ["dump", "Heroku"]
published: false
---

# dumpファイルのリストア

- DBコンテナとの共有フォルダにdumpファイルを移動

```sh
mv latest.dump .database/
```

- DBコンテナに入る

```sh
dc exec db bash
```

- リストアする

```sh
pg_restore --verbose --clean -U root -d develop /var/lib/postgresql/data/latest.dump
```

参考：https://blog.garbanzo.xyz/Docker_Postgres%E3%81%A7%E3%83%AA%E3%82%B9%E3%83%88%E3%82%A2%E3%81%99%E3%82%8B/



# CSVからHerokuのPostgreSQLにデータ移行

```sh
heroku pg:psql -a <アプリ名>

# CSVファイルの内容を指定したテーブルに書き込む
=>\COPY <テーブル名> FROM '<csvファイル名>' CSV HEADER
# シーケンスを回す
=> SELECT setval('<シーケンス名>',(SELECT max(id) FROM <テーブル名>));
```



