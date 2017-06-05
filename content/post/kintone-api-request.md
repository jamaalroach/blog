+++
tags = ["PHP", "API", "kintone"]
categories = ["クリエイティブ"]
description = "PHPでkintoneのREST APIを叩いてデータを拾うところまでをやってみた"
title = "PHPでkintone REST APIにリクエストを送る"
author = "Daisuke Konishi"
date = "2017-06-06T00:06:16+09:00"

+++

## はじめに
1月のWordBench京都でkintoneと連携する話を聞いてからちょっと気になってた。  
なかなか使えそうな案件来ないから、たまーに[サンプルアプリ](https://kintone-sol.cybozu.co.jp/apps/)を見てたんだけど、実は意外と色んなシーンで使えるんじゃ？って気がしたので、社内で喋ったり先行して触ってみてる。

といってもkintone側をガシガシ触るってわけじゃなくて、サンプルアプリ入れて、APIトークン発行して、API叩くみたいなそういうのやってる。

ついでに、サンプルで提示しやすいようにPHPも触ってる。

## ライセンスの取得
無料の開発者向けDeveloperライセンスを取得して触ってる。  
[ここ](https://developer.cybozu.io/hc/ja/signin?return_to=https%3A%2F%2Fdeveloper.cybozu.io%2Fhc%2Fja%2Farticles%2F200720464)から申請ができて、数日後にメールで届く。


## アプリを登録する
先述したサンプルアプリで、使いそうだなーって思ったショップマイスタっていう店舗管理のアプリを入れてみた。
自分でアプリを作ることも出来るんだけど、こういったサンプルアプリを入れてサクッと使えるのも割りと魅力的。


## APIトークンを発行
APIにリクエストを投げるには幾つか方法があるみたいなんだけど、ユーザーIDとパスワードって投げたくないので、APIトークンを使った方法にした。

アプリをインストールした後にアプリの設定からAPIトークンを発行する。やり方は以下。

[APIトークンを生成する | kintone ユーザーヘルプ](https://help.cybozu.com/ja/k/user/api_token.html?utm_medium=kintone&uiver=new)

トークンを発行するページにリクエストの送信先URLは書いてあって、以下の形式(記事作成時)

```
https://(サブドメイン名).cybozu.com/k/v1/(コマンド名).json
```



## リクエストを投げるプログラムを書く

上のURLにリクエストを送るプログラムを作る。  
手探りなんだけど一応書けた。

[d-kusk/kintone-shop](https://github.com/d-kusk/kintone-shop/blob/master/request_shop_data.php)

クラス化とか関数化とかしてないし、値のチェックとかもサボったのであれだけど、流れというかは分かるのかも。

[前回の記事](https://blog.daisukekonishi.com/post/php-load-library-env.html)で、「APIキーとか載せたくないよね」ってやっていたのは今回のこれのため。  
今回はリクエストヘッダーの書き方が学びだった。よくよく考えるとそういうの分かんなかったし。

これ組んでる途中で、実はサンプルが公開されてる事に気付いて辛かった。

[HTTP_Request2を利用したkintone REST APIの扱い方 – cybozu developer network](https://developer.cybozu.io/hc/ja/articles/202657614-HTTP-Request2%E3%82%92%E5%88%A9%E7%94%A8%E3%81%97%E3%81%9Fkintone-REST-API%E3%81%AE%E6%89%B1%E3%81%84%E6%96%B9)

(PHPって調べてるとちょくちょくライブラリ使う感じのコードが出てくるけど使って行くほうがいいんかな？)

## まとめ
簡単なモノ作るならわりとサクッとできそうだし、情報の修正作業なんかもお客さんができちゃうようなシステムが作れそうなので良さそう。

システムを作るときは、APIへの月あたりのリクエスト数の制限が少なめなので、その辺を考慮しつつ作る必要があるみたい。

最近PHPやる上で、フレームワークも触るかってなってCodeigneiterを触ってる。  
これ組み合わせて簡単なアプリ作るの目標にちょこちょこコード書いてる。もうしばらくPHPになりそう…。
