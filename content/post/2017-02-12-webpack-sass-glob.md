---
title: webpackでディレクトリ内のSassファイルをワイルドカードで指定してコンパイルできるようにする
author: コニタン
type: post
date: 2017-02-12T13:54:28+00:00
url: /archives/2044
wordtwit_post_info:
  - 'O:8:"stdClass":13:{s:6:"manual";b:0;s:11:"tweet_times";s:1:"1";s:5:"delay";s:1:"0";s:7:"enabled";s:1:"1";s:10:"separation";i:60;s:7:"version";s:3:"3.7";s:14:"tweet_template";b:0;s:6:"status";i:4;s:6:"result";a:0:{}s:13:"tweet_counter";i:1;s:13:"tweet_log_ids";a:0:{}s:9:"hash_tags";a:0:{}s:8:"accounts";a:1:{i:0;s:6:"skd_nw";}}'
categories:
  - クリエイティブ
tags:
  - Sass
  - webpack

---
以前webpackでsass-loaderを使ってSassのコンパイルを出来るようにしていました。
  
その中で以下のようにSassファイル側でディレクトリの中身のimportをかける指定を行っていたのですが、上手くコンパイル出来ないという問題にしばらくぶつかってました。

    @import "object/project/*";
    

## 環境

webpack: v1.14.0
  
sass-loader: v4.1.1
  
import-glob-loader: v1.1.0

## sass-loaderが対応していない

gulpでSassのコンパイルタスクを組んでいた時も起こっていたので、想像がついていたのですが、sass-loaderがnode-sassを使っているらしく、このモジュールがディレクトリ単位のimportに対応していないというのが原因でした。

参考: [Support for globbed imports? · Issue #151 · jtangelder/sass-loader][1]

## import-glob-loaderで対応する

issue内でも有りましたが、sass-loaderが対応する予定は無いらしく、別のloaderで対応する必要があるようです。
  
ここで使うのが以下のloaderで、SassやCSS, ECMASｃriptのimport周りの拡張をしてくれるloaderのようです。
  
[import-glob-loader][2]

ちなみに、PostCSSなら以下のモジュールで * (ワイルドカード)を使ったimportができるようになるみたいです。
  
[TrySound/postcss-easy-import: PostCSS plugin to inline @import rules content with extra features][3]

npmのページではmoduleのpreloadersで指定するような書き方がされていました。

    {
      module: {
        preloaders: [{
          test: /\.scss/,
          loader: 'import-glob-loader'
        }]
      }
    }
    

そこで指定しても上手くできなかったため、それっぽいことをしていた人の記事やloaderの読み込み方を見ながら手探りでやっていたのですが、以下で出来ました。

    loaders: [
          {
            test: /\.css$/,
            loader: ExtractTextPlugin.extract('style', 'css!sass-loader!import-glob')
          }
        ]
    

CSSファイルをJSファイルではなくCSSファイルでほしかったので、extract-text-webpack-pluginを使っていますが、sass-loaderにつづいてimport-glob-loaderを繋げているのがポイントかなと思います。

webpack2でpreloaderが使えなくなるようなので、それを考えるとこうするのがいいのかも？

今回結構苦戦したので、ドキュメントはしっかり読んだ方がいいなというのと、webpackはもう少し調べたほうが良さそうだなと感じました…。

 [1]: https://github.com/jtangelder/sass-loader/issues/151
 [2]: https://www.npmjs.com/package/import-glob-loader
 [3]: https://github.com/TrySound/postcss-easy-import