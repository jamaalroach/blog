+++
title = "Hugoのブログ用テーマ、minimageが公式のテーマ配布サイトに掲載されました"
description = "このブログで使用しているminimageというHugoのブログ用テーマが公式のテーマ配布サイトに掲載されました。"
date = 2018-08-05T05:58:02+09:00
image = "images/common/hugo.jpg"
tags = ["Hugo"]
+++


つい昨日、このブログで使用している(2018.08.05現在) <a href="https://github.com/d-kusk/minimage" target="_blank">minimage</a> というテーマがHugoの公式のテーマ配布サイトに掲載されました。

<blockquote class="twitter-tweet" data-partner="tweetdeck"><p lang="en" dir="ltr">Minimage is a responsive blogging theme with an emphasis on thumbnails. Made by <a href="https://twitter.com/skd_nw?ref_src=twsrc%5Etfw">@skd_nw</a>.<a href="https://t.co/ajmcuxhNuL">https://t.co/ajmcuxhNuL</a></p>&mdash; GoHugo.io (@GoHugoIO) <a href="https://twitter.com/GoHugoIO/status/1025718148077678594?ref_src=twsrc%5Etfw">August 4, 2018</a></blockquote>
<script async src="https://platform.twitter.com/widgets.js" charset="utf-8"></script>


作ってたのも結構前だし、申請自体もかなり前に出してすっかり忘れていたのですが、一昨日の夜くらいにHugoの中の人からレビューのコメントがついて、修正点を上げてもらったのをキッカケに申請作業を再開しました。  
レビューをしてくれた方は返信も早いしめっちゃ丁寧で助かりました！あったけー

## 特徴
デザインの元ネタはある人のブログを見たのがキッカケだったんですが、Hugoのテーマをざっと見た所同じ形式のものは見つからなかったので作ってみました。

各種設定なんかは <a href="https://github.com/d-kusk/minimage/blob/master/README.md" target="_blank">README</a> や <a href="https://github.com/d-kusk/minimage/tree/master/exampleSite">exampleSite/</a> を見てください。

### サムネイルが設定可能
ページの ``Params`` に ``image`` というパラメーターを設けて、ここに記述されているパスを元に、一覧や詳細ページでサムネイルを設定出来るようにしました。(共通のものが出力されます)
ただ、デザインの関係上、一覧ページでは **大きな画像が設定されていれも中央だけ** しか表示されません。  

また、一覧ではサムネイルが無い場合はフォントを黒に、あれば白に変えていますが、画像の色を判別しているわけではないので、背景が白系の画像を設定すると見えなくなってしまいます。必要に応じてスタイルの変更を行ってください。

最後の修正では、ここでのパスの指定の仕方がメインでした。  
最初は一部相対パスを使って組んでいたみたいなんですが、「投稿側ではルートパスの頭のスラッシュが無い形で書いて、テンプレート側で ``absURL`` をつけよう」って話をされてそれにしました。

Hugoではビルド時に ``static/`` の中や ``content/`` 内なんかののファイルを探しにいってくれるらしいのですが、生成時のパスが少し変わってくるので、記事内でのサムネイルに設定するファイルパスは注意が必要です。

### メニューが設定可能
サイト右上のハンバーガーメニューからオーバーレイでメニューが開くようにしました。
最初の製作時には無かった機能なんですが、運用していく上でほしいなと思ったので追加しました。おかげで ``exampleSite/`` の ``config.toml`` の更新を忘れていてレビュワーの方からツッコミをもらいました(苦笑)

メニューの項目設定は、 ``config.*`` ファイルから行えます。
このブログでは、カテゴリーとタグのページをメニューに設定していますが、 ``config.toml`` ではこんな感じで設定を書いています。

```
[[menu.global]]
    name = "カテゴリ"
    url = "/categories/"
```

こんな感じでタグやカテゴリなんかの一覧ページを表示するもよし、Aboutページとか問い合わせページみたいなページ単体をピックアップして表示することにも使えるんじゃないかなって思います。

### JSON-LDを自動生成
前回の <a href="https://github.com/d-kusk/hugo-gentoo-theme" target="_blank">hugo-gentoo-theme</a> の時にも追加していますが、記事詳細で JSON-LD を生成するようにしています。  

実際入れるとGoogleのインデックス周りで嬉しかったりするの？というところは実際の所分からないのです。  
が、前回のテーマで入れた際に若干検索が引っかかりやすくなったり微妙に順位が上がった気がしたので今回も入れています。

使用される方に何かを設定してもらう必要は全く無く、記事を書いてビルドするだけで記事内に JSON-LD を埋め込んでくれます。

### Google Analyticsのコードも生成可能
Hugoのデフォルトで備えているテンプレートを使用するようになっているため、 ``config.*`` で Google AnalyticsのIDを設定するだけで、Google Analyticsのコードを生成してくれます。  
※ただし、Hugo本体に入っているものなため、Google Analyticsのコードが変わった際に対応することができません。Hugo本体のリリースの確認とアップデートを行ってください。

## 作ってみて
途中レビューが止まって諦めムードだったんですけど、掲載までいくとやっぱ嬉しいですね。  
周りでHugo使ってる人が全然居ないんですが、なんかの機会あれば使ってもらえたらなって思います。

あと、TwitterのLikeもいいけどStarも忘れずに！

## ぜひ使ってみてください
ぜひ一度使ってみてください。  
何か問題や提案があれば github の <a href="https://github.com/d-kusk/minimage/issues">Issue</a> まで。

<a href="https://github.com/d-kusk/minimage" target="_blank">minimage - Github</a>