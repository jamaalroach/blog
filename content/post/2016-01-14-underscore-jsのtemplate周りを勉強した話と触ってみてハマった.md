---
title: Underscore.jsのtemplate周りを勉強した話と触ってみてハマった話
author: コニタン
type: post
date: 2016-01-13T17:56:42+00:00
url: /archives/1738
wordtwit_post_info:
  - 'O:8:"stdClass":13:{s:6:"manual";b:0;s:11:"tweet_times";s:1:"1";s:5:"delay";s:2:"15";s:7:"enabled";s:1:"1";s:10:"separation";i:60;s:7:"version";s:3:"3.7";s:14:"tweet_template";b:0;s:6:"status";i:4;s:6:"result";a:0:{}s:13:"tweet_counter";i:1;s:13:"tweet_log_ids";a:0:{}s:9:"hash_tags";a:0:{}s:8:"accounts";a:1:{i:0;s:6:"skd_nw";}}'
categories:
  - クリエイティブ
tags:
  - JavaScript

---
最近JavaScriptの勉強をしているのですが、この間HTMLのテンプレートを使いたいなと思ったため、<a href="http://underscorejs.org/" target="_blank">Underscore.js</a>のtemplateを使ってみました。その際にハマったので備忘録として。

## 今回使用したもの

  * jQuery: 2.1.4
  * Underscore.js: 1.8.3

## 使い方

    var data = {
        content1: 'value1',
        content2: 'value2'
    };
    
    // 一気に書く
    _.template('<div><%= content1 %></div>')(data);
    
    // 別々で書く
    var compailed = _.template('<div><%- content2 %></div>');
    var compailed(data);
    

テンプレート部分にJavaScriptの変数やコードを埋め込む事が出来るようで、%後が=ならそのまま出力、-なら値をエスケープして。何も書かなければその中に処理を書いていけるみたいです。

## 何にハマっていたのか

### やりたかったこと

HTMLファイルにテンプレートもち、テンプレートを取得してデータを流し込んでDOMを追加したかった。

### 結局

やり方としては以下の様に書くことでいけたのですが、勘違いによりハマりました。

index.html

    (略)
      <script src="https://cdnjs.cloudflare.com/ajax/libs/underscore.js/1.8.3/underscore-min.js"></script>
      <script src="js/script.min.js"></script>
      <script id="my-templpate" type="text/template">
        <%= hoge %>
      </script>
    </body>
    </html>
    

script.js

    var obj = {hoge: 22};
    
    _.template( $('#my-template').html() )(obj);
    

### ハマっていた所

何度か「ReferenceError: data is not defined」というエラーが表示されていました。
  
間違っていたのはテンプレート側に **オブジェクト名を書いていたから** でした。
  
JavaScriptでオブジェクトのプロパティへのアクセスは、オブジェクトにプロパティ名を繋ぐことで出来たよねと思ってそのノリで書いていたのですが、今回の場合はオブジェクト名は必要ではなく、テンプレート側ではその場所で使うプロパティ名のみで良いようです。
  
オブジェクトは既に指定してるんだからその中でどれ使うか選べよ！ってことなんだと思います。