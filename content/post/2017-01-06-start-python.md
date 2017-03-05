---
title: Pythonを始めようと思って環境作った
author: コニタン
type: post
date: 2017-01-05T17:35:49+00:00
url: /archives/2011
wordtwit_post_info:
  - 'O:8:"stdClass":13:{s:6:"manual";b:0;s:11:"tweet_times";s:1:"1";s:5:"delay";s:1:"0";s:7:"enabled";s:1:"1";s:10:"separation";i:60;s:7:"version";s:3:"3.7";s:14:"tweet_template";b:0;s:6:"status";i:4;s:6:"result";a:0:{}s:13:"tweet_counter";i:1;s:13:"tweet_log_ids";a:0:{}s:9:"hash_tags";a:0:{}s:8:"accounts";a:1:{i:0;s:6:"skd_nw";}}'
categories:
  - クリエイティブ
tags:
  - Python

---
少し前からバックエンドに手を出そうと思っていたのですが、知り合いに誘われてPythonです。

色々と寄り道するせいでまだ環境作ってHello Worldを表示させるくらいまでしか出来ていないのですが、とりあえずVagrantとAtomにそれぞれPython書くための環境作りをしたのでそのメモです。

## Vagrantで動作環境の構築

今まで、PHP（というかWordPress）やるときはMAMPなりVCCWなりWockerという先人のありがたいツールを使っていたのですが、Python業界はよく分からないのでVagrant使ってちゃんと作ろうって思ったわけです。

とりあえず目についた以下を参考に作ってみました。
  
[Ubuntu Server 14.04 LTSにPythonの開発環境をつくる &#8211; えんがわ][1]

  * Vagrant 
      * ubuntu/trusty64
      * Python 3.4.3

Pythonは2と３があるらしいのですが、2にしか対応してない分析系？のライブラリを使わない限り3でいいよって聞いたので今回は3系で。
  
Ubuntuにプリインストールされてたのでありがたかったです。

あと、ツールとして以下を入れました。

  * pip
  * virtualenv

pip　はサードパーティモジュールの管理を行うものらしく、　npm　とか　gem　にあたるツールなのかなーというイメージです。
  
一方、virtualenv は仮想環境みたいなものを作るツールらしく、A, B別々で作った環境で競合しちゃうようなモジュールのインストールを行い、チェックするとかそういうので使うんだとか。

見てると他にも色々ツールがあるらしいのですが、調べきれていないのでちょっと保留。

## Atomへの補助系ツールの追加

とりあえず書いていく上で有ると嬉しいようなパッケージを入れました。

  * language-python
  * autocomplete-python
  * linter-flake8

そもそもPythonのハイライトとか補完とかその辺が無かったようなのでそれを。
  
補完って有り難いけど未だ恩恵をしっかり受けれていない気がするので、ガンガン使っていきたい！

なんなら最初からLinteｒに殴られながらちゃんと書いていきたいなと思ったのですが、幾つかあるようで。
  
pep8がコーディング規約らしいので、とりあえずこれに準拠できるようにlinterはpep8のものを入れました。

[mieki256&#8217;s diary &#8211; Atomエディタ上でpep8やflake8を試したり][2]

## 今後

とりあえず色々書いてみるのですが、とりあえずルーティングができるフレームワークのflaskを使って何かアプリを作るところまで頑張ります。

<ins datetime="2017-02-01T14:08:49+00:00">実はこういうの無くても出来ると聞いて、pyenvとvirtualenvに変えました。おそらく3系しか使わないのでvenvでも良いらしいのですが一応。</ins>

 [1]: http://www.flounderedge.com/entry/2016/04/05/002639
 [2]: http://blawat2015.no-ip.com/~mieki256/diary/201610301.html