---
title: WP Social Bookmarking Light のツイートボタンを修正しました
author: コニタン
type: post
date: 2013-11-07T23:20:20+00:00
url: /archives/390
wordtwit_post_info:
  - 'O:8:"stdClass":14:{s:6:"manual";b:0;s:11:"tweet_times";s:1:"1";s:5:"delay";s:2:"15";s:7:"enabled";s:1:"1";s:10:"separation";i:60;s:7:"version";s:5:"3.0.3";s:14:"tweet_template";b:0;s:6:"status";i:2;s:6:"result";a:0:{}s:13:"tweet_counter";i:4;s:13:"tweet_log_ids";a:3:{i:0;i:405;i:1;i:406;i:2;i:407;}s:9:"hash_tags";a:0:{}s:8:"accounts";a:1:{i:0;s:6:"skd_nw";}s:4:"text";s:122:"Blog更新  投稿:  Social Bookmarking Lightのツイートボタンの設定を見直した - http://tinyurl.com/ocn3r74";}'
wordtwit_posted_tweets:
  - 'a:3:{i:0;i:405;i:1;i:406;i:2;i:407;}'
categories:
  - クリエイティブ
tags:
  - WordPress
  - プラグイン

---
簡単にブックマークのボタンを表示出来る <a href="http://wordpress.org/plugins/wp---/" target="_blank">WP Social Bookmarking Light</a>。
  
これのうち、最も使われるのはのツイートボタンとFaceBookのいいねボタンかなって思います。

このうちツイートボタンの内容がちょっと不便かな～って思ったので修正しました。

<!--more-->

### 今回行ったこと

  * ブログタイトルの入力
  * via()の設定

これを行っていなかったので、<a href="http://peng-note.com/archives/374" target="_blank">前回の記事</a>をツイートする場合こうなりました。

[<img src="https://i1.wp.com/peng-note.com/images/2013/11/8cfcb82718c8ab960fa668866e49b329-300x170.png?fit=300%2C170" alt="タイトルとURLのみ…" class="aligncenter size-medium wp-image-401" srcset="https://i0.wp.com/peng-note.com/images/2013/11/8cfcb82718c8ab960fa668866e49b329.png?resize=300%2C170 300w, https://i0.wp.com/peng-note.com/images/2013/11/8cfcb82718c8ab960fa668866e49b329.png?w=544 544w" sizes="(max-width: 300px) 100vw, 300px" data-recalc-dims="1" />][1]

どこの記事かも分からないし、ツイートされても分かんない！
  
実際、前回の記事に対して、<a href="http://stocker.jp/" target="_blank">Stocker.jp</a>のなつきさんにツイートして頂いていたのに全く気付かず。気付いたのは記事書く前でした…。

### ブログタイトルの入力

まずは、ブログタイトルを入れて、どこの記事か分かるようにしました！

参考記事：<a href="http://gucciz03.com/twitibl-1311" target="_blank">WP で記事タイトルとブログ名の表示方法</a>

やり方としては、プラグインのソースに少し書き加えるといった感じで、
  
プラグイン -> インストール済みのプラグイン -> WP の編集 -> wp&#8212;/modules/services.php

最初の関数に、

    
    function WP Social Bookmarking Light ( $url, $title, $blogname )
    {
        $title = $this->to_utf8( $title );
        $this->blogname = $this->to_utf8( $blogname );
        $this->url = $url;
        $this->title = $title;
        $this->encode_url = rawurlencode( $url );
        $this->encode_title = rawurlencode( $title );
        $this->encode_blogname = rawurlencode( $this->blogname );
    }
    

これを、

    
    function WP Social Bookmarking Light( $url, $title, $blogname )
    {
        $title = $this->to_utf8( $title );
        $this->blogname = $this->to_utf8( $blogname );
        $this->url = $url;
        $this->title = $title;
        $this->encode_url = rawurlencode( $url );
        $this->encode_title = rawurlencode( $title ) . ' | ' . rawurlencode( $this->blogname );
        $this->encode_blogname = rawurlencode( $this->blogname );
    }
    

こう書き換えます。

変わったのはココ

    
    $this->encode_title = rawurlencode( $title ) . ' | ' . rawurlencode( $this->blogname );
    <code></pre>
    <p>下から三行目 encode_titleの末尾に . ' | ' . rawurlencode( $this->blogname )が加わりました。<br />
    見てみるとなるほどって思う。なるほど。</p>
    <p>これで区切りの文字「｜」とブログ名が入るようになりました！</p>
    <p><a href="https://i1.wp.com/peng-note.com/images/2013/11/9100c672ca61891c6e84183fbc0c135f.png"><img src="https://i0.wp.com/peng-note.com/images/2013/11/9100c672ca61891c6e84183fbc0c135f-300x158.png?fit=300%2C158" alt="ブログ名が表示された" class="aligncenter size-medium wp-image-400" srcset="https://i1.wp.com/peng-note.com/images/2013/11/9100c672ca61891c6e84183fbc0c135f.png?resize=300%2C158 300w, https://i1.wp.com/peng-note.com/images/2013/11/9100c672ca61891c6e84183fbc0c135f.png?w=538 538w" sizes="(max-width: 300px) 100vw, 300px" data-recalc-dims="1" /></a></p>
    <p>(-∀-).o0( 作者側でこれ直しておいて欲しいな〜 )</p>
    <h3>via()の設定</h3>
    <p>viaの設定をすることで、誰かが記事をツイートした場合、リプが飛んでくるようになります。<br />
    これで反応ができるね！＼ｱﾘｶﾞﾀｲ！／</p>
    <p><a href="https://i0.wp.com/peng-note.com/images/2013/11/878c9c20ff0bebce83feef608ea9778f.png"><img src="https://i0.wp.com/peng-note.com/images/2013/11/878c9c20ff0bebce83feef608ea9778f-300x164.png?fit=300%2C164" alt="viaを設定した結果" class="aligncenter size-medium wp-image-392" srcset="https://i0.wp.com/peng-note.com/images/2013/11/878c9c20ff0bebce83feef608ea9778f.png?resize=300%2C164 300w, https://i0.wp.com/peng-note.com/images/2013/11/878c9c20ff0bebce83feef608ea9778f.png?w=536 536w" sizes="(max-width: 300px) 100vw, 300px" data-recalc-dims="1" /></a></p>
    <p>こんな感じになります。</p>
    <p>方法としては、<br />
    設定 -> WP Social Bookmarking Light -> Twitterのタブ</p>
    <p><a href="https://i2.wp.com/peng-note.com/images/2013/11/2b43bdbe1d68a6b185a662a32b76e734.png"><img src="https://i2.wp.com/peng-note.com/images/2013/11/2b43bdbe1d68a6b185a662a32b76e734-300x245.png?fit=300%2C245" alt="viaの部分にを入れる" class="aligncenter size-medium wp-image-394" srcset="https://i2.wp.com/peng-note.com/images/2013/11/2b43bdbe1d68a6b185a662a32b76e734.png?resize=300%2C245 300w, https://i2.wp.com/peng-note.com/images/2013/11/2b43bdbe1d68a6b185a662a32b76e734.png?w=443 443w" sizes="(max-width: 300px) 100vw, 300px" data-recalc-dims="1" /></a></p>
    <p>viaの部分のテキストフォームに自分のIDを入力します。<br />
    これで先ほどの画像の様にツイートの内容にが入るはずです。</p>
    <p>よくこのプラグインの設定で、デフォルトのままで十分ですといった記事がありますが、に関してはここまでやっておいた方がいいんじゃないかなって思います。</p>

 [1]: https://i0.wp.com/peng-note.com/images/2013/11/8cfcb82718c8ab960fa668866e49b329.png