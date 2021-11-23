---
title: "nodebrewからnodenvに浮気する"
emoji: "📝"
type: "tech" # tech: 技術記事 / idea: アイデア
topics: ["nodenv", "anyenv", "node"]
published: true
---

# 概要

nodenv は異なるバージョンのNode.js を管理することができるバージョンマネージャ

nvm やnodebrew というのもあり、導入が簡単なのでnodebrew を使っていたが `.node-version`によるバージョンの切り替えを使いたくて今回nodenvに浮気することになった



# anyenvとnodenvをインストール

色んな○○env を管理してくれる（phpenvも出来るのかな、今度やってみる）

```sh
brew install anyenv
echo 'eval "$(anyenv init -)"' >> ~/.zshrc  # zshの場合
source .zshrc

anyenv install --init
anyenv install nodenv
source .zshrc
```



# anyenvとnodenv用プラグインをインストール

○○envをまとめてアップデートできるanyenvプラグイン `anyenv-update`

```sh
mkdir -p $(anyenv root)/plugins
git clone https://github.com/znz/anyenv-update.git $(anyenv root)/plugins/anyenv-update
```



npmインストール時にデフォルトでインストールするパッケージを指定できるnodenvプラグイン `nodenv-default-packages`

```sh
mkdir $(nodenv root)/plugins
git clone https://github.com/nodenv/nodenv-default-packages.git $(nodenv root)/plugins/nodenv-default-packages
touch $(nodenv root)/default-packages
```



default-packages の例

```
tarn
typescript
ts-node
typesync
```



# Nodeのインストール

```sh
nodenv install -l
nodenv install {バージョン番号}
nodenv global {バージョン番号}
```



以下の場合ディレクトリ内に `.node-version` が作られる

```sh
noenv local {バージョン番号}
```



# nodebrew の削除

nodenrew でインストールしたNodeを削除する

```sh
nodebrew ls
nodebrew uninstall {バージョン番号}
```

nodebrew のアンインストール

```sh
homebrew uninstall nodebrew
```

設定ディレクトリの削除

```sh
rm -rf ~/.nodebrew
```



