+++
title = "Next.jsを触ってみたので所感"
description = "仕事で使うと良さそうだなーって思う案件の話が気かけているので様子見がてら触ってみた。"
categories = ["クリエイティブ"]
tags = ["React", "Next.js"]
date = 2017-11-08T12:18:15+09:00
author = "Daisuke Konishi"
+++

仕事でこの辺使うチャンスではーと思ったので今更感あるけど、とりあえず触ってみた。

React って環境構築めんどくさいイメージで、create-react-app 使うことがちょくちょくあったんだけど、Next.js ならReactと一緒にとりあえず入れるだけでなんとかなるみたいな感じだった。ありがたや

``` bash
$ npm i —save next react react-dom
```

``node_modules`` 見たら、webpack とか Babel とかその辺まるっと入ってた。

## ページを用意
``pages/`` に index.js と about.js を作成する。  
中身はこんな感じ。

``` js
import React from 'react'
export default () => (
  <div>
    <h2>about</h2>
    <p>Welcome to next.js!</p>
    <img src="/static/img-penguin.jpg" />
    <a href="/">back to top</a>
  </div>
)
```

画像みたいな静的ファイルは、``static/`` に置いて管理するみたい。  
なので、ファイルパスも上みたいな形になる。

実際に動かすとこんな感じ
[![https://gyazo.com/a85551cbb5b678b3c3286c415d24b019](https://i.gyazo.com/a85551cbb5b678b3c3286c415d24b019.gif)](https://gyazo.com/a85551cbb5b678b3c3286c415d24b019)

index と about でレイアウトが違うのはデフォルトでそういう仕様なんかな。  
一瞬404になるのはJSの読み込みとかレンダリングの関係な気がする。この辺は後に解決方法が分かった。(prefetchの話)

## headタグ周り
``next/head`` を import して、<Head> 内に記述すると **記述した内容が既存のものに追加される**って感じみたい。デフォルトが charset しかないから必要に応じて要る分を自分で追加って感じ。  
全ページでお決まりのセットがあるならhead用のコンポーネント作って読み込むのがいいかもしれない。

他のbody内に入れたい要素と一緒に書いたのにheadタグの中に移してくれるのえらい。

## Linkの設定
上の例だといつもみたいにaタグでリンクを入れていたんだけど、nextに入ってる next/link を使うことでクエリで設定したいものを書いておいて、クエリ文字にしてくれたり、

``` js
import Link from 'next/link'

export default () =>
  <div>
    Click{' '}
    <Link href={{ pathname: '/about', query: { name: 'Zeit' } }}>
      <a>here</a>
    </Link>{' '}
    to read more
  </div>
```

prefetch を付けることで前もってデータを読み込むお陰で、早く遷移できたりっていうのは魅力的だった。

``` js
import Link from 'next/link'

export default () =>
  <nav>
    <ul>
      <li>
        <Link prefetch href="/">
          <a>Home</a>
        </Link>
      </li>
    </ul>
  </nav>

```

※コードは[github](https://github.com/zeit/next.js/)から

push とか replace がよく分からんかったからもう少し見てみよう。

## ざっくり一通りやってみて
とりあえずgithubのページ見ながらざっくり触ってみたけど、Link周りのprefetchがいいなって思った。早い。
ただ、ガンガン使っていってオッケーにはならん気がするし、使い所は探っていきたい。

あと、コンポーネントをどこで管理するかも少し気になったんだけど、[FRONTEND CONFERENCE 2017 - Reactハンズオン](https://github.com/fand/react-hands-on/)だと ``pages/`` と同じくルートに ``components/`` を作っていた。まぁそうだよね。

ReactとかVueあたりってなんか使いそうだしもう少し触ってみないとなー

## 参考にしたもの
[zeit/next.js - github](https://github.com/zeit/next.js/)