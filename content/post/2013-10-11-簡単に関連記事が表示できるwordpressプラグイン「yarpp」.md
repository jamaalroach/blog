---
title: 簡単に関連記事が表示できるWordPressプラグイン「YARPP」を導入してみた
author: コニタン
type: post
date: 2013-10-10T16:59:36+00:00
url: /archives/275
wordtwit_post_info:
  - 'O:8:"stdClass":13:{s:6:"manual";b:0;s:11:"tweet_times";s:1:"3";s:5:"delay";s:1:"0";s:7:"enabled";s:1:"1";s:10:"separation";s:3:"300";s:7:"version";s:3:"3.0";s:14:"tweet_template";b:0;s:6:"status";i:3;s:6:"result";a:0:{}s:13:"tweet_counter";i:1;s:13:"tweet_log_ids";a:0:{}s:9:"hash_tags";a:0:{}s:8:"accounts";a:1:{i:0;s:6:"skd_nw";}}'
categories:
  - クリエイティブ
tags:
  - WordPress
  - プラグイン

---
折角来て頂いたユーザーさんに色んな記事を読んで欲しいので、関連記事を表示するプラグインYet Another Related Posts Pluginを導入してみました。<!--more-->

前のサーバーでも設定していたのですが、プラグインが消えていました。
  
バックアップが取れてなかったのかな？
  
ということで再び入れなおしました。

**設定もカスタマイズも簡単**なので、サッと入れれちゃうプラグインかと思います。

### プラグインの追加

まずはささっと新規追加しましょう。
  
管理画面の[プラグイン] > [新規追加] > YARPP で検索

または、
  
[Yet Another Related Posts Plugin (YARPP)][1]
  
からダウンロードする方法もあります。

### 設定

[<img src="https://i2.wp.com/peng-note.com/images/2013/10/39d7a487d5879d944205d8a9eb62309d-300x190.png?fit=300%2C190" alt="YARPP設定画面" class="aligncenter size-medium wp-image-276" srcset="https://i1.wp.com/peng-note.com/images/2013/10/39d7a487d5879d944205d8a9eb62309d.png?resize=300%2C190 300w, https://i1.wp.com/peng-note.com/images/2013/10/39d7a487d5879d944205d8a9eb62309d.png?w=731 731w" sizes="(max-width: 300px) 100vw, 300px" data-recalc-dims="1" />][2]
  
一番上の[自動表示]ですが、ここで[投稿]のチェックボックスにチェックを入れると、記事の一番下に関連記事が出ます。
  
はい簡単。

でも、他にも項目はありますよねｗ
  
続けます。

#### 一度に表示する関連記事数

一度に表示出来る関連記事数はお好みの数に設定してください。
  
カラム幅にもよりますが、

  * サムネイルの表示形式の場合は3か6個
  * リスト形式だと4〜6くらいかと思います。

かと思います。

#### 表示の形式

  * リスト形式
  * サムネイル形式</ul> 

この二種類があり、各々少し違った設定ができます。

個人的にはサムネイルで内容が少し分かりやすくなると思うので、サムネイル形式をオススメします。

あとは表示の順番を設定すると設定は完了です。

### 個別ページにだけ表示したい場合(single.php)

上の設定だと、投稿に対してはすべて関連記事がつくので、index.phpでも表示されます。
  
それをされると一気に多くの記事(タイトル)を見ていただける点ではいいかもしれないですけど、その分トップが長い‥
  
表示は記事を開いて読んでもらって、その上で関連記事を提供したほうが良いんじゃないかなって思ったので、更に設定をしました。

まず、関連記事を表示するためのphpのコードは、
  
[php]
  
<?php related_posts(); ?>
  
[/php]

これを個別ページにのみ表示するには、
  
[php]
  
<?php if (is_single()); ?>
      
<?php related_posts(); ?>
  
[/php]
  
これをsingle.phpの任意の部分に書けば表示されます。

※設定で、[自動投稿]の項目の選択は外しておいてください。

ちなみに、まだ記事数がそこまでないためか、関連記事が表示されていませんｗ(2013/10/11)

追記(2013/09/13)：
  
http://nippondanji.net/blog/wordpress-plugin-yarpp-not-appeared/
  
に記事を表示させる設定の説明がありました。
  
[管理画面]>[表示オプション]>[関連スコア設定]にチェックを入れて、設定をすると表示されるとのこと

 [1]: http://wordpress.org/plugins/yet-another-related-posts-plugin/
 [2]: https://i1.wp.com/peng-note.com/images/2013/10/39d7a487d5879d944205d8a9eb62309d.png