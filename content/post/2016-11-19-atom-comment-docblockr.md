---
title: AtomでPHPやJavaScriptのDocコメントを書くのにdocblockrがめっちゃ便利
author: コニタン
type: post
date: 2016-11-19T07:09:41+00:00
url: /archives/1966
wordtwit_post_info:
  - 'O:8:"stdClass":13:{s:6:"manual";b:0;s:11:"tweet_times";s:1:"1";s:5:"delay";s:1:"0";s:7:"enabled";s:1:"1";s:10:"separation";i:60;s:7:"version";s:3:"3.7";s:14:"tweet_template";b:0;s:6:"status";i:4;s:6:"result";a:0:{}s:13:"tweet_counter";i:1;s:13:"tweet_log_ids";a:0:{}s:9:"hash_tags";a:0:{}s:8:"accounts";a:1:{i:0;s:6:"skd_nw";}}'
categories:
  - クリエイティブ
tags:
  - Atom
  - JavaScript
  - PHP
  - プラグイン

---
最近、業務内でマークアップだけでなく、JavaScriptやPHPを書くことも増えてきました。

再利用とか拡張性とかを考えながらClassを書くことも増えてきたのですが、ガリガリ書いていく上で、やっぱり未来の自分のことを考えるとコメントを書いておいたほうがいいよなと思いコメントも書くようにしています。

何をしているメソッドなのか分かるといいよねと思って調べていると、PHPDocとかJSDocというものがありました。
  
この形式で書いておいたほうが、後々ドキュメントを生成できたり、何を入れたら動いて、何が返ってくるみたいな情報も分かるし良いんじゃないかなと思いそれっぽく書いています。

しかし、やり始めた当初、引数や返り値を一個一個拾って書いていくのは面倒くさいなと数分で投げかけていたのですが、良いパッケージがありました。今回紹介する[docblockr][1]です。

[ドキュメント][1]を見るとまだまだ少ないですが、今使っている言語においては十分です。

よく使うのが、Class内のメソッドに対してのコメントなのですが、先にメソッドを書いておいてコメントを書くために `/**` まで書き改行すると、**メソッド自体の説明と、メソッドで使っている引数や返り値なんかを必要に応じて抽出し、型や説明を書くための雛形を生成してくれます**。
  
<img src="https://i0.wp.com/peng-note.com/images/2016/11/906bdf96418bf40c3ff4d9646239588b.png?fit=408%2C245" alt="%e3%82%b9%e3%82%af%e3%83%aa%e3%83%bc%e3%83%b3%e3%82%b7%e3%83%a7%e3%83%83%e3%83%88-2016-11-19-15-47-10" class="aligncenter size-full wp-image-1971" srcset="https://i0.wp.com/peng-note.com/images/2016/11/906bdf96418bf40c3ff4d9646239588b.png?w=408 408w, https://i0.wp.com/peng-note.com/images/2016/11/906bdf96418bf40c3ff4d9646239588b.png?resize=300%2C180 300w" sizes="(max-width: 408px) 100vw, 408px" data-recalc-dims="1" />

メソッドだけでなく、変数なんかにも使えるようで結構使えるパッケージかなと思います。
  
Docを書くなら入れておいて損は無いパッケージだと思うのでぜひ一度入れて触ってみてください。

[docblockr][1]

 [1]: https://atom.io/packages/docblockr