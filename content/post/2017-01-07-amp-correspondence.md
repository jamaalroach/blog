---
title: 手打ち更新なコラムページをAMP対応したのでその実装手順のメモ
author: コニタン
type: post
date: 2017-01-06T23:05:21+00:00
url: /archives/1997
wordtwit_posted_tweets:
  - 'a:1:{i:0;i:2017;}'
wordtwit_post_info:
  - 'O:8:"stdClass":13:{s:6:"manual";b:0;s:11:"tweet_times";i:1;s:5:"delay";s:1:"0";s:7:"enabled";s:1:"1";s:10:"separation";i:60;s:7:"version";s:3:"3.7";s:14:"tweet_template";b:0;s:6:"status";i:2;s:6:"result";a:0:{}s:13:"tweet_counter";i:2;s:13:"tweet_log_ids";a:1:{i:0;i:2017;}s:9:"hash_tags";a:0:{}s:8:"accounts";a:1:{i:0;s:6:"skd_nw";}}'
categories:
  - クリエイティブ
tags:
  - CSS
  - JavaScript

---
2016年の10月くらいに手探りで対応したのですが、知らないうちに公開されていたのをたまたま発見し、チェックしたらちゃんと認識されていたようなので思い出しながら。

WordPressだとAMPのプラグインを使えば簡単に対応できるそうですが、僕が以前から関わっていたサイトでは、CMSを導入しておらず、HTML手打ちでコラムの更新作業を行っていました。そんな中、ついにAMP対応したいという依頼が来たので対応しました。

## AMP対応するために

今回AMP対応を行うページはampフォルダを作り、既存のファイルを複製したうえで対応していきました。

まず、対応するページの作りを見直しました。
  
JavaScriptが使えないため、JavaScriptありきな実装箇所(ドロワーメニューなど)を、まるっと取るか別の形で再実装。
  
[朝日新聞デジタル][1] さんや [BIGLOBEニュース][2] さんのAMPページではドロワーメニューは無くなっています。

シェアボタンは今回実装しませんでしたが、AMP用の物があるのでそちらに乗り換える。
  
[AMP HTMLのSNSシェアボタンを実装しました &#8211; WEB全般 &#8211; コラム | SEMラボラトリー][3]

AMPページで実装できないものを削ぎ落として、結構スッキリしちゃった状態で対応作業を進めていきます。

## 実際にAMP対応する

実際に作業を進めるうえで、以下のページを参考にしました。

  * [Accelerated Mobile Pages Project][4]
  * [AMPとは～対応HTMLを作ってみてわかったこと～][5]
  * [AMP（Accelerated Mobile Pages）とは？今から導入するための基礎知識と手順書マニュアル｜ferret フェレット][6]

今回は対応するページが有る前提で話を進めますが、もしまっさらな状態から始めるぞって人は以下を。
  
[GitHub &#8211; ampproject/amphtml: AMP HTML source code, samples, and documentation. See below for more info.][7]

### headタグ周り

head タグの中身はごっそり削って以下のようにしました。(ここからもう少し追加します)

    <!DOCTYPE html>
    <html AMP lang="ja">
    <head>
      <meta charset="utf-8">
    　　<title>ページのタイトル</title>
      <link rel="canonical" href="非AMP対応の同じ内容のページのファイルパス" >
      <meta name="viewport" content="width=device-width,minimum-scale=1,initial-scale=1">
      <meta name="keywords" content="ここにキーワード">
      <meta name="description" content="ここにページの説明">
      <style amp-boilerplate>body{-webkit-animation:-amp-start 8s steps(1,end) 0s 1 normal both;-moz-animation:-amp-start 8s steps(1,end) 0s 1 normal both;-ms-animation:-amp-start 8s steps(1,end) 0s 1 normal both;animation:-amp-start 8s steps(1,end) 0s 1 normal both}@-webkit-keyframes -amp-start{from{visibility:hidden}to{visibility:visible}}@-moz-keyframes -amp-start{from{visibility:hidden}to{visibility:visible}}@-ms-keyframes -amp-start{from{visibility:hidden}to{visibility:visible}}@-o-keyframes -amp-start{from{visibility:hidden}to{visibility:visible}}@keyframes -amp-start{from{visibility:hidden}to{visibility:visible}}</style><noscript><style amp-boilerplate>body{-webkit-animation:none;-moz-animation:none;-ms-animation:none;animation:none}</style></noscript>
      <script async src="https://cdn.ampproject.org/v0.js"></script>
    </head>
    

雷の絵文字を付けるとか付けないとか諸説有るようですが、[テンプレート][8]に合わせて、htmlタグの箇所に amp 属性を追加しています。

head の閉じタグ前で、style の記述と script の読み込みを行っていますが、これはそれぞれAMP用のものなので、おまじないだと思って入れておきます。

ogp 周りは canonical で指定した非AMP対応のページを見に行くという話を聞いたのでごっそり削りました。

### CSSの読み込みを追加する

AMP対応を行うページでは link タグを使った CSS ファイルの読み込みができないため、amp-custom 属性を付けた style タグを使って直接書き込む必要があります。

最初はpugを使ってマークアップをしつつ、[gulp-inline-sourceモジュール][9]を用いてstyleタグ内に書き出すかーと思っていたのですが、なんだか上手くいかなかったので模索していたのですが以下で出来ました。なんというか禁じ手感します。
  
ただ、後日見た目の修正が発生した場合でも、一気に全ファイルに適応出来るのでその点では良いのかなと。

    <style amp-custom>
      <?php include($_SERVER['DOCUMENT_ROOT'] . '/css/amp_style.css'); ?>
    </style>
    

### 画像の読み方を変更

img タグでの読み込みが出来ないため、 amp-img というタグを使用します。また、 layout=&#8221;responsive&#8221; を付与することで、レスポンシブな画像にすることもできます。

    <amp-img src="responsive.jpg" width="527" height="193" layout="responsive">
    </amp-img>
    

### JSON-LDで構造化データの記述

構造化データを使って記事の情報を伝えてあげる必要があるようなので、以下のようにJSON-LDで書いた構造化データをhead内に書き込みました。

    <script type="application/ld+json">
      {
        "@context": "http://schema.org",
        "@type": "NewsArticle",
        "mainEntityOfPage": "非AMP対応の同じ内容のページのURL",
        "headline": "記事のタイトル",
        "datePublished": "2016-10-01T10:00:00+09:00",
        "dateModified": "2016-10-01T10:00:00+09:00",
        "description": "ページのdescription",
        "author": {
          "@type": "Person",
          "name": "ページの作者名"
        },
        "image": {
          "@type": "ImageObject",
          "url": "サムネイル画像のファイルパス(ドメインを含んだ絶対パス)",
          "width": 640,
          "height": 427
        },
        "publisher": {
          "@type": "Organization",
          "name": "公開している会社・団体などの名前",
          "logo": {
            "@type": "ImageObject",
            "url": "公開している人のロゴなど",
            "width": 600,
            "height": 60
          }
        }
      }
    </script>
    

image は記事のサムネイルとして設定している画像の情報を記述します。
  
publisher で指定している中身は、検索結果のカルーセル表示の際に表示されます。画像は主にサイトやサービスのロゴを指定する事が多いようです。
  
画像のサイズは仮で入れているものなのでもう少し調整する事ができるかと。

### チェック方法

チェックは主にこの2つを使えばいいかなーと。

  * Google Developer Tools
  * 構造化データテストツール

#### Google Developer Tools

製作時に1番手軽なのは　Google Developer Tools　を使った方法かと思います。

AMP対応作業を行うページで、URLの末尾に #development=1 を入れてページにアクセス。
  
Consoleに以下が出ていればOKです。

Powered by AMP ⚡ HTML – 〜〜〜〜
  
AMP validation successful.

表示されていない場合は、エラーが出ていると思うのでそれを修正しましょう。
  
稀に、この表示があるけど対応出来ていない場合があるそうです。

#### 構造化データ テストツール

Google が公開している構造化データ テストツールを用いて、JSON-LDで記述した構造化データのチェックを行う事ができます。
  
[構造化データ テストツール][10]

## やってみて

大変そうだなーと思ってビビっていたのですが、驚くほど簡単に実装出来たので驚きました。
  
また、JavaScriptが使えないのでやれること狭まるなーと思っていたのですが、Google Analyticsで計測ができたり、シェアボタンが設置出来たり、YouTubeの動画が貼れたりとコラムやニュースのページでやりたいことって意外とやれちゃうのでいいじゃんって思いました。

 [1]: http://www.asahi.com/sp/
 [2]: https://news.biglobe.ne.jp/
 [3]: http://www.oosaka-web.jp/column/web/160527/
 [4]: https://www.ampproject.org/docs/get_started/create
 [5]: https://www.brain-solution.net/blog/seo/amp-html/
 [6]: https://ferret-plus.com/4005
 [7]: https://github.com/ampproject/amphtml
 [8]: https://www.ampproject.org/docs/get_started/create/basic_markup
 [9]: https://www.npmjs.com/package/gulp-inline-source
 [10]: https://search.google.com/structured-data/testing-tool/u/0/