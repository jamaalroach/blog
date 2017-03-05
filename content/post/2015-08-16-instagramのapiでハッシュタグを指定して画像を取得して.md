---
title: instafeed.jsを使ってInstagramのAPIでハッシュタグを指定して画像を取得してみた
author: コニタン
type: post
date: 2015-08-15T23:53:58+00:00
url: /archives/1678
wordtwit_post_info:
  - 'O:8:"stdClass":13:{s:6:"manual";b:0;s:11:"tweet_times";s:1:"1";s:5:"delay";s:2:"15";s:7:"enabled";s:1:"1";s:10:"separation";i:60;s:7:"version";s:3:"3.7";s:14:"tweet_template";b:0;s:6:"status";i:2;s:6:"result";a:0:{}s:13:"tweet_counter";i:3;s:13:"tweet_log_ids";a:2:{i:0;i:1683;i:1;i:1684;}s:9:"hash_tags";a:0:{}s:8:"accounts";a:1:{i:0;s:6:"skd_nw";}}'
wordtwit_posted_tweets:
  - 'a:2:{i:0;i:1683;i:1;i:1684;}'
categories:
  - クリエイティブ
tags:
  - jQuery
  - プラグイン

---
最近友達が次々にInstagramを使い始めて、色々と写真撮って楽しんでいます。

今回触ってみたキッカケは、大学の先生が「Instagramを使ってフォトコンテストをやってみたいんだよね」って(たしか)言っていたことです。

## アプリケーション登録

<a href="http://instagram.com/developer/" target="_blank">http://instagram.com/developer/</a>でアプリケーションを登録します。

流れとしては、

  1. Register Your Applicationをクリック
  2. 右上の新しいアプリを登録ボタンをクリック
  3. アプリケーション名などの情報を登録。
  4. CLIENT IDやREDIRECT URLなどの情報が表示される。

4.で表示されるものは、**アクセストークンの取得**や実際に**アプリで使う**ものです。

この辺りのアプリケーションの説明は色んな記事で紹介されているのでそこを。

## instafeed.jsで情報を取得してみる

この<a href="http://instafeedjs.com" target="_blank">instafeed.js</a>というjQueryのプラグインがかなり使いやすくて、設置も簡単なうえ下記を指定して情報を取得出来るようです。

  * 人気のある画像
  * ハッシュタグ
  * 位置情報
  * ユーザー

人気のある画像やハッシュタグなんかは使いやすそうですね。

また画像の他以下のものが取得できます。

  * 画像のリンク
  * 投稿者コメント
  * likeの数
  * コメント数
  * 撮影した場所(位置)情報
  * ユニークID
  * 画像のjsonオブジェクト

### 使い方

    
        :
        <body>
            <ul id="instafeed"></ul>
            <script src="http://ajax.googleapis.com/ajax/libs/jquery/1.8.3/jquery.min.js"></script>
            <script type="text/javascript" src="path/to/instafeed.min.js"></script>
            <script type="text/javascript">
                var feed = new Instafeed({
                    get: &#039;tagged&#039;,
                    tagName: &#039;awesome&#039;,// 取得したいハッシュタグ名
                    links: true,
                    limit: 20,// 取得する数
                    resolution: &#039;low_resolution&#039;,
                    template: &#039;<li><a href="{{link}}"><img src="{{image}}" alt="{{caption}}"></a></li>&#039;,
                    clientId: &#039;Instagram APIで取得したクライアントIDをココに&#039;
                });
                feed.run();
            </script>
      </body>
    </html>
    

あとはこれをCSSで整形すればOKですね。驚きの簡単さ。

templateというオプションで情報を表示する際のテンプレートを指定できるので上の様に指定すると画像とそのリンクが表示されます。

その他詳しくは<a href="http://instafeedjs.com" target="_blank">instadeed.jsのサイト</a>を御覧ください。

## 注意

今回はJavaScriptを使って情報を取得しましたが、JavaScriptで全て行うとクライアント側にファイルが見えてしまうため、**アクセストークンなんかも見えちゃって良くない**んだとか。**認証の辺りをPHPなどのサーバーサイドでやると良い**らしい。
  
詳しくは下記記事を。<aside class="ref"> 参考: 

<a href="http://syncer.jp/instagram-api-matome" target="_blank">Instagram APIでwebサービスを作りたい全ての人に向けて書きました</a>
  
</aside> 

## まとめ

一応パッと思いついたやりたかったことは出来ました。
  
あとLike押せるといいんですけどね…　それは出来なさそうなので他の手を使ってみます。