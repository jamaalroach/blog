+++
categories = ["クリエイティブ"]
description = "Pythonの開発環境が色々あった中、pyenv+virtualenvにしていたんだけど、こう使う！みたいなものがよく分かっていなくて、暗い道を進んでた。そんな中、venvいいぞというお告げをもらったので触ってみた。"
title = "Pythonのvenv(pyvenv)で環境を作る"
author = "Daisuke Konishi"
date = "2017-03-29T12:08:54+09:00"
tags = ["Python"]

+++

Pythonの開発環境が色々あった中、pyenv+virtualenvにしていたんだけど、こう使う！みたいなものがよく分かっていなくて、暗い道を進んでた。そんな中、venvいいぞというお告げをもらったので触ってみた。正直この手のやり方って覚えてられないので覚書。


## バージョン
Python 3.6.0


## 環境を作る
とりあえず新規プロジェクト始まったときに、ディレクトリ作って、そこに有効化するっぽい。

多分流れはこんな感じ

1. ディレクトリを作成
2. venvで初期化
3. venvの有効化
お好みのパッケージをpipでインストール

### ディレクトリを作成してvenvで初期化
他の人の例を参考にコマンドを叩いてみた。
```
$ mkdir ディレクトリ名
$ pyvenv イイカンジの環境名
```

下記エラーが出た
```
WARNING: the pyenv script is deprecated in favour of `python3.6 -m venv`
```

非推奨っぽいので、以下に変えてみる
```
$ python3.6 -m venv イイカンジの環境名
```

ほんの数秒待った後以下のようなディレクトリが作成された
```
├── bin
├── include
├── lib
└── pyvenv.cfg
```


### venvの有効化

venvを有効化する
```
$ cd 作ったディレクトリ
$ source ./bin/activate
```

プロンプトが以下のようになったら有効化できてるみたい
```
(イイカンジの環境名) $
```

無効化するときは、以下
```
$ deactivate
```

./bin/deactivate
ではないんだ。そんなのねぇよ！って怒られた。

とりあえず有効化してるときにpipが使えて、環境ごとに使い分けてくれるみたい。

#### 試しにpipでパッケージを入れる

```
(イイカンジの環境名) $ pip install pep8
```

入れられた。

pip freeze でファイルに書き出しておくと、他の人が参照した時も -r でインストールできるみたい。
```
$ pip freeze > requirements.txt
$ pip install -r requirements.txt
```

[pip freeze — pip 9.0.1 documentation](https://pip.pypa.io/en/stable/reference/pip_freeze/)
