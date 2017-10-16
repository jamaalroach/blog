+++
title = "WordBench京都(10月)でElastic StackでWordPressのパフォーマンス計測をやってみた話をしてきました"
description = "2017年の10月に行われたWordBench京都で、Elastic StackでWordPressのパフォーマンス計測をやってみた話をしてきました"
categories = ["行ってきた"]
tags = ["WordBench", "WordPress", "Elasticsearch", "Kibana", "Beats"]
date = 2017-10-15T23:18:17+09:00
author = "Daisuke Konishi"
+++

さて、タイトル通り、[2017年の10月に行われたWordBench京都](https://wb-kyoto.connpass.com/event/65182/)で、Elastic StackでWordPressのパフォーマンス計測をやってみた話をしてきました。


<script async class="speakerdeck-embed" data-id="569483c5eefd4e01a53da9e4fbd780d7" data-ratio="1.33333333333333" src="//speakerdeck.com/assets/embed.js"></script>


前回のElasticネタは、Elasitcsearchを繋いで検索を高速化するって話だったのですが、プラグインを入れたらなんとかなる内容でした。
ただ、今回はBeatsを使ってWordPress側のサーバーのパケット情報を拾う予定だったのでそういうわけにもいかず、環境のセッティングから。

環境のセッティングもDockerの導入にチャレンジしてみました。  
Dockerイメージの選定やComposeでまとめるなどもやってみていい経験になりました。


## 補足とか
ちなみに今回使ったのは、以下のDockerイメージです。

### WordPress側のイメージ

- [library/wordpress - Docker Hub](https://hub.docker.com/_/wordpress/)
- [library/mysql - Docker Hub](https://hub.docker.com/_/mysql/)

### Elastic系のイメージやインストール方法

- [proteansec/packetbeat - Docker Hub](https://hub.docker.com/r/proteansec/packetbeat/)
- [Install Elasticsearch with Docker | Elasticsearch Reference [5.6] | Elastic](https://www.elastic.co/guide/en/elasticsearch/reference/current/docker.html)
- [Pulling the image | Kibana User Guide [5.6] | Elastic](https://www.elastic.co/guide/en/kibana/current/_pulling_the_image.html)

今回の登壇に向けての情報収集のお陰でWeb上のいろんな広告が7割くらいElasitc社のものになりました。そのうち押すか…