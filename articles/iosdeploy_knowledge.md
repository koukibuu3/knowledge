---
title: "iOSアプリを実機にインストールする"
emoji: "📝"
type: "tech" # tech: 技術記事 / idea: アイデア
topics: ["iOS", "XCode"]
published: false
---

# CSRファイルの生成

キーチェーンアクセスで作成する

1. キーチェーンアクセス > 証明書アシスタント > 認証曲に証明書を要求…
2. ユーザーのメールアドレスに任意の値を入力
3. 通称に任意の値を入力（管理しやすい名前を付ける）
4. ディスクに保存を選択



# 証明書（Certificates）の生成

Apple Developperで作成する

1. Certificates, Identifiers & Profiles を選択
2. 種類は App Store and Ad Hoc を選択
3. キーチェーンアクセスで作成したCSRファイルをアップロードする
4. 配布用証明書( iOS Distribution Certificate ) をダウンロードする



# 証明書（Certificates）の読み込み

キーチェーンアクセスで証明書を読み込む

1. ファイル > 読み込む… を選択
2. Apple Developperで作成した証明書（ios_distribution.cer）を読み込む



# App ID作成

1. Identifiers を選択
2. App IDs を選択
3. Description と Bundle ID を入力



# Profileの作成

1. Profiles を選択
2. 証明書を選択
3. 対象のdeviceを選択



# アーカイブを作成

xcode で作成する

1. Product > Archive を選択して実行



# IPAファイルの作成

Organizerで作成する

1. アプリを選択し、Exportを選択する
2. Save for Ad Hoc Deployment を選択する
3. Apple IDを選択し、chooseを押下
4. Nextを押していく



# 実機インストール

Apple Configurator 2で作業する

1. iPhoneをMacに接続する
2. IPAファイルをデバイスにドラッグ&ドロップする