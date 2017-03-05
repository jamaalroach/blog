---
title: 画像やテキストを拡大表示するjQueryプラグインfancyboxを使いました。
author: コニタン
type: post
date: 2014-02-27T22:16:38+00:00
url: /archives/750
wordtwit_post_info:
  - 'O:8:"stdClass":13:{s:6:"manual";b:0;s:11:"tweet_times";i:1;s:5:"delay";s:1:"0";s:7:"enabled";s:1:"1";s:10:"separation";s:3:"300";s:7:"version";s:5:"3.5.1";s:14:"tweet_template";b:0;s:6:"status";i:2;s:6:"result";a:0:{}s:13:"tweet_counter";i:4;s:13:"tweet_log_ids";a:3:{i:0;i:759;i:1;i:760;i:2;i:761;}s:9:"hash_tags";a:0:{}s:8:"accounts";a:1:{i:0;s:6:"skd_nw";}}'
wordtwit_posted_tweets:
  - 'a:3:{i:0;i:759;i:1;i:760;i:2;i:761;}'
categories:
  - クリエイティブ
tags:
  - jQuery
  - Webデザイン
  - まとめ
  - プラグイン

---
先日、大学での活動の紹介ページをリデザインしました。

今回のプラグインはそこで使ったjQueryプラグインです。
  
<!--more-->


  
っていうシリーズPart2。

前回に引き続き、リデザインするときに使ったjQueryプラグインです。
  
過去記事：<a href="http://peng-note.com/archives/742" target="_blank">あっという間にスライダーを設置！jQueryプラグインのbxsliderを使いました。</a>

もうひとつ使ったプラグインは、fancyboxです。

参考記事：
  
<a href="http://web-pc.net/jquery006" target="_blank">Webサイトなど、HTMLファイルをLightBox風に表示するjQuery &#8211; ホームページ制作やリニューアル印刷物デザインなら大阪のWPC</a>
  
<a href="http://chun-oki.sw8field.com/webworks/20121102/960.html" target="_blank">Fancyboxでiframeの高さをコンテンツにあわせてみたり | ちゅんもす置き場</a>

どの辺がファンシーなのって思ってたそのバチが当たったのか色々手こずりました。

### fancybox

Lightbox系のプラグインで、画像をクリックすると拡大表示したり、同時に画像のtitleを表示できたりするプラグインです。

<a href="http://fancybox.net/" target="_blank">Fancybox &#8211; Fancy jQuery lightbox alternative</a>

ちなみに画像だけじゃなく、テキストも表示できるようです。

### 使い方

今回使った用途としては、タイトルのようなものを用意し、それをクリックするとそれの細かい内容をfancyboxで表示するというものでした。

まずは、ホームページ右上のリンクからファイルをダウンロードします。
  
<a href="http://fancybox.net/" target="_blank">Fancybox &#8211; Fancy jQuery lightbox alternative</a>

今回は、メンテナンス性を考えてiframで別ファイルから読み込んで表示させることにしました。

#### HTML

    
    <link rel="stylesheet" href="css/jquery.fancybox.css">
    <script type="text/javascript" src="http://ajax.googleapis.com/ajax/libs/jquery/1.8.3/jquery.min.js"></script>
    <script type="text/javascript" src="js/jquery.fancybox.js"></script>
    

以上をhead内に記述します。

更に、fancyboxで表示する為にクリックする要素を、aタグで囲みます。

    
    <a href="別のhtmlファイル" class="sample">
    <p>ここに何か</p>
    </a>
    

#### JavaScript

<pre><code class="javascript">
&lt;script&gt;
  $(document).ready(function() {
    $("a.sample").fancybox({});
  });
&lt;/script&gt;
</code></pre>

body閉じタグ前に記述します。

更に、オプションを加える事ができるので、こう記述してみました。

    
    <script>
      $(document).ready(function() {
        $("a.sample").fancybox({
          'type'          : 'iframe',
          'transitionIn'  : 'elastic',
          'transitionOut' : 'elastic',
          'width'         : '480',
          'autoScale'     : false,
          'scrolling'     : 'no',
          'onComplete'      : function () {
            $('#fancybox-frame').load(function(){
              $('#fancybox-content').height($(this).contents().find('body').height()+50);
              $('#fancybox-overlay').height($(document).height());
            });
          }
        });
      });
    </script>
    

色んなサイトの記述を参考にしました。

色々なカスタマイズができるので表現の幅が広くていいプラグインだと思います。