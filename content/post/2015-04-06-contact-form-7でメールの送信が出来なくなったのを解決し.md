---
title: Contact Form 7でGmailを使ったメールの送信が出来なくなったのを解決しました
author: コニタン
type: post
date: 2015-04-05T23:11:30+00:00
url: /archives/1587
wordtwit_posted_tweets:
  - 'a:1:{i:0;i:1591;}'
wordtwit_post_info:
  - 'O:8:"stdClass":13:{s:6:"manual";b:0;s:11:"tweet_times";i:1;s:5:"delay";s:1:"0";s:7:"enabled";s:1:"1";s:10:"separation";s:3:"270";s:7:"version";s:3:"3.7";s:14:"tweet_template";b:0;s:6:"status";i:2;s:6:"result";a:0:{}s:13:"tweet_counter";i:5;s:13:"tweet_log_ids";a:4:{i:0;i:1591;i:1;i:1592;i:2;i:1593;i:3;i:1594;}s:9:"hash_tags";a:0:{}s:8:"accounts";a:1:{i:0;s:6:"skd_nw";}}'
categories:
  - クリエイティブ
tags:
  - WordPress
  - プラグイン

---
結構ありふれた内容では有るんですが、長期間戦っていた問題がやっと解決したので備忘録も兼ねての記事となります。

## こんな事が起こっていました

### (数ヶ月前)問い合わせ後のメールの自動送信が上手くいかなくなる

フォームからWordPressへの送信は出来ていたようなのですが、WordPress側からメールサーバーへの送信が上手く出来ていませんでした。
  
メールの送信にGmailを使っていたのですが、どうやらスパム的な扱いを受けて上手く届いていなかったようです。
  
始めは送れていたのに突然送れなくなった！というのはよく書かれていますがほんとにそうでした。送れなくなる少し前とかに何か通知が欲しかったです…。

この問題に関しては、Flamingoというお問い合わせフォームからの情報を記録するプラグインを導入し、何が送られてきたかを確認できる状況を作る事で応急処置。
  
<a href="https://wordpress.org/plugins/flamingo/" target="_blank">WordPress › Flamingo « WordPress Plugins</a>

### ついにフォームからの送信すらできなくなる

遂に昨日、「メッセージの送信に失敗しました。間をおいてもう一度お試しいただくか、別の手段で管理者にお問い合わせ下さい。」というエラーが出るようになり利用者の方から連絡を受けました。

## やったこと

  * Contact Form 7の設定を見直す
  * WP Mail SMTPの導入
  * アプリの認証

## Contact Form 7の設定を見直す

Contact Form 7の宛先や差出人が間違っているんじゃないかと必死に見なおしたり打ちなおしたりしました。
  
宛先が間違っていただけっていうパターンもあるので要見直し。
  
前は差出人を書き間違えていて上手くいきませんでした。

## WP Mail SMTPの導入

Gmailを使っている人によく起こる問題らしいのですが、差出人をGmailのアドレスにすることによって送信しているサーバーの情報と異なるためスパム扱いを受けることになるようです。
  
その為WP Mail SMTPというプラグインを使って、外部のSMTPサーバーを使ってメールを送ることで問題を回避するというものがありました。
  
<a href="https://wordpress.org/plugins/wp-mail-smtp/" target="_blank">WordPress › WP Mail SMTP « WordPress Plugins</a>

参考：<a href="http://www.jagaimopotato.com/blog/wordpress/wordpress-smtp-1383.html" target="_blank">WordPressのメールが送信できないので、SMTPサーバの設定を外部サーバに変更する。</a>

この設定を行うことで多くの人がメールを送信できるようになったようですが、僕の場合そうはいかず、テストメールを送っても結果でbool(false)が起きていました。
  
エラーを見てみると結構序盤で起こっていて、SMTPの認証エラーが起きていました。

## アプリの認証

何が原因なのか探ってみたところ、原因が多分これ。

> 最近googleはアカウントの認証を厳しくしてるみたいで、得体のしれない端末がログインしようとするとブロックしてしまうらしい。このブロックに引っかかって、webサーバからgoogleアカウントにログインできていなかったみたい。

Googleさんが仕事をし過ぎたらしいです。
  
そこで以下のサイトを参考にアプリの認証を行いブロック対象から外して貰うことに。

<a href="http://absg.hatenablog.com/entry/2014/08/14/202811" target="_blank">wordpressで作った問い合わせフォームからメールが送信できない &#8211; やったこと</a>

このサイトしっかりは書いていないのですが、Contact Form 7で送信に使用するアカウントで、Googleにログインしたままココ(https://accounts.google.com/DisplayUnlockCaptcha)にアクセスし、アプリの認証を行うことでWP Mail SMTPが上手く動くようになりメールが送信出来るようになりました。

いや〜　長かった。