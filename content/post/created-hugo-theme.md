+++
title = "Hugoのテーマを作ってテーマのギャラリーで公開されました"
description = "Hugoのテーマを初めて自作して、申請し公開するところまでいけました"
categories = ["クリエイティブ"]
tags = ["Hugo"]
date = "2017-09-07T21:20:44+09:00"
image="/images/common/hugo.jpg"
author = "Daisuke Konishi"
+++


Hugoでテーマを作ったのですが、申請して公開までいけました。

## 実際に作ったテーマ
Hugo Gentoo Themeという名前でテーマを作りました。
[d-kusk/hugo-gentoo-theme: Hugo theme](https://github.com/d-kusk/hugo-gentoo-theme/)

こういうの何をテーマに作ろうか毎度悩むんですが、会社マシンのデスクトップの壁紙がジェンツーペンギンに変わったので、Gentooという名前にしました。前後のHugoとThemeはたまたま見かけたのでつけたんですが、別に要らないみたいですね…。
配色の感じも写真から色取って、ヘッダーを頭に、コンテンツ部分を体にしたんですがジェンツーらしさが全くないというか出せなかったです。

### CSSフレームワークのBlumaを採用
楽してサクッとやりたいと思ったので[Bluma](http://bulma.io/)というフレームワークを入れてみました。
ぶっちゃけ要らなかったです。元気あればそのうち抜くかもしれない。

Bluma自体は2年前くらいかな Twitterで流れて来たときに使って以来でした。
色の感じがなんとなく好きなのとなんとなくそのまま使えそうなコンポーネントが幾つかあったのですが、今思い返すとヘッダーくらいしか使ってないんじゃないかな。

### メニューを設定から変更可能に
前使っていたテーマが ``config.toml`` から自由に変えれて地味に便利だったのでこの方式を採用しました。
Aboutページなんかをメニューに入れるときには ``page/about.md`` 内のmenuで設定するみたいなのも見かけたのですが、1個1個ファイル開いて変更するのもなんかやだなーと思ってのでこの方式です。

### JSON-LDを入れてみた
テーマにJSON-LDを組み込んでみました。

前使っていたテーマにもこっそり仕込んでいたのですが、せっかくなので入れてみました。
記事詳細ページなんかに入れてます。

ただ、画像使わないから設定してなかったり、いくつか足りない項目があって完全ではないのですが…。
そのうち直します。

## 作るときのすゝめ
作るときの環境みたいなものとかサンプルの記事とかどうしようかなと思っていたのですが、ちゃんと用意されていました。
[gohugoio/hugoBasicExample: Example site to use with Hugo & Hugo Themes](https://github.com/gohugoio/HugoBasicExample)

ここで以下のコードを叩いてスタートすると始めるのに必要なものが大体揃います。

```
$ hugo new theme [name]
```

作るときの概要はここに載っていますが、実際はドキュメントのTemplatesとかVariablesを見ることのほうが多かった記憶があります。
[Hugo | Create a Theme](https://gohugo.io/themes/creating/)

## ギャラリーへの申請
Hugoのテーマは申請すると、[Hugo Themes](https://themes.gohugo.io/)に公開されるのですが、そこに公開してもらうために申請とかレビューが必要です。

申請方法や必要なものはここのREADMEに載ってます。
[gohugoio/hugoThemes: All Hugo themes](https://github.com/gohugoio/hugoThemes)

色々足りなくて指摘されました…。調べたりてなくて申し訳無さ。

---

もしHugoを触る機会があれば、ぜひ実際に使ってみてIssueください。
