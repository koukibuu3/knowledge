---
title: "Flutterの開発環境構築メモ"
emoji: "📝"
type: "tech" # tech: 技術記事 / idea: アイデア
topics: ["flutter", "AndroidStudio", "Xcode"]
published: false
---

# Flutterのインストール

- インストール

```sh
brew install flutter
```



# Android Studio の設定

- インストール

```sh
brew install android-studio
```

- Configure > Plugins から `Flutter`を検索してインストール
- Configure > SDK Manager > SDK Tools から `Android SDK Command-line Tools`をインストール
- Android SDKのライセンスを認証

```sh
flutter doctor --android-licenses
```

- 連携できたかチェック

```sh
flutter doctor

Doctor summary (to see all details, run flutter doctor -v):
[✓] Flutter (Channel stable, 2.2.3, on macOS 11.4 20F71 darwin-arm, locale
    ja-JP)
[✓] Android toolchain - develop for Android devices (Android SDK version
    30.0.3)
```



## XCode の設定

- cocoapodsを入れる

```sh
brew install cocoapods
```

- これは必要なのか？

```sh
sudo xcode-select --switch /Application/XCode.app
```

- XCodeのライセンスを認証

```sh
 sudo xcodebuild -license
```

