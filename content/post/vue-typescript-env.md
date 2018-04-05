+++
title = "Vue.jsをTypeScriptで書ける環境を作る"
description = "Vue.jsを触ることになり、更にTypeScriptで書く事にもなったので、その環境を作ってみた"
date = 2018-04-02T03:40:16+09:00
image = ""
tags = ["JavaScript", "TypeScript", "Vue.js"]
categories = ["クリエイティブ"]
draft = false
+++



## はじめに
最近Vue.jsやるかもな雰囲気が出てきていたので先行して触ってる。  
更にTypeScriptも使うっていう話しを聞いたので、Vue.jsのプロジェクトでTypeScriptを使う方法を調べながらやってみた。

## 環境

- Vue-CLI v3.0.0-beta.6
- Vue.js v2.5.2
- TypeScript v2.8.1

- VisualStudio Code 1.21.1

## プロジェクトの雛形を作成する

Vue.jsには[Vue-CLI](https://github.com/vuejs/vue-cli)というCLLIツールがあって、プロジェクトの雛形が作成出来るらしいのでこれで作成。

```
$ npm install -g @vue/cli
# or
$ yarn global add @vue/cli
```

雛形を作る上で、テンプレートが幾つかあるらしく、webpackの物を使ってみた。

```
$ vue init webpack project-name
```

対話形式で幾つか聞かれるので、答えていくとCLIがプロジェクトを生成してくれる。  
CLIツールあると初回のセットアップが楽でいいね。(あとで設定いじるのつらいけど)


## TypeScript を使えるようにする
Vue-CLIの[Configuration](https://github.com/vuejs/vue-cli/blob/dev/docs/README.md#configuration)にpluginがあるような記述があって読んでいたんだけど、どう使うのかよく分からず(npm installしてもあれがないこれがないってめっちゃ言われてなんか不安になった)

以下の記事を参考にして進めた。

1.  [VueJS+TypeScript の開発環境を作ってみた - IT探検記](http://itexplorer.hateblo.jp/entry/20170807-vuejs-typescript-dev-env)
2.  [vue-cliを使ってとにかく楽してVue.jsでTypeScriptを使いたい | Black Everyday Company](https://kuroeveryday.blogspot.jp/2017/09/how-to-use-vuejs-with-typescript.html)

特に上が良かったかな。

1. TypeScriptで必要なモジュールをインストール
```
$ npm i -D typescript ts-loader@3.5.0
```

2. Vue.jsが提供している[公式型宣言](https://github.com/vuejs/vue/tree/dev/types)を元に、 ``src/types/index.d.ts`` を作成

3. Vue-CLIが生成した雛形をTypeScriptに対応した記述に書き換えていく

というのがざっくりとした流れ。  
3でどこを書き換えるのかは上であげた1の記事を参考にしてください。

### 補足
ts-loaderで3.5.0を入れたのは、最新版を入れると以下のエラーが出たから。

```
Module build failed: TypeError: Cannot read property 'afterCompile' of undefined
```

これで検索すると、ts-loader のリポジトリに [issue](https://github.com/TypeStrong/ts-loader/issues/729) が立っていて、

> ts-loader がwebpack4系を意識したバージョンが入っているのが問題だから、webpack4を使わないでv3を使うなら ts-loader v3.5.0 を入れてみて

っていうコメントがあったので、入れてみたら無事動きました。今の所問題ない印象。
webpack v4が出てからまだ日が浅いからVue-CLI側のテンプレートがまだv3なのかな。

## おまけ: VisualStudio Codeの設定

TypeScriptのSyntaxなんかは入っていたのですが、 [Vetur](https://github.com/vuejs/vetur) という拡張機能がいいみたいでこれも入れてみました。
入れる前にコードを書いていないのでどうなのかは分かりませんが、Vueコンポーネントの ``<script lang="ts">`` 内でちゃんとTypeScriptが書けてる。いい感じに補完してくれる気がする。

## やってみて
環境作るのは毎度どこかで詰まって頭を抱えていますが、Vue-CLIでだいぶ助けられたかなという印象。
ただ、TypeScriptのVue-CLIプラグイン？は結局よく分かっていないので、また少し調べます。

あと、最近Javaやったのもあってか型いいかもしれないってなってきてるので、このままTypeScript触っていこう。
