+++
tags = ["Hugo","netlify"]
categories = ["クリエイティブ"]
description = "hugoで作成したサイトやページをnetlifyに公開する方法です。"
title = "Hugoで作成したサイトをNetlifyで公開する"
author = "Daisuke Konishi"
date = "2017-03-14T01:36:04+09:00"

+++

## はじめに
前回、[WordPressからHugoに移行した話](/post/migration-from-wordpress-to-hugo.html)を書きました。  
Hugoで静的なファイルを生成するので、折角ならサーバー代を抑えつつHTTPSに対応するか、勉強がてらS3に載せたいよなーと思っていました。そんな中少し前に参加した[フロントエンドエンジニアに伝えたいインフラの話 ](https://kfug.connpass.com/event/49305/)でNetlifyの話を聞いて、興味をもったので移行先にしちゃいました。


## Netlifyとは
* 公開したサイトはCDN経由で配信される
* SSL対応が簡単にできる
* 独自ドメインをあてられる
* PHPやRubyなどの言語は動かないっぽい
* CIツール(新規サイトの作成やデプロイなど色々可)もある

などなど

以下、手順です。

## アカウント作成
<a href="https://app.netlify.com/signup" target="_blank">サインアップ</a>からアカウントを作成します。  
Github, GitLab, Bitbucketの3サービスから選ぶことが出来ますが、Netlifyで公開したいプログラムをリポジトリ


## Hugoを導入する
NetlifyでHugoを運用するのに便利な方法は2種類あります。

1. <a href="https://www.staticgen.com" target="_blank">StaticGen</a>に掲載されているジェネレーターの下部にあるボタンからテンプレートを作成する(アカウントを作成したサービスにリポジトリが作成されます)
2. 自分で作成したHugoプロジェクトのリポジトリをNetlifyの監視対象にする


### 自作のプロジェクトをNetlifyの監視対象にする
1つ目は生成されたテンプレートを編集してpushするだけで特に説明は要らないので、ここでは2の方法についてです。  
※既存のプロジェクトはHugoを丸ごと管理下に置いたリポジトリをGithubに置いているとして進めます。

#### 1.Create your account  
1-1. Github を選択します。  
1-2. ログイン画面が表示されるのでIDとパスワードを入力します。  

#### 2.Create your project  
2-1. I already have a projectのLink to an exitsting repositoryボタンをクリック。  
2-2. Githubで自分が公開しているリポジトリが表示されるので、公開しておいたHugoのプロジェクトを選択。するとConfigureという画面に遷移します。  
ここでは、

* どのブランチを監視するのか
* 公開するディレクトリはどれか
* ビルドに使用するコマンドは何か

を設定出来ます。  
それぞれ以下のように設定しました。

```
Branch: master
Publish directory: public/
Build command: hugo --theme=テーマ名
```

あとは Build your site をクリックして少し待つだけです。  
次回から **masterブランチに push するだけ** で、ビルドに成功すると自動的に公開してくれるようになります。

ビルドが無事完了すると、管理画面左上の細字で表示されているサイト名か、setting の項目内の Name のリンクから実際のページに遷移する事ができます。

### ドメインをあてる
今回はRoute53で取得したドメインを今回作成したサイトにあててみました。
ちなみに、無料枠では example.com のようなネイキッド・ドメインを当てることはできず(?)、サブドメインを当てることができるようです。(一緒にやっていた人の情報)

DNSはAレコードを設定する場合は、``104.198.14.52`` へ、CNAMEを設定する場合はsettingのNameで遷移した先の ``name.netlify.com`` を設定します。  
うっかり書き換えてしまうのが怖いのでAレコードで設定しました。
また、どちらも設定する必要はなく、片方だけでいいそうです。DNS周りはめちゃくちゃ詰まってハゲそうでした。

参考: [Custom Domains | Netlify](https://www.netlify.com/docs/custom-domains/)

無事ドメインがあたったら、Hugo側のbaseURLを変更しておきます。  
baseURLはルートディレクトリにある、``config.toml`` に記述します。

### HTTPS化
HTTPS化は管理画面のHTTPSの項目へ進むだけです。
Fource TLS connectionsにチェックを入れておけばHTTPSでのみ閲覧出来るようになり、HTTPでのアクセスはHTTPSにリダイレクトがかかるようになりました。

HTTPSでアクセス出来るようになったら、baseURLの変更をしておきましょう。

## まとめ
Netlifyへのアップはとても簡単でサクッとできました。
何故かドメインがあてられず悩んだ時間の方が長かったです。

これから静的なもので試しにアップしたいときはここ使うのも良さそうです。
