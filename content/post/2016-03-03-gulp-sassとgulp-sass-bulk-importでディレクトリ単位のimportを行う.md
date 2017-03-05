---
title: gulp-sassとgulp-sass-bulk-importでディレクトリ単位のimportを行う
author: コニタン
type: post
date: 2016-03-02T22:40:40+00:00
url: /archives/1752
wordtwit_post_info:
  - 'O:8:"stdClass":13:{s:6:"manual";b:0;s:11:"tweet_times";s:1:"1";s:5:"delay";s:2:"15";s:7:"enabled";s:1:"1";s:10:"separation";i:60;s:7:"version";s:3:"3.7";s:14:"tweet_template";b:0;s:6:"status";i:2;s:6:"result";a:0:{}s:13:"tweet_counter";i:3;s:13:"tweet_log_ids";a:2:{i:0;i:1754;i:1;i:1755;}s:9:"hash_tags";a:0:{}s:8:"accounts";a:1:{i:0;s:6:"skd_nw";}}'
wordtwit_posted_tweets:
  - 'a:2:{i:0;i:1754;i:1;i:1755;}'
categories:
  - クリエイティブ
tags:
  - gulp
  - Sass

---
普段はgulpを使ってSassのコンパイルをかけていたのですが、その際Sassのコンパイルにgulp-ruby-sassモジュール(ローカルのSassは 3.4.13)を使っていました。

最近SMACSSやFLOCSSなどのCSSの設計手法を勉強していますが、これを実際にSassで実現しようとした際、 **複数のファイルをimportする** 必要が出ました。

    ├── foundation/
    │   └── _normalize.scss
    ├── layout/
    │   ├── _g-header.scss
    │   └── _layout.scss
    ├── object/
    │   ├── component/
    │   ├── project/
    │   │   ├── _p-g-work.scss
    │   │   ├── _p-g-nav.scss
    │   │   
    │   └── utility/
    └── style.scss
    

例えばlayout/下やobject/project下の複数ファイルをstyle.scssでimportするみたいな感じ。

ファイルを1個1個指定してimportすると、ファイルを作る度にimportの記述を書かなきゃいけないしメンドクサイ。
  
そこで、ディレクトリ単位でimportできないかと以下の様に指定していました。

    @import "layout/*";
    @import "object/component/*";
    

するとこんなエラーが&#8230;

    file to import not found or unreadable
    

パスは間違っていないハズなのでどういうことかと思いながら色々調べていたのですが、この記事に出会いました。

<a href="http://qiita.com/ushisantoasobu/items/a40f6f9081ec98df1484" target="_blank"><code>gulp-sass</code>で<code>file to import not found or unreadable</code>のエラー &#8211; Qiita</a>

Sassのバージョンやファイルパスの確認などされていましたが、この人の場合は、拡張子がまずかったようです。

今回の拡張子は.scssのため原因はコレではないようです。

## Sass-globbingも1つの手

更に調べていると、sass-globbingというものがあるらしく、これを用いることでディレクトリ単位のコンパイルが可能になるらしいです。<aside class="ref"> 

<a href="http://qiita.com/t32k/items/229745617da41f308f20" target="_blank">参考：sass-globbingでSassファイルをお手軽管理 &#8211; Qiita</a>
  
</aside> 

しかし、これはおそらくターミナル上でSassコマンドを叩いてコンパイルをかける場合の話で、gulpに任せてる自分には使えないものなのかなぁと。

## 解決

そこでgulpで使えるものを探していたのですが、以下の記事を見つけました。
  
<a href="https://torounit.com/blog/2015/08/10/2045/" target="_blank">gulp-sass-bulk-importを使ってSassの@importをすっきり管理する。 – Toro_Unit</a>

gulp-sassでのコンパイルに<a href="https://www.npmjs.com/package/gulp-sass-bulk-import" target="_blank">gulp-sass-bulk-import</a>を用いる事でディレクトリ単位でコンパイルかけれるようになるという話。
  
sassのコンパイル用のモジュールは変わってしまうけど、コンパイルできるなら…！と思いタスクを組むことで出来ました。

    var gulp     = require('gulp');
    var sass     = require('gulp-sass');
    var bulkSass = require('gulp-sass-bulk-import');
    
    gulp.task('sass', function() {
      return  gulp.src('./scss/**/*.scss')
        .pipe(bulkSass())
        .pipe(sass().on('error', sass.logError))
        .pipe(gulp.dest('./css'))
    });
    

### 各モジュールのバージョン

  * &#8220;gulp-sass&#8221;: &#8220;^2.2.0&#8221;,
  * &#8220;gulp-sass-bulk-import&#8221;: &#8220;^1.0.1&#8221;

困っていた方はこれを試してみてください。

gulp-ruby-sassの方は書き方が特殊なため上手く組み込めませんでした。どうやったら良いんだろ？