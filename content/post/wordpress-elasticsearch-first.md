+++
date = "2017-04-02T11:23:29+09:00"
tags = ["WordPress","ElasticSearch"]
categories = ["クリエイティブ"]
description = "2017年1月のBench京都でプラグインを使ってWordPressとElasticSearchを連携させる話をしてきた"
title = "WordBench京都でWordPressとElasticSearchを連携させる話をしてきた"
author = "Daisuke Konishi"

+++

1月のWordBench京都は、WordPressに色んなサービスを連携するというテーマで行われたのですが、その中でElasticsearchと連携する話をしました。っていう話をそういえば書いてないわと思って今書いてるわけです。

スライドは<a href="https://speakerdeck.com/dkonishi/wordpressnielasticsearchwolian-xi-sitarapu-falsejian-suo-gajia-su-sitahua">SpeakerDeck</a>であげてます。

## はじめに
もともとElasticsearchを触っていたわけでも無いし、普段から検索周りのものを作ってるってわけではなかったんですが、岡本さんが登壇するとき結構な割合では前を聞いていて、ちょっと気になるなーと思っていたんです。


## Elasticsearchを調べるところから
<a href="https://www.elastic.co/jp/products/elasticsearch">Elasticsearchのサイト</a>を見たり、いくつかのサイトを見ていると、Elastic社の出しているサービス郡の1つで、**オープンソースの分散型RESTful検索/分析エンジン**というのが分かりました。

他にも、以下の特徴が目に止まりました。

* 多くの型をサポートしてる
* 検索が早くて精度が高い
* JSONみたいな感じでデータを扱える
* 位置情報なんかのデータも扱える
* Kiberaという同社開発のツールを使うことでElasticsearchで扱っているデータを可視化できる

GithubのリポジトリやDockerのコンテナの検索なんかで使われてるみたいです。


## WordPressと連携させる

### そもそもなぜ連携？
そもそもなんでWordPressと連携させるのか、検索ってもともとあるじゃんと思っていたのですが、どうやらWordPressの検索がLikeしか対応していないらしく…。

Like検索というのが、

> 検索条件が完全一致しない対象を、一定のルールのもとで抽出する検索方法のこと
> - weblio

結構曖昧な結果になっちゃうみたいです。

なので、Like検索だと

* あんまり精度が良くない
* DBのインデックスが使えないからDBをフルスキャンするため時間がかかり、データ数によっては負荷がすごい
* 条件幾つか指定してAND検索したいときに対応できない

のでElasticsearchを連携させて、検索はそっちでやっちゃおうという感じです。


### Amazon Elasticsearch Serviceを使って連携させる

実際に連携させる上で、Elasticsearchはどうしたらいいんだろうと思って調べたのですが、**自分で立てるか、サービスを使うか** って感じらしいです。  

一度ローカルでやるときにVagrantでやりかけたのですが、少しやってみて自分で立てるのはその後がしんどそうだなと思ってサービスを使う方にシフトしました。

サービスは、以下のどちらかを使うのが良いらしく、今回はAmazon Elasticsearch Searviceを使ってみました。

* <a href="https://aws.amazon.com/jp/elasticsearch-service/" target="_blank">Amazon Elasticsearch Service</a>
* <a href="https://www.elastic.co/jp/cloud" target="_blank">ElasticCloud</a>

連携自体はやってくれるプラグインがあったのでそれを利用しました。

<a href="https://ja.wordpress.org/plugins/wp-simple-elasticsearch/" target="_blank">WP Simple Elasticsearch — WordPress Plugins</a>

連携方法は<a href="http://dev.classmethod.jp/server-side/elasticsearch/wordpress-plugin-wp-elasticsearch/" target="_blank">クラスメソッドさんの記事</a>を参考にしました。

手順はざっくり以下。細かいやり方はちゃんと覚えていないので、上のサイトを見るか調べてください。

1. AES側で使えるように準備
2. プラグインのインストールして有効化
3. 設定画面から1.で作成したものの情報を入力
4. 変更を保存

基本的にはタイトルと本文の情報をElasticsearchに渡すらしいのですが、指定すればカスタムフィールドの情報も渡すことが出来るらしいです。

### 実際に連携してみると…
導入前と導入後で同じ時間帯に同じキーワードで検索を書けたところ、**表示まで5秒かかっていたものが2秒ほどに短縮**する事が出来ました。めっちゃ早いです。


## やってみて
全然深くは触れていないので顔見知り程度なレベルなのですが、実際やってみて得られる恩恵は結構ありそうなので、Elasticsearchはちょっと触ってみてもいいなという気になりました。
