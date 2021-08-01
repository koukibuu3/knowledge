---
title: "Laravel開発メモ"
emoji: "📝"
type: "tech" # tech: 技術記事 / idea: アイデア
topics: ["Laravel"]
published: false
---

# artisanコマンド

## php artisan migrate





## phpコンテナのDockerfileに以下が必要

```sh
# pdo_pgsqlのインストール
RUN apt-get update && apt-get -y install libpq-dev
RUN docker-php-ext-install pdo_pgsql
```

