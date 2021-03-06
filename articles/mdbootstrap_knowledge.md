---
title: "MDB - Material Design for Bootstrapã®å°å¥"
emoji: "ð"
type: "tech" # tech: æè¡è¨äº / idea: ã¢ã¤ãã¢
topics: ["MDB", "Bootstrap"]
published: true
---

# Bootstrapã®å°å¥

## npmã®ã¤ã³ã¹ãã¼ã«

```sh
$ yum install epel-release

$ yum install nodejs npm --enablerepo=epel
$ yum install gcc gcc-c++
```

## Laravelã®åç¨®è¨­å®ãã¡ã¤ã«ãå¤æ´

- package.json

```json
"bootstrap-sass": "^3.3.7",
        â
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

## bootstrap4ãã¤ã³ã¹ãã¼ã«

```sh
$ npm install
$ npm install popper.js
```

### ã¨ã©ã¼çºç

### npm run dev ã§ã¨ã©ã¼çºç

1. `package.json` ã® `cross-env` ã `node_modules/cross-env/dist/bin/cross-env.js` ã«å¤æ´
2. `rm -rf node_modules`
3. `rm package-lock.json yarn.lock`
4. `npm cache clear --force`



# MDBã®å°å¥

## éçãã¡ã¤ã«(CSS,JS)ã®éç½®

1. `npm install mdbootstrap` ãå®è¡
2. `npm run dev`ãå®è¡
   - `webpack.mix.js`ã«æ¸ãã¦ããåå®¹ãåã«css/jsãæ¸ãåºã
   - æ¨æºã§ã¯ä¸è¨ã®è¨­å®ãããã¦ãã
     - `resource/js/app.js` => `public/js`
     - `resource/js/app.scss` => `public/css`
   - æ°ããªcss/jsãè¿½å ãããå ´åã¯ãã³ã³ã«è¿½å ãã
3. htmlã«ä¸è¨ã®èª­ã¿è¾¼ã¿å¦çãè¿½å ãã
```html
<link type="text/css" href="{{asset('/css/xxx.css')}}" rel="stylesheet">
```

```html
<script type="text/javascript" src="{{asset('/js/xxx.js')}}"></script>
```

- `npm run dev`ã§æ¸ãåºããã`app.js / app.css`ã¯ãããã`resource/js/app.js`ã`resource/js/app.scss`ãåã«ãã¦ãã

- `resource/js/app.js`ãä¸è¨ã®ããã«ä¿®æ­£ãããã¨ã§ãæ¸ãåºããã`app.js`ãå¤æ´ãããã¨ãã§ããã

```js
require('mdbootstrap/js/mdb');
```

- `resource/js/app.scss`ãä¸è¨ã®ããã«ä¿®æ­£ãããã¨ã§ãæ¸ãåºããã`app.css`ãå¤æ´ãããã¨ãã§ããã

```scss
@import '~mdbootstrap/scss/mdb';
```