---
title: WordBench京都テーマにまつわるエトセトラに参加してきました
author: コニタン
type: post
date: 2015-11-08T23:12:00+00:00
url: /archives/1708
wordtwit_post_info:
  - 'O:8:"stdClass":13:{s:6:"manual";b:0;s:11:"tweet_times";i:1;s:5:"delay";s:1:"0";s:7:"enabled";s:1:"1";s:10:"separation";s:3:"240";s:7:"version";s:3:"3.7";s:14:"tweet_template";b:0;s:6:"status";i:2;s:6:"result";a:0:{}s:13:"tweet_counter";i:4;s:13:"tweet_log_ids";a:3:{i:0;i:1711;i:1;i:1712;i:2;i:1713;}s:9:"hash_tags";a:0:{}s:8:"accounts";a:1:{i:0;s:6:"skd_nw";}}'
wordtwit_posted_tweets:
  - 'a:3:{i:0;i:1711;i:1;i:1712;i:2;i:1713;}'
categories:
  - 行ってきた
tags:
  - Webデザイン
  - WordPress
  - イベント

---
久々な気がしますが、WordBench京都に参加してきました。

以前のBench京都で「10月はマテリアルデザインの話します！」っていうのを聞いていたので、応募ページが流れてきた際にすぐに申し込んだような気がします。

今回は、

  * 聞いて覚えるマテリアルデザイン入門
  * テーマ開発座談会

の二本立てでした。

## 聞いて覚えるマテリアルデザイン入門

マテリアルデザインの紹介セッションでした。

フラットデザインとはどう違うのか、どういう事に気をつけて作らないといけないのかそんな話。

マテリアルデザインはあらゆるデバイスで統一感のある「UIの基礎原則」を作る事が目的のようです。

色んなUIの実装の時に色はどうする、アニメーションを実装するときは意味が伝わるようにしたり協調性をもたせたりと色々とすべきことがあるようです。

また、画像を使うときには**喜びの画像**を使ったり、ユーザーに確認をするときの文言などは**動詞を付ける**など幾つかのこだわりも見えておもしろいなと思いました。

個人的にはInboxなどにある丸いボタンの使い方が難しい気がして気になるところです。

詳しいことはGoogleが公開しているガイドラインを参照とのこと。
  
<a href="https://www.google.com/design/spec/material-design/introduction.html" target="_blank">Introduction &#8211; Material design &#8211; Google design guidelines</a>

## テーマ開発座談会

参加者の質問に応えるという場でした。
  
参加の際に質問事項を入れることになっていたようでしたが、入れてなかったような…スイマセン。

幾つか気になっていた質問を。

### ベースにするテーマは？

僕は基本フルスクラッチで制作する人なんですけど、色々あるみたいだしたまには使ってみても良いのかなーと思っていましたが、以下の様な感じ？

ブログじゃないものや凝ったモノなら<a href="http://underscores.me/" target="_blank">_s</a>。
  
子テーマ対応するなら<a href="https://ja.wordpress.org/themes/habakiri/" target="_blank">habakiri</a>が良いんだとか。
  
あと、<a href="http://lightning.vektor-inc.co.jp/ja/" target="_blank">Lightning</a>も使いやすいとか。

個人的にはその後紹介された<a href="https://github.com/wp-bathe/bathe" target="_blank">bathe</a>が気になります。

### 機能をfunctions.phpに入れるかプラグインにするかというのは何か基準があるの？

この間のWordCampKansaiでそんな話を聞いてどうするのが良いんだろうともやもやしていましたがなんとなく分かったような気がします。

A.テーマに依存する機能はテーマに、そうでないものはプラグインを使うと良い。

Analyticsとかカスタム投稿タイプとか**テーマ変えて消えちゃうと困るもの**はプラグインを使おうという事の様です。

参考:
  
<a href="https://firegoby.jp/archives/5975" target="_blank">Plugin Territory – WordPressのその処理はテーマでやるべきかプラグインでやるべきか？ | Firegoby</a>
  
<a href="http://www.slideshare.net/mignonstyle/wordpress-themepluginterritory" target="_blank">WordPress公式ディレクトリテーマ登録のポイント：プラグインテリトリーを理解してハッピーになろう</a>

&#8212;

## ビアバッシュ！

さて<del datetime="2015-11-08T09:12:04+00:00">ここからが本編！</del>。

今回は飲み食いしながら喋ってる間にLTが開催されました。

ネタとしては、公式テーマ登録目指して頑張ってる人のテーマ紹介やWordCampTokyo2015の振り返り(兼じゃんけん大会)、会社のサイトをYahoo砲にも耐えられるような仕組みをAWSで作った話、Bourbonの紹介などなどありました。

じゃんけん大会ではありがたいことにWordCampTokyoの景品？だったコースターとか、ステッカーを頂けました。
  
行ってないからなんか使いにくい(；´Д｀)

今はとりあえずBoutbonで何かサイト作りたい。