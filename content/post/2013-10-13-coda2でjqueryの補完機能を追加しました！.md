---
title: Coda2でjQueryの補完機能を追加しました！
author: コニタン
type: post
date: 2013-10-12T18:47:26+00:00
url: /archives/285
wordtwit_post_info:
  - 'O:8:"stdClass":13:{s:6:"manual";b:0;s:11:"tweet_times";s:1:"1";s:5:"delay";s:1:"0";s:7:"enabled";s:1:"1";s:10:"separation";i:60;s:7:"version";s:3:"3.0";s:14:"tweet_template";b:0;s:6:"status";i:2;s:6:"result";a:0:{}s:13:"tweet_counter";i:4;s:13:"tweet_log_ids";a:3:{i:0;i:293;i:1;i:294;i:2;i:295;}s:9:"hash_tags";a:0:{}s:8:"accounts";a:1:{i:0;s:6:"skd_nw";}}'
wordtwit_posted_tweets:
  - 'a:3:{i:0;i:293;i:1;i:294;i:2;i:295;}'
categories:
  - クリエイティブ
tags:
  - Coda2
  - jQuery

---
エディタは、Vimから乗り換えて<a href="http://panic.com/coda/" target="_blank">Coda2</a>を使っています。
  
快適です。

そのCoda2を使っていたらjQueryの補完があれれ？ってなったのでその話。
  
<!--more-->

最近jQueryの勉強しようと思って、<a href="http://www.amazon.co.jp/Web%E5%88%B6%E4%BD%9C%E3%81%AE%E7%8F%BE%E5%A0%B4%E3%81%A7%E4%BD%BF%E3%81%86-jQuery%E3%83%87%E3%82%B6%E3%82%A4%E3%83%B3%E5%85%A5%E9%96%80-WEB-PROFESSIONAL-%E8%A5%BF%E7%95%91/dp/4048684116" target="_blank">Web制作の現場で使う jQueryデザイン入門 (WEB PROFESSIONAL) [大型本]</a>を読んでます。
  
読みながらサンプルを書いていたのですが、しっかり補完されない。
  
いや、されるんだけどなんかオカシイ。
  
なんだこれ？って思ってたらJavaScriptの方で補完されてたらしくて。
  
.fadeIn()とか.show()とか打っても全く候補に出てこないという。

そこで調べてみると、
  
**Coda2には初期ではjQueryの補完機能が入ってない**んだとか
  
そりゃできない。
  
卵なしで目玉焼き作れくらいできない。

そこで入れましたプラグイン。

参考サイト：<a href="http://blog.morizotter.com/2013/09/12/javascript-jquery/" target="_blank">Coda2のjQueryコード補完プラグイン &#8211; Morizotter Blog</a>

### プラグインのインストール方法と設定

上記のサイトで殆ど書かれています。

> <a href="https://github.com/rayman813/coda2-mode-jquery" target="_blank">coda2-mode-jquery &#8211; Github</a>
  
> ダウンロードして、.modeファイルをダブルクリックすればもう導入完了です。Coda2を再起動する必要もありませんでした。 

ほんとこれだけ。
  
やり方に困る必要もありませんでした。

と思ってたら、僕の場合は[書式]>[言語モード]に現れただけでJavaScriptのままだったので、それをjQueryに変えたらできました。

これで快適！