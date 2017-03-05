---
title: 【感想】WordPressの講義をうけてみた
author: コニタン
type: post
date: 2013-08-10T14:51:05+00:00
url: /archives/105
wordtwit_post_info:
  - 'O:8:"stdClass":13:{s:6:"manual";b:0;s:11:"tweet_times";s:1:"3";s:5:"delay";s:1:"0";s:7:"enabled";s:1:"1";s:10:"separation";s:3:"330";s:7:"version";s:5:"3.0.2";s:14:"tweet_template";b:0;s:6:"status";i:3;s:6:"result";a:0:{}s:13:"tweet_counter";i:1;s:13:"tweet_log_ids";a:0:{}s:9:"hash_tags";a:0:{}s:8:"accounts";a:1:{i:0;s:6:"skd_nw";}}'
categories:
  - クリエイティブ

---
schoo webcampasで行われたWordPressの講義に参加してきました。

schooで行われたWordPressの導入からテーマ作成までの講義に参加してきました。
  
<!--more-->

> <a href="http://schoo.jp" title="schoo webcampas" target="_blank">schoo webcampas</a>って？
  
> Ustreamを用いて講義を受けられるサイトです。IT以外にもいろいろと講義があるようです。

<a href="http://stocker.jp/diary/schoo-wordpress/" target="_blank">「WordPressを始めたい方の第一歩」</a>

ここでこうして日記を書いている時点で導入などは出来る訳ですが、テーマの作成はよく分かっていませんでした。(一度ドットインストールで作りました。)

それと、そろそろデフォルトのテーマから変えたいし、いい機会だということで受けてみました。

講師は、<a href="http://http://stocker.jp/" target="_blank">stocker.jp</a>の庄崎さん。
  
色々な情報を発信してらっしゃったりするこの方、どんな風にするのかなーと思っていると結構丁寧で。
  
とても分かりやすい説明と、手順書の用意などとてもしっかりとした講義だったと思います。

講義はXAMPPによるローカル開発環境と、NetBeansという統合開発環境を使って行いました。
  
受けるまではローカルにWordPressを入れれるとは思ってなかったのでビックリしました。
  
(サーバーを別で用意し、ロボットに登録させないようにして行う物だとばかり…)

XAMPPを使いましたが、別にMAMPでも良かったようです。ただ、XAMPPはWin, Mac, Linux板があるため、説明がしやすかったからこれを用いたようです。

まず、トップページ？を作る。
  
と思いきや、「あらかじめ作っておいたのでダウンロードしておいてください」
  
(さすがに時間の関係か、１から作成ではなかった…)

そんで出来たページのファイルから、header部分、footer部分、sidebarの部分を切りとってそれぞれ別部分として保存。記事の部分はloopっていうファイル名で作成。

なぜloopなのかっていうのが、記事の表示件数だけパーツを使って、そこに記事のデータを当てていくって言う感じらしい。

とりあえずheaderやfooterを一つのファイルとして作り、それを色々なファイルで使い回すってのがWordPress流っぽい。

ただ、そうやって切り分けるだけではtitleや記事のタイトルなどが管理画面などから更新んできないため、PHPを使って少し書き換える事によって、しっかりと変わるようになりました。

ちょっと書けば使えるようになるとは…

まぁここまでずっとコピペなんですけどね。

そんなこんなで説明を聞きつつ作業をし、シンプルなテーマを作る事が出来ました。

昨日講義があって、その内容は一週間無料で見る事が出来るようです。

受けたい人はぜひ！

今後、Illustratorで名刺を作成する講義に参加する予定です。