---
title: webpackでES2015とSassのコンパイルができるようにした
author: コニタン
type: post
date: 2017-01-23T11:36:47+00:00
url: /archives/2029
wordtwit_post_info:
  - 'O:8:"stdClass":13:{s:6:"manual";b:0;s:11:"tweet_times";s:1:"1";s:5:"delay";s:1:"0";s:7:"enabled";s:1:"1";s:10:"separation";i:60;s:7:"version";s:3:"3.7";s:14:"tweet_template";b:0;s:6:"status";i:4;s:6:"result";a:0:{}s:13:"tweet_counter";i:1;s:13:"tweet_log_ids";a:0:{}s:9:"hash_tags";a:0:{}s:8:"accounts";a:1:{i:0;s:6:"skd_nw";}}'
categories:
  - クリエイティブ
tags:
  - es2015+
  - Sass
  - webpack

---
これまでプライベートではgulpを、仕事ではCodekitを使ってたんだけど、ちょっと違うのも触ろうと思ったのと、前ちょこっと触ったっきりで仕事での導入になかなか踏み切れなかったので、時間ができたタイミングでやってみた。

目指したのはES2015+とSass(PostCSSでも良かったけどまだSass使う頻度の方が多そうだった)のコンパイルが出来る環境で、ついでにSassファイル分けるためのディレクトリも作っておくこと。
  
そうしておけばスタート時に0からのスタートじゃないし楽だよねって発想。

とりあえずできたのは [ここ][1] においてる。

## ES2015

「2016使えます」とかなんなら「もう2017ですよ」とか煽ってる人も居るんだけどとりあえず2015でやってみた。後で徐々に上げる予定。

色々記事見てたけど、結局やりたいことやってたのは [@misumi_takuma][2] さんのやつだったので拝借してとりあえず自分に分かるようにちょっと書き換えた。

[web-starter-kit/webpack.config.babel.js at master · mismith0227/web-starter-kit · GitHub][3]

## Sass

この記事の冒頭でも書いてあったけど、ESのコンパイルまでやってもSassのコンパイルまでやってるやつってなかなか無くて困ったんだけど、これの通りに進めたら一応コンパイルはできた。

[webpackを使ってsassをコンパイルできるようにしよう！ &#8211; Qiita][4]

### Bourbon / Neat

いつもはSassだけじゃなく、MixinライブラリのBourbonを使っていて、隙あらばNeatも使いたいので、そのコンパイルもできるようにした。

[webpackを使ってnode-sass環境にbourbon3兄弟を導入する &#8211; Qiita][5]

Sass-loaderのオプションでそれぞれのpathを渡すことで、BourbonとNeatも使えるようになるみたいなので、他のものも使えるようになるのかな。

## 今後やりたいこと

SassからPostCSSに変えても良いなーとは少し前から思っているので、別ブランチで進めようかな

 [1]: https://github.com/d-kusk/webBoilerplate
 [2]: https://twitter.com/misumi_takuma
 [3]: https://github.com/mismith0227/web-starter-kit/blob/master/webpack.config.babel.js
 [4]: http://qiita.com/nicchi__1985/items/e30e73de6d8443909537
 [5]: http://qiita.com/cotto89/items/ddd12a24cd40fac5c419