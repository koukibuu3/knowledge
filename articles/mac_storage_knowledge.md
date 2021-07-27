---
title: "Macのストレージを空ける"
emoji: "📝"
type: "tech" # tech: 技術記事 / idea: アイデア
topics: ["Mac"]
published: true
---

# iOS Simulator関連の削除

```sh
# シミュレーターの一覧表示
xcrun simctl list devices

# 使えないシミュレーターを削除
xcrun simctl delete unavailable

# キャッシュの削除
xcrun --kill-cache
```



# coreSimulator/casheの削除

```sh
rm -rf ~/Library/Developer/CoreSimulator/Caches/*
```



# DerivedDataの削除

```sh
rm -rf ~/Library/Developer/Xcode/DerivedData/*
```



#  iOS DeviceSupportの削除

```sh
rm -rf ~/Library/Developer/Xcode/iOS\ DeviceSupport/{要らないver.}
```



# Library/Cachesの削除

```sh
rm -rf ~/Library/Caches/*
```



# safariのキャッシュ削除

- safari > 開発 > キャッシュをクリアにする