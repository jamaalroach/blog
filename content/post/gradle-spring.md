+++
title = "Gradleを使って、SpringFramework+Thymeleafの環境を作る"
description = "依存管理ツールのGradleを使ってSpringFrameworkやThymeleafの環境構築を行ったのでその備忘録"
date = 2018-05-13T23:22:32+09:00
image = ""
categories = ["クリエイティブ"]
tags = ["Java", "SpringFramework", "Gradle"]
+++



最近Javaのプロジェクトに参加してるんだけど、Gradleを使ったSpringFrameworkの環境構築を任されて手探りでやってみたのでその備忘録

## 環境

- Java 8(1.8)
- Gradle 4.7
- SpringFramework 2.0.2

## Gradleって
依存管理とかビルドとかやってくれるツール。  
前やってたプロジェクトではMaven使ってたんだけど、より便利らしいのでGradleを使ってみる

参考: [Gradle入門 - Qiita](https://qiita.com/vvakame/items/83366fbfa47562fafbf4)

## Gradleのインストール
上の記事の方法1でPATHは通せた。

apt-getでも入れれたんだけど、ファイルを落としてきてPATHを通す方法を取ってみた。
やり方は上の記事の通り。ただ、バージョンだけ新しいものにしてる。

> gradle-1.4-bin.zip を解凍し、適当な所に置きます。解凍したフォルダを環境変数GRADLE_HOMEにそのパスを設定します。また、GRADLE_HOME/binにパスを通しておきます。

## プロジェクトの環境を作っていく
``build.gradle`` というファイルを作ってここに設定を書いていく。
ざっくり Node.js の package.json みたいなものって思ってるけど多分ちょっと違うのかも。

1個1個書いてもいいけど、 ``gradle init`` で雛形を作ってくれるらしいのでこれに乗っかる。
オプション無しだと1番シンプルな物ができる。 ``--java-library`` とかある。

他にどんなのがあるかと何が生成されるかは[ココが分かりやすい](http://etc9.hatenablog.com/entry/2015/04/25/020740)。

``gradle init`` だとこんな感じの**設定ファイルとコードの雛形が生成される**。

```
apply plugin: 'java'

// リポジトリの設定
repositories {
  mavenCentral()
}

// 依存関係の設定
dependencies {
  :
}
```

``apply plugin``で Gradle のプラグインを使う指定が出来るっぽいんだけどこっちはまだあんまり調べられてない。  
とりあえず eclipse を使ってるので、eclipse の指定だけ入れてる。  
SpringBoot の plugin を指定してる人が何人か居たんだけど、それを入れてるとビルドでコケるのが多かったので抜いた。

### インストールしたい物を追記していく
ここに使うJavaのバージョンと、ライブラリなんかの情報を追記していく。
Spring をいれるのでJavaのバージョン指定と依存ライブラリの追記を行う。


```
sourceCompatibility = 1.8
targetCompatibility = 1.8

ext {
  springBootVersion = '2.0.2.RELEASE'
}

dependencies {
  // gradle plugin
  compile "org.springframework.boot:spring-boot-gradle-plugin:$springBootVersion"

  // SpringBoot
  compile "org.springframework.boot:spring-boot-starter-web:$springBootVersion"
  compile 'org.springframework.boot:spring-boot-devtools:1.3.0.RELEASE'
}
```

dependencies が依存管理を行っている部分。  
ext では Spring のバージョン指定を変数みたいな形で持っていて、 dependencies でのバージョン指定に使っている。このやり方は調べる中でちょくちょく出てきたので乗っかってみてる。



### 余談1: Thymeleaf も入れておく
テンプレートエンジンの Thymeleaf を入れてみる。
dependencies に以下を追記するだけでいける。

```
dependencies {
  :
  compile "org.springframework.boot:spring-boot-starter-thymeleaf:$springBootVersion"
  compile "org.thymeleaf:thymeleaf:3.0.9.RELEASE"
  compile "org.thymeleaf:thymeleaf-spring4:3.0.9.RELEASE"
}
```

テンプレートを用意するときに、共通部分をまとめて使ったり、 ``layout:fragment`` で置き換えたりして使ってる。
Thymeleaf Layout Dialectって言うらしい。

参考: [Thymeleaf Layout Dialectのご紹介 - Developers.io](https://dev.classmethod.jp/client-side/intro-to-thymeleaf-layout-dialect/)

これをやるには別途追加する必要があって、それに気づくのに時間がかかった。以下を入れたら使えるようになった。

```
dependencies {
  :
  compile "nz.net.ultraq.thymeleaf:thymeleaf-layout-dialect:2.3.0"
}
```

### 余談2: Mavenプロジェクトに突っ込んでみる
最初イマイチ何か分かってないときに、Mavenでやってた既存プロジェクトでブランチ切って ``gradle init`` してみた。  
Mavenで設定してるものを元に作ってみようっていう発想。

ただ、実際の所Gradleが賢くって、既存プロジェクトのpom.xmlを元に設定を作ってくれたので、さてbuild.gradle触ってみるかって思ったら終わってた。(厳密に調べたわけじゃないので分からないけど)
移行はやりやすいのかも。


## やってみて
どうすんのかなーと思ってたけど結構情報があったりCLIで雛形の生成をやってくれるのはいいなーって思った。  
どこまで出来るのか把握しきれてないんだけど、便利そうだしJavaプロジェクトはまだまだこれからなので、もうちょっと調べておこうと思う。