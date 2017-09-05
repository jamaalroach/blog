+++
tags = ["Hugo"]
categories = ["クリエイティブ"]
description = "Hugoでサイト全体で使われているタグやカテゴリーの一覧のページを作ったのでその覚書"
title = "Hugoでサイト全体で使われているタグやカテゴリーの一覧のページを作る"
author = "Daisuke Konishi"
date = "2017-09-04T22:02:32+09:00"
draft = true
+++


Hugoでのテーマ制作を進めているのですが、サイト内で使われているタグとカテゴリーの一覧ページ(WordPressのウィジェットであるタグクラウドとかカテゴリー一覧みたいなイメージ)を出力する方法がイマイチ分からず、困っていましたがようやく解決したので覚書です。

## バージョン

- Hugo v0.19

## 必要なもの


### config.tomlへの記述
タグやカテゴリーといった分類を使う場合、``config.toml``に以下を記述します。

```
[taxonomies]
  tag = "tags"
  category = "categories"
```

参考: [Hugo | Taxonomies]( https://gohugo.io/content-management/taxonomies/#configure-taxonomies)


### 書き出せるか確認する

初めて使ったのですが、出力できるかは以下のコマンドでできました。

```
$ hugo -F
```

``/public/`` に出力されます。

### ハマったところ
上で書いたconfig.tomlへの記述は早いタイミングで
