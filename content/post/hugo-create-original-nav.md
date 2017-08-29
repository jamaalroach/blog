+++
author = "Daisuke Konishi"
date = "2017-08-30T02:58:06+09:00"
tags = ["Hugo"]
categories = ["クリエイティブ"]
description = "Hugoでメニューに表示する内容をconfig.tomlから設定し、絞り込んで出力する方法"
title = "Hugoでオリジナルのメニューを作って絞り込んで出力する方法"
draft = true
+++

Hugoでテーマを作る中で、自分で指定した項目だけメニューに出すみたいなことをしたかった。

テーマを作る上で、以下を使っており、これでチェックを行うと、テスト側でメニュー用に追加された不要なデータが表示されてしまう。  
[gohugoio/hugoBasicExample - Github](https://github.com/gohugoio/hugoBasicExample)

そこで、今回は自分が表示したいページを ``config.toml`` から設定して、絞り込んで出力するまでをやってみたのでその覚書。

## 環境

- Hugo v0.19

## メニューに項目を追加する
Hugoでメニューに項目を追加するときは、以下のコードを ``config.toml`` に記述する。

```
[[menu.main]]
    name = "About"
    url = "/page/about/"

[[menu.main]]
    name = "Contact"
    url = "/page/contact/"
```

指定できる値は以下を参照。  
[Hugo | Menus](https://gohugo.io/content-management/menus/)


## 出力する項目を絞り込む
メニューの出力には ``range`` を使ってメニューの値をループさせることで出力する。

```
<ul>
{{ range .Site.Menus.main }}
  <li>
    <a href="{{ .URL }}">
      {{ .Name }}
    </a>
  </li>
{{ end }}
</ul>
```

この時 ``where`` 句が使えて、この ``where`` 句はSQLのものと同じような使い方ができるらしい。

### 参考
- [Hugo | Logic (range)](https://gohugo.io/templates/introduction/#logic)
- [Hugo | where](https://gohugo.io/functions/where/)
- [SELECT構文：WHEREで検索条件を設定する| 第3章　SQL構文 | [Smart]](http://rfs.jp/sb/sql/s03/03_2-2.html)

なので、例えば ``config.toml`` で指定したメニュー項目に ``identifier`` を追加し、以下のように書き換えて

```
[[menu.main]]
    name = "About"
    url = "/page/about/"
    identifier = "global"
```

rangeでフィルタリングすると、identifier が global なモノのみを出力することができる。

```
<ul>
{{ range where .Site.Menus.main ".Identifier" "global" }}
  <li>
    <a href="{{ .URL }}">
      {{ .Name }}
    </a>
  </li>
{{ end }}
</ul>
```

あとは、好きな箇所に設置すれば、グローバルナビゲーションやフッターナビゲーションのようなものも作成できる。
