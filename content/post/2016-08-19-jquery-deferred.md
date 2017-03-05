---
title: jQueryのDeferredでアニメーションの順序を指定してみた
author: コニタン
type: post
date: 2016-08-18T23:33:13+00:00
url: /archives/1884
wordtwit_post_info:
  - 'O:8:"stdClass":13:{s:6:"manual";b:0;s:11:"tweet_times";s:1:"1";s:5:"delay";s:2:"15";s:7:"enabled";s:1:"1";s:10:"separation";i:60;s:7:"version";s:3:"3.7";s:14:"tweet_template";b:0;s:6:"status";i:2;s:6:"result";a:0:{}s:13:"tweet_counter";i:4;s:13:"tweet_log_ids";a:3:{i:0;i:1893;i:1;i:1894;i:2;i:1895;}s:9:"hash_tags";a:0:{}s:8:"accounts";a:1:{i:0;s:6:"skd_nw";}}'
wordtwit_posted_tweets:
  - 'a:3:{i:0;i:1893;i:1;i:1894;i:2;i:1895;}'
categories:
  - クリエイティブ
tags:
  - jQuery
  - Webデザイン

---
最近全然やったこと無いのにアニメーションの実装がどんどん増えていて、しんどいけど反面ワクワクな毎日です。

この間Aのアニメーション後にBのアニメーションをしてその後にC&#8230;っていう連なったアニメーションの実装をしていたのですが、この時の実装方法を考える上でDeferredというものに出会って試してみたのでその覚書。

最初は良いやり方が分からなかったので、animateのcomplete引数を利用して書き続ける事を考えていましたが、流石に処理が増えると読みづらくて仕方ないと思い他を探しました。
  
そこで出会ったのがDeffered。

## Deferredって

非同期処理を監視するためのオブジェクトで、v1.5から導入されたものらしいです。

## 実装

### Differredオブジェクトを生成し、処理を繋げる

アニメーションの処理を関数化しておいて、その中でDeferredオブジェクトを生成。
  
アニメーションの終了後、promiseオブジェクトを返すようにする。これが返ってきた事を監視して次に繋げるという全体の動きを管理する関数も用意するって感じ。

処理を繋げるときは、最初に動作させるものにthen()で繋いでいく感じみたいです。

    $(function() {
        function playAnimation(){
            // .then(関数名)で関数を繋げる
            firstAction()
                .then(scoundAction)
                .then(thirdAction)
                .then(showReplay);
        }
    
        function firstAction(){
            // Deferredオブジェクトを生成
            var d = new $.Deferred;
            $(".box_red").animate({
                "top" : "400px"
            }, 1000, function(){
                // 状態を実行可能にする
                d.resolve();
            });
            // Promiseオブジェクトを返す
            return d.promise();
        }
    
        function scoundAction(){
            var d = new $.Deferred;        
            $(".box_green").animate({
                "top" : "450px"
                }, 1000, function(){
                d.resolve();
            });
            return d.promise();
        }
    
        function thirdAction(){
            var d = new $.Deferred;
            $(".box_blue").animate({
                "top" : "300px"
                }, 1000, function(){
                d.resolve();
            });
            return d.promise();
        }
    
        function showReplay(){
            $("#replay").fadeIn("fast");
        }
    
        // 実行
        playAnimation();
    });
    

コードは以下の記事が分かりやすかったので引用。
  
[【32：jQuery.Deferred】要素を順にアニメーション表示 &#8211; one&#8217;s way blog][1]

### 連続しつつAとBの処理を非同期で動作させたい場合

今回、Aが動いた後にBとCが動くみたいな事をやりたかったので、一緒にやるにはどうしたら良いんだろうと思っていたのですが、以下の記事が分かりやすかったです。

[jQueryのPromiseとDeferredとは &#8211; ハッカーを目指す白Tのブログ][2]

上のコードで、最初に動作する処理の後にthen()で繋いでいましたが、その中で関数をとってwhen()で処理をまとめちゃうっていう方法。

    delayHello()
    　　.then(delayHello)
    　　.then(function(){
      　　　return $.when(delayHello(), delayHello(), delayHello());
    　　　　})
    　　.then(delayHello)
    　　.then(function(){
      　　　　return $.when(delayHello(), delayHello(), delayHello());
    　　　　})
    　　　　.then(delayHello);
    

コードは上記記事より引用。

やってみると結構見やすいし分かりやすいので良いかなーと思いました。

## ただし、複雑なものでなければsetTimeoutでやる方が調整が効くらしい

今回の様な連続したアニメーションをする場合にDifferedでの実装だと、Aが終わってからB、またはAと一緒にBを実行といった形の指定になり、微調整はanimateのdulationでやるって感じになりそうです。

ただ、アニメーションの中ではAが動いている途中でBを走らせるみたいな処理が有ったりとか、「このBのアニメーションワンテンポ早く動かせませんか」みたいな注文が来たりするんだとか。
  
そういうのに対応する場合、setTimeoutで実装しておいた方が対応しやすいらしいです。

ちょっとモヤッとする部分もありますけど、そっちも試してみて場合によって使い分けれるようにしておこうと思います。

 [1]: http://onesway.hatenablog.com/entry/deferred
 [2]: http://beck23.hatenablog.com/entry/2014/11/08/022842