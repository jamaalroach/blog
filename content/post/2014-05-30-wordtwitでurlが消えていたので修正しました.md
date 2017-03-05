---
title: WordTwitでURLが消えていたので修正しました
author: コニタン
type: post
date: 2014-05-29T23:14:03+00:00
url: /archives/994
wordtwit_post_info:
  - 'O:8:"stdClass":13:{s:6:"manual";b:0;s:11:"tweet_times";i:1;s:5:"delay";s:1:"0";s:7:"enabled";s:1:"1";s:10:"separation";s:3:"270";s:7:"version";s:3:"3.6";s:14:"tweet_template";b:0;s:6:"status";i:2;s:6:"result";a:0:{}s:13:"tweet_counter";i:5;s:13:"tweet_log_ids";a:4:{i:0;i:998;i:1;i:999;i:2;i:1000;i:3;i:1001;}s:9:"hash_tags";a:0:{}s:8:"accounts";a:1:{i:0;s:6:"skd_nw";}}'
wordtwit_posted_tweets:
  - 'a:4:{i:0;i:998;i:1;i:999;i:2;i:1000;i:3;i:1001;}'
categories:
  - クリエイティブ
tags:
  - WordPress
  - プラグイン

---
ここ最近、夜書いて朝公開されるように予約投稿して寝ていますが、朝起きたらリプが来ていて、
  
「URLついてないですよ〜」
  
なんて言われるわけです。
  
おかしい…

前起こった時は短縮サービスが原因なのかな？と思い変更とかしてました。
  
ですが結局解決せず、放置していました。

そして最近検索して分かったのでそのまとめを書いておきます。

<!--more-->

※初期設定は省きます。
  
設定をする記事なんかも多いのでそこは検索してください。

### とりあえず日本語化

WordTwitの管理画面へ行きます。
  
WordTwit設定 >Option > General のプルダウンを日本語にして変更保存
  
これでとりあえず管理画面を日本語化しておきます。
  
完全には日本語化されませんがしないよりは分かりやすいはずです。

### URLを表示させる

[<img src="https://i2.wp.com/peng-note.com/images/2014/05/40c08c20340fb78d2608bf4c10077c0d.jpg?fit=600%2C159" alt="投稿タイトルの短縮チェックボックス" class="aligncenter size-full wp-image-995" srcset="https://i2.wp.com/peng-note.com/images/2014/05/40c08c20340fb78d2608bf4c10077c0d.jpg?w=600 600w, https://i2.wp.com/peng-note.com/images/2014/05/40c08c20340fb78d2608bf4c10077c0d.jpg?resize=300%2C79 300w" sizes="(max-width: 600px) 100vw, 600px" data-recalc-dims="1" />][1]
  
原因から言うと、WordTwit設定 > Option > Publishing Widget の「ツイートの文字数制限のために投稿タイトルを短縮する」(上の画像参照)という部分にチェックが入っていたからのようです。
  
投稿タイトルを短縮なので、記事のタイトルの事だと思ったんですけどね…
  
ここのチェックを外して投稿しなおした結果ちゃんとURL付きで投稿出来ました。

 [1]: https://i2.wp.com/peng-note.com/images/2014/05/40c08c20340fb78d2608bf4c10077c0d.jpg