---
title: "ReactNativeの開発環境を構築する"
emoji: "📝"
type: "tech" # tech: 技術記事 / idea: アイデア
topics: ["ReactNative"]
published: false
---

# 初期構築

## 必要なパッケージをインストール

```sh
brew install watchman
npm install -g react-native-cli
```



## ReactNativeアプリケーションを作成

```sh
react-native init <アプリ名>
? CocoaPods (https://cocoapods.org/) is not installed. CocoaPods is necessary for the iOS project to run correctly. Do you 
want to install it?
○ Yes, with Gem
● Yes, with Homebrew
```



### cocoapodsのインストールに失敗した場合

- 以下エラーが発生する場合あり

```sh
The formula built, but is not symlinked into /usr/local
Could not symlink bin/pod
Target /usr/local/bin/pod
already exists. You may want to remove it:
rm '/usr/local/bin/pod'

To force the link and overwrite all conflicting files:
brew link --overwrite cocoapods

To list all files that would be deleted:
brew link --overwrite --dry-run cocoapods
```



- `brew doctor`で見てみても下記のようなWarningが確認できる

```sh
$ brew doctor
Warning: You have unlinked kegs in your Cellar.
Leaving kegs unlinked can lead to build-trouble and cause brews that depend on
those kegs to fail to run properly once built. Run `brew link` on these:
  cocoapods
```



- cocoapodsのリンクが作成出来ていないようなので、指示にしたがって作成する

~~よく分からないけれど強制的に上書きしてしまう~~

```sh
brew link --overwrite cocoapods
```



- cocopodsによるライブラリのインストールに失敗しているはず（以下エラーが発生）

```sh
(node:6594) UnhandledPromiseRejectionWarning: Error: Failed to install CocoaPods dependencies for iOS project, which is required by this template.
Please try again manually: "cd ./<アプリ名>/ios && pod install".
```



- なので、これも指示にしたがってインストールを実行する

```sh
cd <アプリ名>/ios
pod install
```



※ あらかじめHomebrewでcocoapodsをインストールしている場合は発生しないかも



# ビルド

```sh
react-native run-ios

or

npx react-native run-ios
```

## Ctrl + R でリロード

これが必要な場合もある

```sh
ln -s $(which node) /usr/local/bin/node
```



# パッケージの導入

## eslintの導入

```sh
npm install --save-dev eslint

./node_modules/.bin/eslint --init

? How would you like to use ESLint? To check syntax and find problems
? What type of modules does your project use? JavaScript modules (import/export)
? Which framework does your project use? React
? Does your project use TypeScript? No
? Where does your code run? Browser
? What format do you want your config file to be in? JSON
The config that you've selected requires the following dependencies:
```



## react-navigationの導入

```sh
npm install react-navigation

# 参考：https://qiita.com/zaburo/items/81c39f73216e87f443ea
npm install react-native-gesture-handler react-native-reanimated
cd ios
pod install
```

- ex.) screens/Home.js

```javascript
import React from 'react';
import {View, Text, Button} from 'react-native';

export default class Home extends React.Component {
  render() {
    return (
      <View style={{flex: 1, justifyContent: 'center', alignItems: 'center'}}>
        <Text>Home</Text>
      </View>
    );
  }
}

```

- ex.) App.js

```javascript
import React from 'react';

import {createAppContainer} from 'react-navigation';
import {createBottomTabNavigator} from 'react-navigation-tabs';

// import screens
import Home from './screens/Home';
import List from './screens/List';

// Tab
const Tab = createBottomTabNavigator({
  Home: {screen: Home},
  List: {screen: List},
});

export default class App extends React.Component {
  render() {
    const Layout = createAppContainer(Tab);
    return <Layout />;
  }
}

```



### どうやら古いらしい

- 以下コマンドが必要

```sh
npm install react-navigation-stack @react-native-community/masked-view react-native-safe-area-context
npm install react-native-screens
```



## native-baseの導入

```sh
$ npm install native-base
$ react-native link
```

- ex.) Home.js

```javascript
import React from 'react';

import {Container, Header, Left, Body, Right, Button, Icon, Title} from 'native-base';

export default class Home extends React.Component {
  render() {
    return (
      <Container>
        <Header>
          <Left>
            <Button transparent>
              <Icon name="arrow-back" />
            </Button>
          </Left>
          <Body>
            <Title>タイトル</Title>
          </Body>
          <Right>
            <Button transparent>
              <Icon name="menu" />
            </Button>
          </Right>
        </Header>
      </Container>
    );
  }
}

```



## react-native-firebaseの導入

### バンドルIDを設定

ex. ) com.sample.{アプリ名}



### Firebaseのプロジェクトにアプリを追加

1. iOSアプリに設定したバンドルIDを設定
2. App Store ID は後で設定する
3. 設定ファイル（GoogleService-Info.plist）をダウンロードする
4. `iOS/{プロジェクト名}` 直下にGoogleService-Info.plistを配置する
   - 上手くいかなかった場合は、xcodeから配置してみる



```sh
$ npm install react-native-firebase
```



### Podfileに以下を追加

```makefile
pod 'Firebase/Core'
pod 'Firebase/Firestore'  # Firestoreを使いたいのでこれも追加
```



### AppDelegate.hに以下を追加

```objective-c
@import Firebase;  // ←追加
```



### AppDelegate.mに以下を追加

```objective-c
- (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions
{
  [FIRApp configure]; // ←追加
  ...
}
```



```sh
$ cd ios
$ pod install
```



## react-native-modal-datetime-pickerの導入

```sh
npm install react-native-modal-datetime-picker
```



# 実機デバッグ

```sh
$ npm install -g ios-deploy
$ react-native run-ios --device {デバイス名}
```
