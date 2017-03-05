---
title: hubotスクリプトをherokuに置いてhubotに息を吹き込んだ話
author: コニタン
type: post
date: 2015-11-15T23:19:18+00:00
url: /archives/1714
wordtwit_post_info:
  - 'O:8:"stdClass":13:{s:6:"manual";b:0;s:11:"tweet_times";s:1:"1";s:5:"delay";s:1:"0";s:7:"enabled";s:1:"1";s:10:"separation";i:60;s:7:"version";s:3:"3.7";s:14:"tweet_template";b:0;s:6:"status";i:2;s:6:"result";a:0:{}s:13:"tweet_counter";i:5;s:13:"tweet_log_ids";a:4:{i:0;i:1717;i:1;i:1718;i:2;i:1719;i:3;i:1720;}s:9:"hash_tags";a:0:{}s:8:"accounts";a:1:{i:0;s:6:"skd_nw";}}'
wordtwit_posted_tweets:
  - 'a:4:{i:0;i:1717;i:1;i:1718;i:2;i:1719;i:3;i:1720;}'
categories:
  - クリエイティブ
tags:
  - hubot
  - JavaScript

---
先日研究室内でSlackの話をしたところ、色んな人がチームに参加してくれました。
  
そこでもっとチーム内を盛り上げたり出来ないかなーと思い、hubotでのbot制作を始めました。
  
最近ようやくまともに動くようになったので、その辺の実装のメモです。

※HubotとSlackの連携やherokuのアカウント取得とかその辺の話はありません。

## Coffeescriptとhubotをローカルにインストール

CoffeeScirptでHubotのスクリプトを書くため、Hubotと一緒にCoffeeScriptもインストールする。

<pre><code class="bash">$ npm install -g coffeescript hubot
</code></pre>

## Hubotのひな形を作る

よく以下のコードを見かけたけどコマンド叩いたら怒られた。

    $ hubot --create XXXbot
    

代わりに以下のジェネレーターを勧められたので入れたら上手くいった。

    $ npm install -g yo generator-hubot
    

この後ディレクトリを作成し、その中で以下のコマンドを入力。

    $ yo hubot
    
                         _____________________________  
                        /                             \ 
       //\              |      Extracting input for    |
      ////\    _____    |   self-replication process   |
     //////\  /_____\   \                             / 
     ======= |[^_/\_]|   /----------------------------  
      |   | _|___@@__|__                                
      +===+/  ///     \_\                               
       | |_\ /// HUBOT/\\                             
       |___/\//      /  \\                            
             \      /   +---+                            
              \____/    |   |                            
               | //|    +===+                            
                \//      |xx|                            
    
    
    ? Owner: Daisuke
    ? Bot name: nurupobot
    ? Description: call 'nurupo' return 'ga' bot
    ? Bot adapter: (campfire) slack
    
    

片腕ドリルなキャラクターが出てきた。誰だよお前って動揺して何度かキャンセルしたけどこれがHubotのキャラらしい。よく見ると胸に名前書いてあった。ごめん。

下のOwnerの行の項目からは自分で入力する所。ノリと勢いで書いたんだけど滅茶苦茶な書き方してるなーと後悔。

この後Enterを押すことでひな形は完成。

## サンプルコード

パッと思いつかなかったので下記サイトのコードを頂いて使ってみた。
  
あのおなじみのぬるぽに対してガッ！って返すアレ。

[&#8220;ぬるぽ&#8221;に反応してｶﾞｯしてくれるHubotスクリプト Slack内での表示に最適化済][1]

script/ 下に落としてきたスクリプトファイルを入れた。

## ローカルで確認

    $ bin/hubot
    nurupobot> Hubot ぬるぽ
    nurupobot> ```
       Λ＿Λ     ＼＼
    （  ・∀・）  | | ｶﾞｯ
     と     ）  | |
      Ｙ /ノ     人
       / ）    < >   _Λ  ∩
    ＿/し'   ／／  Ｖ｀Д´）/
    （＿フ彡             / ←>> @Shell
    

痛い。
  
vexus2さん(スクリプト書いた人)には感謝。

## コミットからherokuへデプロイする

slackと連携するためのパッケージをインストール

    $ npm install hubot-slack --save
    

作ったbotのディレクトリ内にある Procfile に以下を書き込む

    web: bin/hubot --adapter slack
    

    $ git init
    $ git add --all
    $ git commit -m "first commit"
    $ git remote add origin リモートリポジトリのURL
    $ git push -u origin master
    

## herokuでの操作

    $ heroku login
    $ heroku create herokuでのアプリ名
    $ git push heroku master
    
    $ heroku ps:scale web=1
    $ heroku addons:add rediscloud
    

最後の行を行う前にクレカの登録が要るみたい。

### memo

何度かappを作っては消ししていると、ある日herokuにpushするタイミングでpermission deniedになった。その際の参考は下。
  
[herokuでpushしようとしたらPermission deniedとなってしまう | 世界はどこまでもシンプルである][2]

## Hubotの設定

    $ heroku config:add HUBOT_SLACK_TOKEN=トークン
    $ heroku config:add HUBOT_SLACK_TEAM=botを動かしたいチーム名
    $ heroku config:add HUBOT_SLACK_BOTNAME=ボットの名前
    $ heroku config:add HEROKU_URL=http://xxx.herokuapp.com
    

  * Hubotのトークンは、SlackのIntegrationsに連携したHubotがあり、それの詳細で見れる。
  * HerokuのURLはherokuの画面で右上の…メニューからOpen AppがあるのでそこをクリックするとURLが分かる。(ちょっと迷った)

## まとめ

herokuを使ってHubotを動かす方法が分かった。
  
今後定時実行するbotを作る予定。他にも何か思いついたら作ってみよう。

 [1]: https://gist.github.com/vexus2/94f1d666485931a8c9c6
 [2]: http://daipresents.com/2012/post-5010/