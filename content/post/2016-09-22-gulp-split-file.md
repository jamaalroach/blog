---
title: gulpのタスクが長くなってきたのでファイル毎に分割した
author: コニタン
type: post
date: 2016-09-22T00:41:13+00:00
url: /archives/1901
wordtwit_post_info:
  - 'O:8:"stdClass":13:{s:6:"manual";b:0;s:11:"tweet_times";s:1:"1";s:5:"delay";s:1:"0";s:7:"enabled";s:1:"1";s:10:"separation";i:60;s:7:"version";s:3:"3.7";s:14:"tweet_template";b:0;s:6:"status";i:2;s:6:"result";a:0:{}s:13:"tweet_counter";i:3;s:13:"tweet_log_ids";a:2:{i:0;i:1915;i:1;i:1916;}s:9:"hash_tags";a:0:{}s:8:"accounts";a:1:{i:0;s:6:"skd_nw";}}'
wordtwit_posted_tweets:
  - 'a:2:{i:0;i:1915;i:1;i:1916;}'
categories:
  - クリエイティブ
tags:
  - gulp

---
思い出したようにgulpのタスク分割をしました。
  
[随分前][1]に作ってから、新しいタスク考えたらgulpfileに書き足していくスタイルだったのですが、さすがに長くて見通しが悪くなってきたので分割しました。

## 確認した環境

  * Node.js v5.6.0
  * gulp.js 
      * CLI version 3.8.11
      * Local version 3.9.1

## 分割作業

もともと空行を入れつつタスクを書いていたので塊は分かりやすかったので助かりました。（ありがとう過去の俺。

とりあえずそれぞれを別のファイルに分けて、[require-dir][2]というモジュールをインストールしました。

    $ npm i --save-dev require-dir
    

<small>※require-dir v0.3.0</small>

これを読み込んで実行した箇所で各タスクを読み込んで実行してくれるみたいです。
  
なので、gulpfile.jsに以下のように記述しました。

    var gulp     = require('gulp');
    var requireDir = require('require-dir');
    
    requireDir('./gulp/tasks', {recurse: true});
    

ファイル構造は以下のようになっていて、gulp/tasks/の中に各タスクのファイルをまとめています。

    ├── gulp/
    │     ├── config.js
    │     └── tasks/
    ├── gulpfile.js
    └── source/
              ├── coffee
              ├── jade
              └── sass
    

## configファイルの作成

タスク毎にファイルを分けたので、タスク単位での**処理は見やすくなりました**が、案件によって違うであろうファイルのパスを修正するのが面倒になりました。
  
なので、configファイルで一括管理できるようにします。

例えばこんな感じ

gulp/config.js

    module.exports ={
      source: {
        jade: 'source/jade/',
        sass: 'source/scss/',
        coffee: 'source/coffee/',
        js: 'source/js/'
      },
      dest: {
        html: './',
        css: 'assets/css/',
        js: 'assets/js/',
      }
    };
    

あとは各タスクのファイルで以下のように記述するだけです。

gulp/tasks/sass/js

    var gulp     = require('gulp');
    var config   = require('../config');
    var sass     = require('gulp-sass');
    
    gulp.task('sass', function() {
      return gulp.src([
          config.source.sass + '**/*.scss',
          '!' + config.source.sass + '**/_*.scss'
        ])
    
    

これでパスの変更もファイル1つ編集するだけでOKになりました。

参考:
  
[gulpタスクの分割 &#8211; Qiita][3]

出来たものはGitHubにあがっているのでよければどうぞ
  
[d-kusk/gulpfile][4]

 [1]: http://peng-note.com/archives/1322
 [2]: https://www.npmjs.com/package/require-dir
 [3]: http://qiita.com/dhun/items/c8633800097f1e7ecf70
 [4]: https://github.com/d-kusk/gulpfile