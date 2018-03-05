+++
date = "2017-03-14T00:12:46+09:00"
title = "WordPressからHugoに移行しました"
description = "ブログに使うシステムをWordPressからHugoに移行したので、特にシステムの移行部分とページの生成までの覚書です"
categories = ["クリエイティブ"]
tags = ["Hugo", "WordPress"]
image="images/common/hugo.jpg"
author = "Daisuke Konishi"
+++


ブログに使うシステムをWordPressからHugoに移行したので、特にシステムの移行部分とページの生成までの覚書です。

## 大体の流れ
1. Hugoの環境を作る
2. WordPressからデータをエクスポートする
3. Hugoにファイルを追加してページを生成する


## 環境
今回移行した環境は以下です。

* WordPress v4.7.3
* Hugo v0.19

## 1.Hugoをインストールしてサイトを作る
まずはHugoでサイトを運用できるように準備します。

Macを使っている人の場合、以下でインストールからサイトの生成まで出来ます。

```
$ brew update && brew install hugo

$ hugo version

$ hugo new site
```

この辺りは全て<a href="https://gohugo.io/overview/quickstart/" target="_blank">Quick Start</a>に載っているので参照してください。

別のOSの人は分からないですが、元気出してください。


## 2.WordPressから現状のデータをエクスポート

エクスポートには、以下のプラグインを使いました。

<a href="https://github.com/SchumacherFM/wordpress-to-hugo-exporter" target=_blank"">SchumacherFM/wordpress-to-hugo-exporter</a>

このプラグインを ``wp-content/plugins/`` に設置して、有効化した後、エクスポートを実行するだけです。
ほとんど投稿だったので楽でした。

エクスポートされたファイルはHugoのディレクトリ構成で吐き出され、中身も自動的にHugoの形式に整形されました。

### ディレクトリ構造はちゃんとHugoに合わせてくれる

```
.
├── about/
├── config.yaml
├── post/
└── wp-content/
```

config ファイルが .toml ではなく .yaml なのが少し気になりましたが、toml、yaml、jsonの順で参照してくれるそうなので、yamlファイルでも大丈夫そうです。ただ、テーマファイルなんかはtomlファイルが多いのそちらに合わせておく方が、書き方も同じで管理しやすいかなと思います。  
<a href="https://gohugo.io/overview/configuration/" target="_blank">Hugo - Configuring Hugo</a>

また、``wp-content/`` の中には画像が入っていました。

### 記事の中身


```
---
title: ブログ始めました。
author: コニタン
type: post
date: 2013-05-28T07:55:59+00:00
url: /archives/5
categories:
  - 雑記

---
WordPressを使ってみたく、ブログを作ってみました。

これから色々とデザインをいじったりしていく予定です。
    :
```

あとはこれらのまるっとHugoのプロジェクト内のに入れるだけ。

参考:
<a href="http://creative-tweet.net/blog/2015/10/good-bye-wordpress.html" target="_blank">WordPressからHugoへ移行して、ビルドとデプロイを自動化した話</a>


## 3.ページを生成する
記事のデータも揃ったので、ページを生成してみましょう。

とりあえず<a href="http://themes.gohugo.io/" target="_blank">この辺り</a>から適当にテーマを入れておきます。(themes/に配置)

どんな見た目になるかのプレビューは以下で。
```
$ hugo server --theme=テーマ名
```

プロジェクトのルートディレクトリで以下のコマンドを叩くことで生成出来ます。  
生成先は、``public/``です。

```
$ hugo --theme=テーマ名
```

## まとめ
乗り換えたことで、スマホからちょこっと記事を触ったり、予約投稿と自動投稿/ツイートが出来なくなりましたが、また違ったシステムを知れたので良かったです。  
ちょくちょく触りながら公式でテーマ公開までいきたいですね。
