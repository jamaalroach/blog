+++
title = "JAWS-UG KOBE Alexa meetupでAlexa Deviceを自作する話をしてきました"
description = "先日開催されたJAWS-UG KOBEでAlexa Deviceを自作する話をしてきました"
categories = ["行ってきた"]
tags = ["JAWSUG", "Alexa", "RaspberryPi"]
date = 2017-10-20T11:28:07+09:00
author = "Daisuke Konishi"
+++


先日、JAWS-UG KOBEのAlexa meetupでAlexa Deviceを自作した話を喋ってきました。

登壇資料はこちらです。
<script async class="speakerdeck-embed" data-id="b78d69236a79442c9776e90107f0c0a8" data-ratio="1.33333333333333" src="//speakerdeck.com/assets/embed.js"></script>

実際できたのはこんなの。

![出来上がったAlexa Deviceの画像](/images/2017/jawsug-slexa-start/21981555_924077604397357_569612756_o.jpg "")

今回は筐体にプリングルスを指定されたのですが、登壇後に「プリングルスに入れろよー」ってめっちゃ言われましたｗ

今回RaspberryPiを初めて触ったんですが、とてもいい経験になりました。
ラズパイ周りは相性があるって聞いたんですが、調べ回ってとりあえず以下で揃えました。

- [Raspberry Pi 3 MODEL B](https://www.amazon.co.jp/gp/product/B01CD5VC92/ref=as_li_ss_tl?ie=UTF8&psc=1&linkCode=ll1&tag=ksk1207-22&linkId=cecaddc3144b23eeb2d97862e81da005)
- [Raspberry Pi用電源セット(5V 3.0A)－Pi3フル負荷検証済](https://www.amazon.co.jp/gp/product/B01N8ZIJL8/ref=as_li_ss_tl?ie=UTF8&psc=1&linkCode=ll1&tag=ksk1207-22&linkId=09284da0a5bf58b13f506c740f9ba5d0)
- [TOSHIBA 東芝 microSDHC 16GB Class10](https://www.amazon.co.jp/gp/product/B018ZIVPL6/ref=as_li_ss_tl?ie=UTF8&psc=1&linkCode=ll1&tag=ksk1207-22&linkId=d7dd936d3d1bc5d42bde554f2e22ab19)
- [サンワサプライ USBマイクロホン MM-MCU02BK](https://www.amazon.co.jp/gp/product/B01M7YIYZV/ref=as_li_ss_tl?ie=UTF8&psc=1&linkCode=ll1&tag=ksk1207-22&linkId=30e12e49c288117daf3f8c59dc2f05f4)

マイクに関してはUSBタイプであまり場所を取らないものが良かったんですが、あまり情報が無く、これにしました。
あともう1つUSBドングルみたいな形のものがありました。

## RaspberryPIの設定周り
SDカードにはRASPBIANのSTRETCH、DESKTOP版をインストールしました。

[Download Raspbian for Raspberry Pi](https://www.raspberrypi.org/downloads/raspbian/)

フォームでCLI版はWi-Fiに繋がりにくいバグがあるみたいな書き込みがある事を教わったのですが、そろそろ直ったんでしょうか…。
今はDESKTOP版で色々設定し、モードをCLI版に切り替えて使っています。


## Alexa Clientの設定
スライド内でも書いていましたが、今回は以下の資料をもとに組んでいきました

資料: [JAWS DAYS 2017 ハンズオン RaspberryPi で 自作Echoを作ろう！ - Qiita](https://qiita.com/haruharuharuby/items/8d4c83423cbfe13c9121)


1. <a href="https://developer.amazon.com/ja/" target="_blank">developer.amazon.com</a>でアプリの登録と設定を取得
2. Alexa Clientの環境作成
  + git, pyenv, virtualenvの追加
  + AlexaPiを設定

## Alexa と戯れる
設定が終わると喋れるようになっていました。
ラズパイの設定さえできればあとはすんなりいけました。

```
$ cd AlexaPi
$ python wakeword_detection.py
```

Echoが来たら買って、スキルとか触ってみたいですね