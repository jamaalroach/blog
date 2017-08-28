+++
author = "Daisuke Konishi"
date = "2017-08-29T00:41:33+09:00"
tags = ["Travis","bash", "git"]
categories = ["クリエイティブ"]
description = "TravisCIを使って、ビルドした後Githubにpushする方法に悩んでいたけどようやくできたので覚書"
title = "TravisCIからGithubに別ブランチでpushするときに色々コケたので覚書"

+++

最近、知り合いが申請して掲載されたこともあり[Hugoのテーマを作ってみている](https://github.com/d-kusk/hugo-gentoo-theme/)のですが、申請したりユーザーがダウンロードする時の事を考えて、必要なファイルと制作用のファイル(Sassとか)を分けたかった。
知り合いがTravisでやっているとの事だったので、いい機会だと思って ~~パクって~~ 触ってみました。

## Travis CIについて
Travis CIについては以下の記事を何度か読んだり、[この間のWordBench京都](https://wb-kyoto.connpass.com/event/61990/)で書き方とか連携・設定あたりはなんとなく理解していたが、なかなか使えずにいた。

参考:

- [GitHubと連携できる継続的インテグレーションツール「Travis CI」入門 - さくらのナレッジ](http://knowledge.sakura.ad.jp/tech/3754/)
- [Travis CI | ド素人のための使い方 (公式ガイドより) - Qiita](http://qiita.com/YumaInaura/items/8021d38cb202950fb18c)

## 今回やりたかった(やった)こと

Hugoのテーマはdevelopで開発。  
ここにpush or PRすることで、Travis CIが走って配布版のファイルを作ってくれて、masterにまとめてくれる(pushする)ところを自動化。

ほんとはテストとかLint走らせたりするんだろうけどねー。


## Travisの設定
別にビルドするものも無いけどなんかできないか探ろうと思ってやってたんだけど、結局めんどくさくなって知り合いのやつ参考にちょっと変えて書いた。

ビルドして、成功したらデプロイのスクリプトを走らせるというもの。
デプロイのスクリプトでは、既存の ``.git`` 、 ``.gitignore`` を削除して、開発用のファイルを削除した後再度リポジトリを作ってcommit&pushするというもの。

詳細は最初の方に載っけたリポジトリを見てほしい。

## Shell Scriptというかコマンド周りで学びがあった

### 変数を定義してるのに未定義
``ambiguous redirect`` というエラーが頻発してpushができなかった。
このエラーはShell Script内で変数を使っていて、未定義なものがあるときに発生するとかって話がStackoverflowによくあがってた。

でも、実際使っていた変数は環境変数で定義していたし、ログを見る限りexportも上手くいっていたので原因は変数じゃなさそうだった。

結果をいうと **改行コードがまざっていた** ことっぽい。すごいハマった。
途中までLFだったのに一部CRLFになっていたので、コピペ危ないなって思った。エディタで変えたらエラーも消えたので多分ここの関係で出てた。

### ログ安全にするためのオプションのようなものがある
Travis CIで実行するとログが残る。更にログはバッジがからビルド画面が見れて、そこから見えてしまう。
なので travis のCLIツールを入れて暗号化させる他、git操作時に ``--quiet`` というオプションを入れて出力しないモードにするらしい。

さらに ``> /dev/null 2>&1`` というコマンドをつけることで出力を無効化できるらしい。
このあたりはこの記事に書いてある。  
参考: [cmd > /dev/null 2>&1」の話 - Qiita](http://qiita.com/sue71/items/cef17fabd180f4121f9e)

## 触ってみて
Travis CIというよりShell Script周りにすごく悩まされたのでおのれShell Scriptという気持ち。

ただTravis CIに触れるいい機会だったので良かったし、別プロジェクトではこれ参考にテストやLint走らせてみたいなと思った。

<blockquote class="twitter-tweet" data-lang="ja"><p lang="ja" dir="ltr">とりあえず▲さんをコントリビューターの欄にぶっこみたいくらい感謝</p>&mdash; こにたん (@skd_nw) <a href="https://twitter.com/skd_nw/status/902199323194122242">2017年8月28日</a></blockquote>
<script async src="//platform.twitter.com/widgets.js" charset="utf-8"></script>


## 参考

- [Travis CIのテストの中でGitHubのレポジトリへpushする](https://rcmdnk.com/blog/2014/10/09/computer-github-travisci/#アクセストークンの暗号化)
- [Travis CI から GitHub へ git push を行う設定 ｜ Tips Note by TAM](https://www.tam-tam.co.jp/tipsnote/program/post11795.html)
