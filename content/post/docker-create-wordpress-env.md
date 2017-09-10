+++
title = "Dockerを使ってWordPressの構築構築をやってみた"
description = "Dockerを使ってWordPressの環境を作ってみたのでその覚書とか"
categories = ["クリエイティブ"]
tags = ["Docker", "WordPress"]
date = 2017-09-10T16:19:49+09:00
author = "Daisuke Konishi"
+++


Dockerを触りつつありますが、ちょっとやることがあったのと、ついでと思ってWordPress環境を作ってみました。

WockerというDockerベースの環境構築ツールがあるので、そっちを使っても良かったんですが勉強です。

## Docker イメージの準備
いつも通りDocker HubからWordPressとMySQLのイメージを取得します。

```
$ docker pull wordpress

$ docker pull mysql
```


## コンテナの起動
### MySQLの起動
まずは、MySQLのコンテナを起動します。

```
$ docker run --name mysite_db -e MYSQL_ROOT_PASSWORD=password -e MYSQL_DATABASE=mysite -d mysql
```

### WordPressコンテナの起動
WordPressのコンテナを起動し、先程立ち上げたMySQLのコンテナに接続します。

```
$ docker run --name mysite --link mysite_db:mysql -p 80:80 -e WORDPRESS_DB_PASSWORD=password -d wordpress
```

## ブラウザからアクセス
以下のコマンドでローカルのIPをはじめ色々確認できます。
```
$ ifconfig
```

僕はコンテナ外で叩いてローカルのIPを知った(en0のところにありました)んですが、実際はコンテナ内で叩くみたい？

上記コマンドで調べたローカルIPにブラウザからアクセスすると、無事インストール画面が表示できました。


## コンテナはまとめて操作できる
今回 WordPress と MySQL のコンテナをそれぞれいろんなオプションをつけて起動していましたが、docker-compose というコンテナをまとめて操作できるツールがあり、これを使うことで複数のコンテナをまとめて操作できるみたいです。
一度設定ファイルを書いてしまえば、短いコマンド1個で起動と停止ができるのでとてもありがたいです。

docker-compose に関しては前触ったときに1度触れたもののよく分からず断念したのを覚えています…。
丁度いい機会なのでちゃんと勉強して使い方を覚えておきたい…！

今回やったこととや docker-compose については以下で書かれているのでぜひ読んでみてください。  
[はじめてのDocker 〜公式イメージで簡単にWordPressサイトをつくる方法〜 | WebNAUT](https://webnaut.jp/technology/20170118-1828/)

## その他参考
* [library/wordpress - Docker Hub](https://hub.docker.com/r/library/wordpress/)
* [library/mysql - Docker Hub](https://hub.docker.com/_/mysql/)