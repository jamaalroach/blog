+++
tags = ["Hugo"]
categories = ["クリエイティブ"]
description = "Hugoでサイト全体で使われているタグやカテゴリーの一覧のページを作ったのでその覚書"
title = "Hugoでサイト全体で使われているタグやカテゴリーの一覧のページを作る"
author = "Daisuke Konishi"
date = "2017-09-04T22:02:32+09:00"
+++


Hugoでのテーマ制作を進めているのですが、サイト内で使われているタグとカテゴリーの一覧ページ(WordPressのウィジェットであるタグクラウドとかカテゴリー一覧みたいなイメージ)を出力する方法がイマイチ分からず、困っていましたがようやく解決したので覚書です。

## バージョン

- Hugo v0.19

## 必要なこと

- config.tomlで設定
- (テンプレートの用意)

### config.tomlへの記述
タグやカテゴリーといった分類を使う場合、``config.toml``に以下を記述します。

```
[taxonomies]
  tag = "tags"
  category = "categories"
```

参考: [Hugo | Taxonomies]( https://gohugo.io/content-management/taxonomies/#configure-taxonomies)

### テンプレート(layout/terms.html)を用意する
基本的には、 ``list.html`` が出力されると思って問題ないと思います。
ただ、今回は一覧の出し方(レイアウト)が記事の一覧とは少し違う想定なので、terms.htmlを作成します。
(terms.htmlがあればそちらが、無ければlist.htmlが使用される。)

```
{{ range $key, $value := .Data.Terms }}
    <div class="tags_item">
        <a href="{{ $key | urlize }}">{{ $key }} <span class="tags_number">{{ len $value }}</span></a>
    </div>
{{ end }}
```

これで、 ``/categories/`` にアクセスするとサイト内で使われているカテゴリの一覧が表示されているはずです。
また、 ``tags/`` でも同じようにサイト内で使われているタグの一覧が表示されているはずです。

### 書き出せるか確認する
ファイルの出力は以下のコマンドできます。

```
$ hugo --theme=テーマ名
```

``/public/`` に出力されます。

おそらく ``/public/categories/index.html`` や ``/public/tags/index.html`` が作成されているかと思います。
僕はなぜか出力されず、 ``hugo searver -t テーマ名`` で見ているときは見れるみたいな状況でした。

実際に公開してみると見れたので何かしらやり方が違うのか…も？

## 参考

- [[Hugo] タグを追加する](https://code-house.jp/2016/08/19/hugotaxonomy/)
- [静的サイトジェネレータHugoを使ったサイト構築（Taxonomy編） · feedtailor Inc. スタッフブログ]( http://staff.feedtailor.jp/2016/06/29/hugo_11/)


## やってみて
設定自体はすぐに出来ていたのですが、なかなかできず、 **サンプルの記事に入っている項目が悪さをしている** ビルドコマンドで確認できなかったり色んなところで引っかかりました。

今回は個別でページを用意しましたが、サイドバーがあるようなテーマだとそこに生成すれば、各ページから内部リンクが貼れていいのかもしれませんね。
