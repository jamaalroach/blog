+++
title = "PythonでTwitterのトレンドワードを取得してElasticsearchに突っ込んで、Kibanaで見るサンプルを写経した"
description = "DockerでElasticsearch+Kibanaの環境をつくれるようになったので、QiitaにあがっていたPythonでトレンドワードを取得してELKで可視化するサンプルをやってみた"
categories = ["クリエイティブ"]
tags = ["Python", "Twitter API", "Elasticsearch", "Kibana", "Docker"]
date = 2017-09-12T01:22:27+09:00
author = "Daisuke Konishi"
+++


DockerでElasticsearchとKibanaの環境を作ることができたので、何かできないかなーと思ってた。  
この間、Elastic社の人がイベントのブースで「Twitterのトレンドワード拾ってElasticsearchに突っ込んでKibanaで可視化してまーす」みたいなツイートをしてるのを思い出して探してみたら、1年前の記事なんだけどこんな記事があったのでやってみた。

[ElasticsearchとKibanaを使ってTwitterのトレンドワードを可視化してみた - Qiita](http://qiita.com/yoppe/items/3e61fd567ae1d4c40a96)

出来上がったものは[ここ](https://github.com/d-kusk/elk-twitter-trend-py)にあげてる。

今回はDockerで[nshou/elasticsearch-kibana - Docker Hub](https://hub.docker.com/r/nshou/elasticsearch-kibana/)を立ち上げた。  
Pythonはvenvで環境作って、Dockerで立ち上げたElasticsearchに送信するって形。

ホントはPythonの環境もDockerで作ったほうが良いんだろうなーと思いつつ、とりあえずお試しだったのと他でやることあったから今回はよし。

## 小さな学びが多かった
今回Dockerで立ち上げるあたりは得に変わらなかったけど、Python側で色々と学びがあった。

たとえば、書きながらflake8を走らせて適宜修正って感じで進めてたんだけど、その中でお作法を知ったり命名の仕方なんかも見れてよかった。  
引数での=前後にスペースつけちゃ駄目なのは慣れない…。

コードの中でも全然触ったことないモジュールやメソッドがいっぱい出てきてその都度調べて分かった(気になってる)んだけど、そういうことも出来るんだってものが分かったのはよかった。多分使っていく中で覚えるでしょう。  

余談だけど、最近VSCodeを使い始めていて、VSCodeでの環境設定みたいなものがちょっとわかった。

## Kibanaでの可視化

![Kibanaで取得したTwitterの可視化をした画面](/images/2017/python-elk-search-trend/kibana-twitter-trend.png)

ちなみに、Kibanaではこんな感じで見れた。

触り方がよく分かってないので、デフォルトのまま。  
触り方は時間作って調べておこう。

## やってみて
Twitterからの取得とかElasticsearchへの投げる部分とかってどうなってんだろうと思ったけど、モジュールあるしすごいあっさりしてるしで驚いた。
コードは理解しきれてないのでもう少し読んで理解したい。

ところで、プロジェクトのファイルの作り方、こうじゃない気がする。
