+++
author = "Daisuke Konishi"
date = "2017-08-30T02:58:06+09:00"
tags = ["Hugo"]
categories = ["クリエイティブ"]
description = "Hugoでメニューに表示する内容をconfig.tomlから設定し、それを出力する方法"
title = "Hugoでオリジナルのメニューを設定し出力する方法"
+++

Hugoでテーマを作る中で、 **自分で指定した項目だけメニューに出す** みたいなことをしたかった。

テーマを作る上で以下を使っており、これでチェックを行うとテスト側でメニュー用に追加された不要なデータが表示されてしまう。  
[gohugoio/hugoBasicExample - Github](https://github.com/gohugoio/hugoBasicExample)

そこで、今回は自分が表示したいページを ``config.toml`` から設定し、それを出力するまでをやってみたのでその覚書。

## 環境

- Hugo v0.26

## メニューに項目を追加する
Hugoでメニューに項目を追加するときは、以下のコードを ``config.toml`` に記述する。

```
[[menu.global]]
    name = "About"
    url = "/page/about/"

[[menu.global]]
    name = "Contact"
    url = "/page/contact/"

[[menu.utility]]
    name = "Access"
    url = "/page/access/"
```

指定できる値は以下を参照。  
[Hugo | Menus](https://gohugo.io/content-management/menus/)

メニューを表示したい箇所で以下のコードを入れることで、設定した項目が出力される。

```
<ul>
{{ range .Site.Menus.global }}
  <li>
    <a href="{{ .URL }}">
      {{ .Name }}
    </a>
  </li>
{{ end }}
</ul>
```
