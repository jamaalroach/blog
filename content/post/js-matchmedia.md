+++
date = "2017-07-04T23:26:16+09:00"
tags = ["JavaScript"]
categories = ["クリエイティブ"]
description = "JavaScriptでレスポンシブページを作っているときに、特定の幅の時だけ実行する処理をどう組んだらいいのか悩んだのでその覚書"
title = "レスポンシブページで、特定のデバイス幅だけJavaScriptを動作させるときの覚書"
author = "Daisuke Konishi"

+++

レスポンシブページのコーディング時に、スマホビューだけプルダウンにするみたいな要望があって、普段よく対応しているのがPC, SPで出し分けなサイトなので、どういう実装にするのが良いのかちょっと悩んだ。

とりあえず思い浮かんだのはこれ

- ユーザーエージェントで判別
- ``window.innerWidth`` で処理を当てる

ただ、上の方はレスポンシブサイトの場合あまり適さない。
``window.innerWidth`` の方かなーと思っていたけど、スクロールバーの関係で、``innerWidth`` でやると面倒くさいらしい。
参考: [window.matchMedia をそろそろ活用してもいい頃](http://qiita.com/sdn_tome/items/a29b29f5267196a5e4ea)

そこで割りと良さそうなのが、 ``window.matchMedia`` 。

[window.matchMedia - Web API インターフェイス | MDN](https://developer.mozilla.org/ja/docs/Web/API/Window/matchMedia)

## window.matchMediaを使って実装
matchMedia() の引数にメディアクエリの文字列を入れることで、その幅かどうかを判別してくれるみたいなそんな雰囲気。

```
if (window.matchMedia( "(min-width: 400px)" ).matches) {
  /* ビューポートの幅が 400 ピクセル以上の場合のコードをここに */
} else {
  /* ビューポートの幅は 400 ピクセル未満の場合のコードをここに */
}
```
window.matchMedia - Web API インターフェイス | MDN から抜粋


## IE9対応もしやるなら
window.matchMedia がIE9以下は対応していない。
もし対応するなら以下のスクリプトを読み込ませる必要があるのかも。

[matchMedia.js - github](https://github.com/paulirish/matchMedia.js/)


対応しない場合でも、閲覧されるとスクリプトとしては動いてしまうので、以下みたいにすると対応してないブラウザでは動作しないようにできる。

```
if (window.matchMedia) {
  // 対応しているブラウザだけ動作
}
```


## 参考
[[JS] window.matchMedia をつかって JavaScript のコードをレスポンシブに分ける方法](https://memocarilog.info/jquery/6500)
