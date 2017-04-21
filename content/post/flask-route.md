+++
date = "2017-04-21T13:34:36+09:00"
tags = ["Python","Flask"]
categories = ["クリエイティブ"]
description = "FlaskとJinja2を使ってルーティング周りの勉強をしている話"
title = "Python のFlaskでルーティングまわりを触った"
author = "Daisuke Konishi"

+++

触りだしてからというもの、仕事や他の用事でなかなか触れてませんでしたが、ようやく一区切りついたので一旦メモ。

[Flask](http://flask.pocoo.org/docs/0.12/)というPythonの軽量フレームワークを使って、ルーティング周りの実装はどうするのかを勉強した。というか今も継続中。

## バージョンなど
* Flask 0.12
* Jinja2 2.9.5

これまでルーティングといえばWordPressがなんやかんやいい感じにやってくれる世界で生きていたのでそこまで意識しなかったのですが、いざやってみてなんとなくでも仕組みが分かると楽しい。

勉強する上で、とりあえずDocument読んだり、[A Minimal Application](http://flask.pocoo.org/docs/0.12/quickstart/#a-minimal-application)をなぞった。


## ルーティング周りの初めの1歩
とりあえずpipでflaskを入れて、本体をimport。
ここから**デコレータでパスを指定し、そこにアクセスが来たときに行う処理を関数で定義する**という形らしい。

とりあえずindexにアクセスがあればお決まりのあれを返すやつ。

```
# -*- coding: utf-8 -*-
from flask import Flask
app = Flask(__name__)


@app.route('/')
def index():
    return 'Hello world
```

やってることが少ないのもありますが、構造は結構分かりやすいのかなーと思いました。ただ、規模によっては結構長くなって管理が大変なとこな気も‥。

デコレータって関数1個につき1個しか付けられないと思っていたのですが、サンプルの中で、indexと/にアクセスが来た時の処理を同じものにするために2つ続けて書いていたのが驚き。

また、パスの指定と合わせてmethodの指定も出来るため、特定のメソッドでの絞り込みのような事もできるみたい。API作るときとかにはいいのかも。

## URLの値を拾う
以下のようにURLの後にカッコ有りの記述を入れることで、URLと一緒についてきたものを拾えるみたい。

```
@app.route('/archive/<cat>')
def archive(cat):
```

検索周りとかこういうのを使えば良いんだろうか。


## テンプレートの利用と値渡し(Jinja2)
幾つか上のような物を作った後で、テンプレートエンジンを使ってみた。FlaskだとJinja2がデフォルトらしい。

Pythonがインデントで書くのでテンプレート側も同じような書き方のpugみたいな物を想像していたけど、実際はEJSみたいなHTML内に値や処理を埋めるようなものだったので意外だった。

```
<!DOCTYPE html>
<html lang="ja">
<head>
  <meta charset="UTF-8">
  {% if title %}
  <title>{{ title }}</title>
  {% else %}
  <title>TopPage</title>
  {% endif %}
</head>
```


Flask側では、``render_template()``の第1引数で template/ 内のテンプレート名(拡張子まで)を指定し、第二引数以降でテンプレートに渡す値を設定するという処理を書く。

```
def index(title='hello, world'):
    return render_template('index.html', title=title)
```

テンプレートは同一の物を使い、アクセス先によってデータを変えるなんて事もできそう。

## リダイレクトと404
``redirect()``と``url_for()``を用いて以下のような記述にすることで、指定したパスにアクセスがあったときにリダイレクトをかけることができる。

```
@app.route('/works')
def work():
    return redirect(url_for('index'))
```

404 のハンドリングはこんな感じで組むっぽい

```
@app.route('/404')
def abort404():
    abort(404)


@app.errorhandler(404)
def error_handler(error):
    '''
    abort(404) したと時にレスポンスをハンドリングするハンドラ
    '''
    msg = 'Error: {code}\n'.format(code=error.code)
    return msg, error.code
```

今回はメッセージを返してるけど、それ用のテンプレートを返すほうが良いかも。  
``abort()`` がよく分からなかった。

## 今後
リクエストとかファイルへの書き込みのやり方分かれば、APIのデータのキャッシュなんかに使えそうですね。
今後はリクエストやエラー処理、テストとかその辺をもう少しおさえようかなと思ってます。
