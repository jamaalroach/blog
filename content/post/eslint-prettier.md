+++
title = "ESLintとPrettierを触って導入してみた"
description = "ESLintは前から導入していたのですが、最近作っているものに対してLintやFormatをかけてみようと思ったため、ちゃんと使いつつPrettierを入れてFormatをかけてみた"
data = 2018-03-16T01:52:21+09:00
image = ""
categories = ["クリエイティブ"]
tags = ["ESLint", "Prettier"]
author = "Daisuke Konishi"
+++

最近ちょこちょこものづくりをしていて、触るリストに溜まっていたものを少しずつ消費しているのですが、今回はESLintとPrettierを触ってみました。

## 環境とか

- Node.js v8.8.1
- [ESLint](https://eslint.org/) v4.18.2
- [Prettier](https://prettier.io/) v1.11.1


```
$ npm i --save-dev eslint prettier eslint-plugin-prettier eslint-config-prettier
```

Standard.jsを使う場合は以下も。

```
$ eslint-config-standard eslint-plugin-standard eslint-plugin-promise eslint-plugin-import eslint-plugin-node
```

## 設定してみる
やり方がいろいろ有るようなのですが、設定ファイルを増やしたくないので、既にあった ``.eslintrc.json`` に設定を追加しました。

```
{
  "extends": ["standard", "prettier"],
  "plugins": ["prettier"],
  "rules": {
    "prettier/prettier": [
      "error",
      {
        "singleQuote": true,
        "semi": false
      }
    ]
  }
}
```

最近はStandard.jsを主に使っているので、それをベースに。
ESLintに書いておくことで、Prettierを走らせた後にESLintを走らせる事ができるようです。

設定ファイルを書いた後は、 ``package.json`` の scripts に以下を書いておく事で簡単に使えるようになります。

```
"scripts": {
  "lint": "./node_modules/.bin/eslint src/**/*.js",
  "lint:fix": "./node_modules/.bin/eslint src/**/*.js --fix",
}
```

```
$ npm run lint
$ npm run lint:fix
```

## もっと便利に使う
Linterって意識して使わないと使うのを忘れてしまう可能性が高い気がします。なので、自動化してしまうとその辺りを解決しつつ、より便利に使えるようになる気がします。

### エディタでファイルを保存時にLinterが走るようにする

普段VSCodeを使っているのですが、ESLintのパッケージを入れて、ユーザー設定(⌘+,)に以下を追加することで自動でLintが走って .eslintrc を元に修正してくれます。

```
"eslint.autoFixOnSave": true,
```

これが割と便利だなーと思うのですが、エディタによって差異が出るのもよくないので、git のcommit時にLintを走らせるのも手です。この辺は好みで。

## 参考にしたもの

- [ESLint(あるいはTSLint)とPrettierを併用する](http://tech-1natsu.hatenablog.com/entry/2018/01/07/154941)
- [コミット前に Lint を強制するなら lint-staged が便利](https://qiita.com/ybiquitous/items/553479cfcb2cee124ae0)

1個目がかなり参考になりました。今回はこれに沿って書いていったので詳しい説明は1個目を参照してください。
