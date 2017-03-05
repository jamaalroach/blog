---
title: DBのバックアップに! WP DBManager の設定をしました
author: コニタン
type: post
date: 2014-02-11T23:00:05+00:00
url: /archives/713
wordtwit_post_info:
  - 'O:8:"stdClass":13:{s:6:"manual";b:0;s:11:"tweet_times";i:1;s:5:"delay";s:1:"0";s:7:"enabled";s:1:"1";s:10:"separation";s:3:"300";s:7:"version";s:5:"3.5.1";s:14:"tweet_template";b:0;s:6:"status";i:2;s:6:"result";a:0:{}s:13:"tweet_counter";i:4;s:13:"tweet_log_ids";a:3:{i:0;i:726;i:1;i:727;i:2;i:728;}s:9:"hash_tags";a:0:{}s:8:"accounts";a:1:{i:0;s:6:"skd_nw";}}'
wordtwit_posted_tweets:
  - 'a:3:{i:0;i:726;i:1;i:727;i:2;i:728;}'
categories:
  - クリエイティブ
tags:
  - WordPress
  - プラグイン

---
ずっと前に入れたはいいものの、放置していたプラグイン「WP DBManager」の設定をしたのでそのメモ。

<!--more-->

### WP DBManagerって？

WordPressのデータベースの最適化やバックアップをしてくれるプラグインです。

ダウンロードはこちら
  
<a href="http://wordpress.org/plugins/wp-dbmanager/" target="_blank">WordPress › WP-DBManager « WordPress Plugins</a>

なんか色々と出来るらしい　色々と。

### プラグインを入れた経緯

サーバーの引っ越しや、データ改ざんを受けた時にもバックアップは大切になってくるので、入れとかないとなって思ってだいぶ前に入れました。
  
居るだけで仕事してないやつです。

### WP DBManagerの日本語化

なぜ放置していたかというと、設定がよく分からなかったんです。
  
全部英語ですから。読めない！ｗ

そこで検索してみると、あるじゃないですか！
  
<a href="http://ozpa-h4.com/2012/07/19/wp-dbmanager-japanese/" target="_blank">WordPressデータベースのバックアップをとってくれるプラグイン「WP-DBManager」を日本語化して分かり易くしよう | OZPAの表4</a>

ただ、記事内にあったページにいってDLしようとすると出来なくて。どうやら2013年の8月くらいからページにアクセスできなくなってるようです。

ということで、日本語化は諦めました。

### WP DBManagerの設定

設定は意外と簡単でした。(項目が読めてないだけ…ｗ)

参考にしたのはコチラ：
  
<a href="http://liginc.co.jp/web/wp/plug-in/67897" target="_blank">WordPressのデータを改ざんされる前に！プラグイン「WP DBManager」の使い方 | 株式会社LIG</a>

インストールした後、.htaccess.txtを wp-content/plugins/wp-dbmanager から wp-content/backup-db に移動し、.htaccessに変更します。

管理画面のサイドバーの下の方にDatabaseの項目が出るので、そこからDB Optionsを選択し、以下の設定をします。

#### Path To Backup

バックアップの保存場所です。大体が wp-content/backup-db に保存されると思います。

#### Maximum Backup Files

上で設定したディレクトリに保存するバックアップの最大数です。

#### Automatic Backing Up Of DB

データベースのバックアップを行う間隔を設定できます。
  
そこまで更新頻度が高いわけでもないので、2週間くらいにしてみました。
  
引越し時などで.gzip形式にしておくと良いという記述をよく見かけるので、gzipにする項目を有効にしておきました。

更に、メールアドレスを入力し、バックアップをとった後にメールで送ってくれるようにしておきました。時系列も分かりやすくていい気がします。

#### Automatic Optimizing Of DB

データベースの最適化を行う間隔を設定できます。
  
2週間の頻度で行うようにしてみました。

最適化を行った後でバックアップをとってくれるようにして欲しいな〜

* * *これが最低限の設定らしいです。ここまでできたらとりあえずSaveChangeを押して保存しましょう。


  
メールアドレスを入力していれば、バックアップのデータがメールで飛んできます。</p> 

なにか起こるまでにしっかり設定しておきましょう。