---
title: Vagrant(VCCW)のゲスト側に他の端末からアクセス出来るようにした
author: コニタン
type: post
date: 2016-04-10T23:43:51+00:00
url: /archives/1766
wordtwit_post_info:
  - 'O:8:"stdClass":13:{s:6:"manual";b:0;s:11:"tweet_times";s:1:"1";s:5:"delay";s:3:"180";s:7:"enabled";s:1:"1";s:10:"separation";i:60;s:7:"version";s:3:"3.7";s:14:"tweet_template";b:0;s:6:"status";i:2;s:6:"result";a:0:{}s:13:"tweet_counter";i:2;s:13:"tweet_log_ids";a:1:{i:0;i:1767;}s:9:"hash_tags";a:0:{}s:8:"accounts";a:1:{i:0;s:6:"skd_nw";}}'
wordtwit_posted_tweets:
  - 'a:1:{i:0;i:1767;}'
categories:
  - クリエイティブ
tags:
  - Vagrant

---
最近ようやく重い腰を上げ、WordPressなんかの開発環境として使っているMAMPから、別の仮想環境への移行を決意して動いてます。

Wordmove使いたい思いもあったのでWockerではなくVCCWにしました。

## 今回やりたかったこと

  * VCCWの導入
  * 他の端末からのアクセスを可能にする

## VCCWの導入

導入からブラウザで確認するまでは簡単でした。
  
サイトに手順が載っているので落ち着いてコマンドを叩いていけばできます。

<a href="http://vccw.cc/" target="_blank">VCCW &#8211; A WordPress development environment.</a>

## 他の端末からのアクセスを可能にする

最近知ったのですが、MAMPってローカル環境で設定しているIPアドレスとポート番号を教えたら同じWi-Fiに接続している他の端末からでもアクセス出来るんです。チームで開発していて、こんな感じで組んでるんだけどどうよ？って共有したい場合、IPアドレスとポート番号を教えるだけで見てもらえるのは結構便利です。

こういうのできないのー！って言ってたら、＼ポートフォワーディング／＼ポートフォワーディング／みたいな言葉を聞いたので調べていたのですが、うまくいく方法が全然見つからなくて解決までかなりの時間がかかりました。ググるときの考え方とか表現の仕方って重要だなぁと思いました。

方法としては、

  * ポートフォワーディング
  * ブリッジ接続

の2つがあるっぽくて、僕は後者のブリッジ接続(多分)で実現しました。

    config.vm.network :public_network, bridge: "en1: Wi-Fi (AirPort)"
    

この1文を以下のようにVagrantfileに書き込みました。

    Vagrant.configure(2) do |config|
    
      config.vm.network :public_network, bridge: "en1: Wi-Fi (AirPort)"
    
      vccw_version = '2.18.0';
    
      _conf = YAML.load(
        File.open(
          File.join(File.dirname(__FILE__), 'provision/default.yml'),
                :
                :
    

分かりにくいですが、スペースは半角2コです。

これでvagrant upすると準備は完了です。

また、以下のコマンドをホストOS側で実行することで同じWi-Fiに接続している端末からアクセスするIPアドレスが分かりました。

    $ ifconfig | grep inet

また、毎回IPアドレスを調べるのは面倒なので、指定する事も出来るようです。<aside class="ref"> 参考:</p> 

  * <a href="http://www.d-wood.com/blog/2014/06/13_6344.html" target="_blank">Vagrant: 同じLAN内の端末から仮想マシンにアクセスする | deadwood</a>
  * <a href="http://qiita.com/teratsyk/items/10bf89422ce98265c8a8" target="_blank">LAN内の他端末からvagrantの仮想マシンにsshする &#8211; Qiita</a></aside> 

何度かこの記述を見て実際に書き込んでいたのですが上手くいかず困惑していました。
  
きっと書く場所が悪かったんだと思います。

## 今後

実はまだWordMoveがうまく設定出来ておらず、モヤモヤしています。
  
はやいとこ解決して幸せになりたい！

<ins><br /> 追記: <time>2016.05.05</time><br /> この間WordMoveの設定も終わり、使用できるようになりました。<br /> </ins>