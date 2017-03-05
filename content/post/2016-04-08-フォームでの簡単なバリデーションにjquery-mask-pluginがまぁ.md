---
title: フォームでの簡単なバリデーションにjQuery Mask pluginがまぁまぁ便利だった
author: コニタン
type: post
date: 2016-04-07T16:14:45+00:00
url: /archives/1774
wordtwit_post_info:
  - 'O:8:"stdClass":13:{s:6:"manual";b:0;s:11:"tweet_times";s:1:"1";s:5:"delay";s:2:"15";s:7:"enabled";s:1:"1";s:10:"separation";i:60;s:7:"version";s:3:"3.7";s:14:"tweet_template";b:0;s:6:"status";i:2;s:6:"result";a:0:{}s:13:"tweet_counter";i:3;s:13:"tweet_log_ids";a:2:{i:0;i:1776;i:1;i:1777;}s:9:"hash_tags";a:0:{}s:8:"accounts";a:1:{i:0;s:6:"skd_nw";}}'
wordtwit_posted_tweets:
  - 'a:2:{i:0;i:1776;i:1;i:1777;}'
categories:
  - クリエイティブ
tags:
  - jQuery
  - プラグイン

---
流れにのってES6かTypeScriptにいきたいなーと思いつつ、プラグインの恩恵が凄くて感謝しながらjQuery使ってます。

さて、この間フォームを組むことがあって、その中で **簡単なバリデーションをしたい** という要望がありました。
  
自分で組んでもよかったのですが中には面倒なものもあって便利なプラグインはないものかーと思っていたら有りました。

それがこの<a href="https://igorescobar.github.io/jQuery-Mask-Plugin" target="_brank">jQuery Mask Plugin</a> です。

例えば、

  * 2016/04/03のように年月日毎に／を挟みたい
  * 時間の表記を入力する時、2桁毎にコロン( : )を入れたい
  * 半角英数のみ認めて、全角英数の入力は弾きたい
  * 入力だけでなく、コピペにも対応したい

この辺は大丈夫だった気がします。

## 導入

    <script src="https://ajax.googleapis.com/ajax/libs/jquery/1.12.2/jquery.min.js"></script>
    <script src="FILEPATH/jquery.mask.min.js"></script>
    

プラグインお約束のjQueryの後で読み込みます。

    $(function(){
      $('.date').mask('00/00/0000');
    });
    

そして、実際に使うときはこんな感じで、バリデーションを当てたい要素に対してmaskメソッドを繋ぎ、引数で指定するだけです。何を指定するのかはサイトを見てください。

## 感じたこと

また、単に入力のチェックを行うだけでなく、placeholderをあてたり、パターンで絞り込むようなカスタマイズもできるのは良かった。
  
しかし、作者が海外の人のようなので、色んなバリデーションが海外仕様で使えないものも幾つかある。

[jQuery Mask Plugin &#8211; A jQuery Plugin to make masks on form fields and html elements.][1]

 [1]: https://igorescobar.github.io/jQuery-Mask-Plugin/