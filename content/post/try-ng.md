+++
title = "Angularでデータバインディングとルーティング周りを触ってみた"
description = "仕事でAngularを使いそうだったので、少し触ってみた話"
categories = ["クリエイティブ"]
image = "images/common/angularjs.jpg"
tags = ["JavaScript", "Angular"]
date = 2018-01-29T01:49:48+09:00
author = "Daisuke Konishi"
+++

仕事でAngularを触りそうな気配がしてきたので少し触っておこうと思ってよく聞く辺りに触れてみた。
バージョンによって呼称が違うとかって話を小耳に挟んだんだけど、どうやらプロジェクトで使うのは1系らしいのでv1.6.0でいってみた。

## データバインディング(?)とか
View側で、``{{args}}`` と書けば値を埋め込むことができた。

また、JSファイル側(Controller)でコントローラーを定義して、View側のコントローラーで操作したいタグ(bodyタグとか)にコントローラーを指定すると、ViewとControllerを紐付ける事ができた。これによって$scopeにViewで扱う値や関数を入れる事でViewとControllerでやり取りできるようになったみたい。ちょっと感動した。

```
<html ng-app="App">
  <head>
    :
    <script src="https://ajax.googleapis.com/ajax/libs/angularjs/1.6.0/angular.min.js"></script>
  </head>
  <body ng-controller="AppController">
    <input type="text" ng-model="displayText">
    <input type="button" value="Go" ng-click="display()">
    <h1>{{text}}</h1>
  </body>
</html>
```

```
var app = angular.module('App', []);

app.controller('AppController', function($scope) {
  $scope.display = function() {
    var str = $scope.displayText;
    $scope.text = str;
  }
}
```

なんとなくReactより分かりやすい感じはあるけど、HTML側への準備が多い(色んな属性つけないといけない)所を考えるとどうかなって感じ。慣れな気はするけど。

onClickにあたるものとか、repeatのための指定があったりと色々用意されてるものっぽい。

## ルーティング
angular-routeというものを使って、ルーティングにも少し触れてみた。

ルーティング担当のコントローラーを作って、アクセスによって``tepmlateUrl``で指定したファイルを読み込んで ``ng-view`` の中にレンダリングをかけるというものっぽい。  
まるっと変える必要がない場合でもごそっと変わりそうだけど、細かく分けたりって出来るんだろうか。

あと、一緒にそれぞれで使用するコントローラーも指定するらしい。
ViewとControllerを分けやすそう。

```
var app = angular.module("App", ["ngRoute"]);

app.config(function ($routeProvider) {
  $routeProvider
    .when('/', {
      templateUrl: 'page1.html',
      controller: 'page1_controller'
    })
    .when('/page2', {
      templateUrl: 'page2.html',
      controller: 'page2_controller'
    })
});

app.controller('page1_controller', function ($scope) {});
app.controller('page2_controller', function ($scope) {});
```

```
<body>
  <div ng-view></div>
</body>
```

## 参考にしたもの

- [AngularJS入門](https://qiita.com/daiki7nohe/items/769c8f2f60a0e94c5e56)
- [AngularJSのルーティング](https://qiita.com/daiki7nohe/items/c9678097a8e7efe58256#_reference-b0c6dd5a57113aa616db)


## やってみて
今回はふんわり触ったって感じ。
ルーティング周りはまだまだ疑問が残るし、他のモジュールがどんな感じなのかもわかんないし、そもそもAngular自体の機能に全然触れられてない気がするのでもう少し深掘りしないとって感じ。どこまでやるか分かんないけど、頑張ろう