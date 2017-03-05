---
title: WordPressのカスタム投稿タイプをfunctions.phpからプラグインに移行した
author: コニタン
type: post
date: 2015-12-07T00:13:13+00:00
url: /archives/1726
wordtwit_post_info:
  - 'O:8:"stdClass":13:{s:6:"manual";b:0;s:11:"tweet_times";s:1:"1";s:5:"delay";s:1:"0";s:7:"enabled";s:1:"1";s:10:"separation";i:60;s:7:"version";s:3:"3.7";s:14:"tweet_template";b:0;s:6:"status";i:2;s:6:"result";a:0:{}s:13:"tweet_counter";i:5;s:13:"tweet_log_ids";a:4:{i:0;i:1731;i:1;i:1732;i:2;i:1733;i:3;i:1734;}s:9:"hash_tags";a:0:{}s:8:"accounts";a:1:{i:0;s:6:"skd_nw";}}'
wordtwit_posted_tweets:
  - 'a:4:{i:0;i:1731;i:1;i:1732;i:2;i:1733;i:3;i:1734;}'
categories:
  - クリエイティブ
tags:
  - WordPress
  - プラグイン

---
以前、別に運営しているWordPressを用いたサイトでカスタム投稿タイプを実装しました。
  
その際勉強したかった事もあって、自作テーマのfunctions.phpにコードを書いて実装しました。

こんな感じ。大体Codexに載っているものそのままだった気がします。

functions.php

<pre><code class="php">&lt;?php
// カスタム投稿タイプ
add_action( 'init', 'create_post_type' );
function create_post_type() {
  register_post_type( 'event',
    array(
      'labels' =&gt; array(
        'name' =&gt; __( 'イベント情報' ),
        'singular_name' =&gt; __( 'イベント情報' )
      ),
      'public' =&gt; true,
      'menu_position' =&gt; 5,// 投稿の下
      'supports' =&gt; array('title', 'editor', 'thumbnail', 'author', 'revisions')
    )
  );
}
?&gt;
</code></pre>

実際動いていた(動作確認: WordPress 4.3.1)のですが、先日開催されたWordCamp Kansai 2015で、Plugin Territoryの話をチラッと聞いて( ﾟдﾟ)ﾊｯ!となったわけです。

> Plugin Territory
    
> プラグインテリトリーと言うのは、テーマに依存せずそのサイトの設定になるような項目 

参考:
  
[WordPressのテーマを作る時に気をつけている事 | Cntlog][1]
  
[Plugin Territory – WordPressのその処理はテーマでやるべきかプラグインでやるべきか？ | Firegoby][2]

Analyticsとかカスタム投稿タイプとか**テーマ変えて消えたら困る機能**とかはプラグインで本体側に実装しろよみたいな話？

ちょくちょくプラグインで導入しましたって人見かけて、え～コードで実装出来んじゃんって思ってたけどこういうことだったの…。

今回扱ってるサイトも過去に1, 2度テーマを変えた事が有ったんですけど、そろそろまた変えるんじゃないかなーと思い、今回のプラグイン導入に至りました。消えると怖いし。

## Custom Post Type UIの導入

とりあえずググったら出たし、更新もわりと最近だったのでコレを導入しました。

<a href="https://wordpress.org/plugins/custom-post-type-ui/" target="_blank">WordPress › Custom Post Type UI « WordPress Plugins</a>

いつもどおり、管理画面のプラグインの所から検索してインストール、有効化です。

するとサイドバー下に項目が現れるので、そこから add/edit Post Types を選択して早速カスタム投稿タイプを作ります。
  
<img src="https://i2.wp.com/lolipop-646524cb2e85409d.ssl-lolipop.jp/images/2015/12/f78735c96e60d88ef31a0c472e8611bf.png?resize=164%2C295&#038;ssl=1" alt="サイドバーに項目が現れた" class="aligncenter size-full wp-image-1728" data-recalc-dims="1" />

上で書いたコードを元にこんな感じで入力しました。
  
<img src="https://i2.wp.com/lolipop-646524cb2e85409d.ssl-lolipop.jp/images/2015/12/78d235accbc4951649f099fde43e440d.png?resize=1064%2C732&#038;ssl=1" alt="Custom Post Type UIの設定画面。上のコードを元に入力した" class="aligncenter size-full wp-image-1727" srcset="https://i0.wp.com/peng-note.com/images/2015/12/78d235accbc4951649f099fde43e440d.png?w=1064 1064w, https://i0.wp.com/peng-note.com/images/2015/12/78d235accbc4951649f099fde43e440d.png?resize=300%2C206 300w, https://i0.wp.com/peng-note.com/images/2015/12/78d235accbc4951649f099fde43e440d.png?resize=660%2C454 660w" sizes="(max-width: 1000px) 100vw, 1000px" data-recalc-dims="1" />

他にも右の項目で例えば以下のことなんかも設定できるようです。

  * サイドバーでの表示(label)
  * メニューの位置
  * カスタム投稿タイプでサポートするもの 
      * エディター
      * サムネイル
      * カスタムフィールド
      * etc.

あとはSave Pot Typeをクリックするだけ。

## カスタム投稿タイプの表示

表示するためのコードは以前使っていたものから変更の必要はありませんでした。

今回編集したサイトでは少し変わった出力を行っていたので、分かりやすいCodexのものを拝借しました。

<pre><code class="php">&lt;?php
$args = array( 'post_type' =&gt; 'event', 'posts_per_page' =&gt; 10 );
$loop = new WP_Query( $args );

while ( $loop-&gt;have_posts() ) : $loop-&gt;the_post();
  the_title();
  echo '&lt;div class="entry-content"&gt;';
  the_content();
  echo '&lt;/div&gt;';
endwhile;
?&gt;
</code></pre><aside ="ref"> 参考: 

<a href="https://wpdocs.osdn.jp/%E3%82%AB%E3%82%B9%E3%82%BF%E3%83%A0%E6%8A%95%E7%A8%BF%E3%82%BF%E3%82%A4%E3%83%97#.E3.82.AB.E3.82.B9.E3.82.BF.E3.83.A0.E6.8A.95.E7.A8.BF.E3.82.BF.E3.82.A4.E3.83.97" target="_blank">投稿タイプ &#8211; WordPress Codex 日本語版</a>
  
</aside> 

## まとめ

Custom Post Type UIを導入するだけで簡単にカスタム投稿タイプが実装できました。

実装も早いしこっちでやっちゃう方が良いのかなー

 [1]: http://blog.cntlog.net/?p=1173
 [2]: https://firegoby.jp/archives/5975