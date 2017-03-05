---
title: D2Draft jade+Sass+Foundationで爆速コーディングに参加してきた
author: コニタン
type: post
date: 2015-05-18T23:26:35+00:00
url: /archives/1601
wordtwit_post_info:
  - 'O:8:"stdClass":13:{s:6:"manual";b:0;s:11:"tweet_times";s:1:"1";s:5:"delay";s:2:"15";s:7:"enabled";s:1:"1";s:10:"separation";i:60;s:7:"version";s:3:"3.7";s:14:"tweet_template";b:0;s:6:"status";i:2;s:6:"result";a:0:{}s:13:"tweet_counter";i:4;s:13:"tweet_log_ids";a:3:{i:0;i:1604;i:1;i:1605;i:2;i:1606;}s:9:"hash_tags";a:0:{}s:8:"accounts";a:1:{i:0;s:6:"skd_nw";}}'
wordtwit_posted_tweets:
  - 'a:3:{i:0;i:1604;i:1;i:1605;i:2;i:1606;}'
categories:
  - 行ってきた
tags:
  - CSS
  - Sass

---
先日行われた、D2D jade+Sass+Foundationで爆速コーディングに参加してきました。

> D2D &#8220;Dev & Design Draft&#8221; 特定の技術やプロダクトに限定せずに、Web制作者が今イチバン気になる情報を知ろうという領域横断型の勉強会シリーズ。 

[Slimを導入した際][1]も「jade良いよ！」っていう声を聞いており興味があったのと、Foundationの使い方で疑問があったので参加してきました。

今回は[CodePen][2]が使われました。Web上でHTML, CSS, Javascriptのコーディングができて、ライブプレビューまで出来ちゃう優れもの。 ちなみにそれぞれ今回使うjadeやSassの他のテンプレートエンジンやCSSメタ言語なんかにも対応しているCofeescriptなんかにも対応しているという

## jade

jadeはHTMLのテンプレートエンジンで、よく聞くHamlとかNode.jsで動いてるらしく、jadeの中でJavascriptのコードが埋め込めるらしいです。

書き方はSlimに似ていて要素(タグ)の山括弧<>を外して、属性なんかは丸括弧()で書いていくものらしいです。
  
書き方に関しては、[Jadeの記法について（あまりまとまっていない） &#8211; Qiita][3]がタイトルに見合わずまとまっているようなのでそちらを御覧ください。

前作ったものもjadeでやりたいなーって人は[html2jade][4]というサービスを使えばHTMLからjadeに変換されるのでオススメ。 ただ、途中の一行で書けるところなんかも1個1個行を分けて書き出されるので、その辺は適宜修正しましょう。

今回はじめてjadeを触りましたが、_書きやすそうな雰囲気やテンプレートを分けれる_ あたりに少し惹かれる部分がありました。

## Sass

今回の参加者の方は何かしらの形でコーディングに関わっている人が多いみたく、Sassについて理解している人も多かったようです。 内容としては、入れ子の話がメインだったように思います。入れ子だけでも使えると少し幸せになれますよね。

こちらも既存のコードは[css2scss][5]というサービスで簡単にSCSS(記法)のコードに変換してくれます。Sass記法派の方は他をあたってください。

## Foundation

最近僕もお気に入りのCSSフレームワーク。 自分の中で、今回は使い方があっているかの確認と疑問の解消でした。

### 変数の値ってどう変えるのがいいの？

変数の値を変更する場合は_setting.scssをいじる。 これまで、変数の値を変えるとなると、コンポーネントのファイルを直接触っていたのですが、この方が楽なのとかバージが。

### 使いたいコンポーネントを_setting.scssのコンポーネントからコメントアウト外して使ってるけどこれでいいの？

むしろ上に書いてあるfoundationをimportするより、ファイルサイズを抑えられるらしい。

### rem-calc() お前は誰だ

A. 引数( ()の中の値 )をremに変換してくれる関数。 この前さわる機会があって、適当に値を変えるも意味がわからずでしたが解消されて良かったです。

## まとめ

今回は新しい技術に触れるだけでなく、既に使っているものの復習が出来て良かったです。

また、懇親会がめちゃくちゃ楽しくて、新しい出会いの他、勉強会を超えた知識を付けることも出来て良かったです。

次回以降のD2Draftの情報は次から <https://d2draft.doorkeeper.jp/>

 [1]: http://peng-note.com/archives/1491
 [2]: http://codepen.io
 [3]: http://qiita.com/sasaplus1/items/189560f80cf337d40fdf
 [4]: http://html2jade.org/
 [5]: http://sebastianpontow.de/css2compass/