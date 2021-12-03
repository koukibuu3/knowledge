---
title: "phpenvに入門する phpenv/anyenv"
emoji: "📝"
type: "tech" # tech: 技術記事 / idea: アイデア
topics: ["phpenv", "anyenv"]
published: true
---

# 概要

https://zenn.dev/koukibuu3/articles/nodeenv_knowledge

で anyenv に入門したので、今度は anyenv 管理の phpenv を使うようにしてみる。



# brewでインストールしていたPHPを削除

```sh
brew uninstall php

rm -rf /opt/homebrew/etc/php
```



# phpenv と phpbuild をインストール

```sh
anyenv install phpenv
```



# 動作に必要なパッケージのインストール

```sh
brew install curl autoconf bzip2 icu4c krb5 libedit libiconv libjpeg libpng libxml2 libzip oniguruma openssl@1.1 pkg-config tidy-html5 gcc re2c bison openssl zlib
```



# 環境変数の設定

```sh
# .zshrc

## phpenv
export PATH="/opt/homebrew/opt/bison/bin:$PATH"
export PATH="/opt/homebrew/opt/libxml2/bin:$PATH"
export PATH="/opt/homebrew/opt/bzip2/bin:$PATH"
export PATH="/opt/homebrew/opt/curl/bin:$PATH"
export PATH="/opt/homebrew/opt/libiconv/bin:$PATH"
export PATH="/opt/homebrew/opt/krb5/bin:$PATH"
export PATH="/opt/homebrew/opt/openssl@1.1/bin:$PATH"
export PATH="/opt/homebrew/opt/icu4c/bin:$PATH"
export PATH="/opt/homebrew/opt/tidy-html5/lib:$PATH"
export PKG_CONFIG_PATH="/opt/homebrew/opt/krb5/lib/pkgconfig:$PKG_CONFIG_PATH"
export PKG_CONFIG_PATH="/opt/homebrew/opt/icu4c/lib/pkgconfig:$PKG_CONFIG_PATH"
export PKG_CONFIG_PATH="/opt/homebrew/opt/libedit/lib/pkgconfig:$PKG_CONFIG_PATH"
export PKG_CONFIG_PATH="/opt/homebrew/opt/libjpeg/lib/pkgconfig:$PKG_CONFIG_PATH"
export PKG_CONFIG_PATH="/opt/homebrew/opt/libpng/lib/pkgconfig:$PKG_CONFIG_PATH"
export PKG_CONFIG_PATH="/opt/homebrew/opt/libxml2/lib/pkgconfig:$PKG_CONFIG_PATH"
export PKG_CONFIG_PATH="/opt/homebrew/opt/libzip/lib/pkgconfig:$PKG_CONFIG_PATH"
export PKG_CONFIG_PATH="/opt/homebrew/opt/oniguruma/lib/pkgconfig:$PKG_CONFIG_PATH"
export PKG_CONFIG_PATH="/opt/homebrew/opt/openssl@1.1/lib/pkgconfig:$PKG_CONFIG_PATH"
export PKG_CONFIG_PATH="/opt/homebrew/opt/tidy-html5/lib/pkgconfig:$PKG_CONFIG_PATH"
export PHP_RPATHS="/opt/homebrew/opt/zlib/lib /opt/homebrew/opt/bzip2/lib /opt/homebrew/opt/curl/lib /opt/homebrew/opt/libiconv/lib /opt/homebrew/opt/libedit/lib"
export PHP_BUILD_CONFIGURE_OPTS="--with-bz2=$(brew --prefix bzip2) --with-iconv=$(brew --prefix libiconv) --with-tidy=$(brew --prefix tidy-html5) --with-external-pcre=$(brew --prefix pcre2) --with-zip --enable-intl --with-pear"
```



# PHPのインストール

```sh
phpenv install 8.1.0

# バージョン切り替え
phpenv global 8.1.0

# 特定のディレクトリでのみのバージョン指定
phpenv local 8.1.0

# 更新
phpenv rehash
```

