---
title: 早いしカスタマイズできると噂のPostCSSに触れてみた
author: コニタン
type: post
date: 2016-09-26T23:19:57+00:00
url: /archives/1920
wordtwit_post_info:
  - 'O:8:"stdClass":13:{s:6:"manual";b:0;s:11:"tweet_times";s:1:"1";s:5:"delay";s:2:"15";s:7:"enabled";s:1:"1";s:10:"separation";i:60;s:7:"version";s:3:"3.7";s:14:"tweet_template";b:0;s:6:"status";i:2;s:6:"result";a:0:{}s:13:"tweet_counter";i:3;s:13:"tweet_log_ids";a:2:{i:0;i:1932;i:1;i:1933;}s:9:"hash_tags";a:0:{}s:8:"accounts";a:1:{i:0;s:6:"skd_nw";}}'
wordtwit_posted_tweets:
  - 'a:2:{i:0;i:1932;i:1;i:1933;}'
categories:
  - クリエイティブ
tags:
  - CSS
  - gulp
  - Postcss
  - Sass

---
普段はSass & Bourbonでオラオラやっているのですが、Sassの機能も主にimportや変数、入れ子、ちょっとした計算くらいで、mixin辺りも使わなくなってきていて、必要な機能だけにしぼりつつ欲しい機能を追加出来たら良いよねって思っていました。
  
そんな中少し前ですが、自称CSSエンジニアのある人からPostCSSの話を聞いたことを思い出し、今回はサッと導入できそうなものに軽く触れてみました。

## PostCSSって？

JSの **プラグインを使ってCSSを変換してくれるツール** で、導入するプラグインによって色んな処理ができます。

**カスタマイズできる**点と**パフォーマンスが良い**という点ではかなり惹かれました。

## プラグインについて

結構数が有るみたいでどれを入れると良いのか、そもそも入れたい物ってどれなのかと探すのが大変ですが、使いたいものだけ導入できるのは良いですね。

とりあえずベンダープレフィックスを自動付与してくれるAutoprefixerやコードの圧縮をしてくれるcssnano辺りは鉄板になるだろうなと思います。

その他導入できるプラグインは以下で見ることが出来ます。
  
[postcss/plugins.md at master · postcss/postcss][1]

他にも[PostCSS.parts][2]というカテゴリ毎に見ることができるサイトもありました。

## gulpでタスクを組んで見る

今回は以下が出来るようにしてみました。

  * 他ファイルのimport (ワイルドカードで指定も可能)
  * 変数の使用
  * ネストの使用
  * ベンダープレフィックスの自動付与
  * CSSの圧縮

<pre><code class="js">var gulp       = require('gulp');
var postCss    = require('gulp-postcss');

gulp.task('css', function() {
  gulp.src([
      'source/pcss/*.css',
      '!source/pcss/_*.css'
    ])
    .pipe(postCss([
      require('postcss-easy-import')({
        glob: true
      }),
      require('postcss-simple-vars'),
      require('postcss-nested'),
      require('autoprefixer'),
      require('cssnano')
    ]))
    .pipe(gulp.dest('dest/css/'));
});
</code></pre>

オプションの指定に悩みましたが、こんな感じに指定できるようです。
  
今回は `@import` でディレクトリ全体なんかの指定が出来るワイルドカード(*)を使えるようにしてます。

実際に組んでみたものを以下にあげているので良かったら使ってみてください。
  
[d-kusk/try-postcss][3]

## その他環境について

Atomの場合、言語パッケージが公開されていたので入れてみました。
  
[language-postcss][4]

拡張子が .pcss か SugarSSの .sss に対応するようです。
  
付けるなら前者かなぁ…と思っていたのですが、PostCSSによる変換後に .pcss の拡張子から .css に変換してくれないみたいなので、もし上記の使うならちょっと気持ち悪いけど gulp-rename 辺りのお世話になるのかな？

あんまりコレだって感じがしなかったのと、多くの人が変換対象のファイルの拡張子にcssを指定していたのでこのパッケージにはサヨナラしました。

## 触れてみて

バリバリプラグイン使って書いていくと読めなさそうなので、とりあえずprecssプラグイン + αである程度Sassっぽい書き方が出来るようにしておいて、徐々に導入していくのが良さそうな気がします。

あと、今後流行ってくるとオレオレ秘伝のCSS変換器があちこちにあるみたいな状況になりそうなので、ボイラープレートとして作って置いておく場合や複数人で使う場合は **READMEやその他テキストに何が出来るのか書く** というのはやって置いたほうが良さそうです。

## オススメの資料

PostCSSに関しては以下のスライドが分かりやすかったのでオススメです。
  
[PostCSS とは何か &#8211; SSSSLIDE][5]

 [1]: https://github.com/postcss/postcss/blob/master/docs/plugins.md
 [2]: http://postcss.parts/
 [3]: https://github.com/d-kusk/try-postcss
 [4]: https://atom.io/packages/language-postcss
 [5]: http://sssslide.com/speakerdeck.com/jmblog/postcss-tohahe-ka