+++
title = "(Python)AWS Lamda から Slack に通知するまでを組んでみた"
description = "AWS Lamda から python で組んだ関数を使って Slack に通知するまでを組んでみた"
categories = ["クリエイティブ"]
tags = ["Lambda", "Python"]
date = 2017-11-09T11:30:44+09:00
author = "Daisuke Konishi"
+++

最近名前を聞いたり、知っておくと便利そうだなと思って、AWSのLambdaを触ってみた。  
ずっとLamdaだと思ってたので最初死んだ。

## Lambdaってなんなのか
リクエストを受けて実行とか cron 回して定時実行とかそういうイベント駆動なものが用意できるやつ。

僕らは実際に実行する Lamda Function っていう関数を作って、その他関連ファイルとまとめてデプロイしておくことで、それを実行してもらうことができる。 Node.js や Python 、C++ なんかで書かれたコードを実行するらしい。なんか Node.js の記事が多いのが肌感。

ちなみに無料枠があって、以下な感じ。

> AWS 無料利用枠には、AWS Lambda での1 か月あたり 100 万の無料要求と最大 3.2M 秒のコンピューティング時間が含まれます。


## IAM で専用のユーザーを作成
ユーザーバレて色々触られると厄介なので、専用の権限を割り振ったユーザーを作って、それ経由で動作させるというもの。

以下を参照した気がする。  
[AWS Lambdaを始めてみる(1).ユーザーアプリケーションからのイベントを扱う ｜ Developers.IO](https://dev.classmethod.jp/cloud/aws/getting-started-with-aws-lambda-1st-user-application/)

新規でグループを作り、ポリシーとして **AWSLambdaFullAccess** を付与し、ここにユーザーを突っ込んだ。
後で ユーザーの ARN(arn:aws ~~~) を使うことになる。

## Python で色々用意
幾つか記事はあったんだけど、料金分かるといいよねって思って以下をもとに進めた。多分部分的にか書かないので下をあわせて読むのがいいかも。
[LambdaでAWSの料金を毎日Slackに通知する（Python3） - Qiita](https://qiita.com/tomohiko_isobe/items/88e8e0dcb0ee224a31e4)

(リージョンミスってるのか1個値が帰ってこなくてエラーで通知されないけど…。)

用意するファイルは以下

* lambda_function.py  実行する関数
* lambda.py  lambdaの設定。リージョンやroleの設定など。variablesで環境変数も用意できる
* (requirements.txt)

その他必要なもの

* lambda-uploader
* aws cli

```
$ pip install lambda-uploader awscli
```

### AWSで使うユーザーの設定

AWS CLIはどのユーザーとしてアクセスするのかの設定に使いました。
以下で対話形式で設定。

```
$ aws configure
```

### AWS Lambdaへのデプロイ
lambda-uploader はローカル環境で用意したファイル群のデプロイやモジュールを Lambda 上でインストールするため。
最終的には以下でデプロイする。

```
$ lambda-uploader
```

## Slack に通知するコードを作成
幾つかモジュールはあったんだけど、Python の requests モジュールを使った。

また、コード自体はLambdaで関数を作成するときに幾つか雛形が用意されているものを選べるので、そこから組んでいくのが楽だと思う。

![Lambdaの関数の雛形](/images/2017/lambda-slack/lambda-template.png)

### 実際に通知するところの処理
slack に投げる情報を辞書でまとめて、post するという流れ。
色々ハマったんだけど、とりあえず、iconが無いとなんかpostしても通知されなかった。

``` python
def lambda_handler(event, context):
    # SlackにPOSTする内容をセット
    slack_message = {
        'channel': SLACK_CHANNEL,
        "text": 'Lambdaからでーす',
        "icon": ':penguin:',
    }

    # SlackにPOST
    try:
        res = requests.post(SLACK_POST_URL, data=json.dumps(slack_message))
        logger.info("Message posted to %s", slack_message['channel'])
    except requests.exceptions.RequestException as e:
        logger.error("Request failed: %s", e)
```

### 問題: Lambda 上で pip install ができなかった
いろんな所で書かれていて、requirements.txt に書いておくと lambda_uploader がうまいことやってくれるって記載もあったんだけど、僕の環境ではうまく行かなかった。

そこで他を調べていると、以下のコマンドが紹介されていて、これを使うといけた。

```
$ pip install -t requests .
```

requests モジュールをインストールして、ローカルに展開するみたいな感じ。ディレクトリ構成は汚くなるけど、致し方ない…。


## 参考にしたもの
* [練習を兼ねてAWS LambdaからSlackにPOSTするプログラムを組んだ](https://geeknavi.net/aws/auto-post-to-slack#Slack)
* [LambdaでAWSの料金を毎日Slackに通知する（Python3） - Qiita](https://qiita.com/tomohiko_isobe/items/88e8e0dcb0ee224a31e4)