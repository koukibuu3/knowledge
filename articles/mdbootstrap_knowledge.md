---
title: "MDB - Material Design for Bootstrapの導入"
emoji: "📝"
type: "tech" # tech: 技術記事 / idea: アイデア
topics: ["MDB", "Bootstrap"]
published: true
---

# Bootstrapの導入

## npmのインストール

```sh
$ yum install epel-release

$ yum install nodejs npm --enablerepo=epel
$ yum install gcc gcc-c++
```

## Laravelの各種設定ファイルを変更

- package.json

```json
"bootstrap-sass": "^3.3.7",
        ↓
"bootstrap": "^4.0.0",
```

- resources/js/bootstrap.js

```js
try {
    window.$ = window.jQuery = require('jquery');

    // require('bootstrap-sass');
    require('bootstrap');
} catch (e) {}
```

- resources/sass/app.scss

```scss
// Bootstrap
// @import "~bootstrap-sass/assets/stylesheets/bootstrap";
@import "~bootstrap/scss/bootstrap";
```

## bootstrap4をインストール

```sh
$ npm install
$ npm install popper.js
```

### エラー発生

### npm run dev でエラー発生

1. `package.json` の `cross-env` を `node_modules/cross-env/dist/bin/cross-env.js` に変更
2. `rm -rf node_modules`
3. `rm package-lock.json yarn.lock`
4. `npm cache clear --force`



# MDBの導入

## 静的ファイル(CSS,JS)の配置

1. `npm install mdbootstrap` を実行
2. `npm run dev`を実行
   - `webpack.mix.js`に書いてある内容を元にcss/jsを書き出す
   - 標準では下記の設定がされている
     - `resource/js/app.js` => `public/js`
     - `resource/js/app.scss` => `public/css`
   - 新たなcss/jsを追加したい場合は、ココに追加する
3. htmlに下記の読み込み処理を追加する
```html
<link type="text/css" href="{{asset('/css/xxx.css')}}" rel="stylesheet">
```

```html
<script type="text/javascript" src="{{asset('/js/xxx.js')}}"></script>
```

- `npm run dev`で書き出される`app.js / app.css`はそれぞれ`resource/js/app.js`、`resource/js/app.scss`を元にしている

- `resource/js/app.js`を下記のように修正することで、書き出される`app.js`を変更することができる。

```js
require('mdbootstrap/js/mdb');
```

- `resource/js/app.scss`を下記のように修正することで、書き出される`app.css`を変更することができる。

```scss
@import '~mdbootstrap/scss/mdb';
```