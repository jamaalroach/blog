---
title: WordPressで期間限定で記事を表示する方法メモ
author: コニタン
type: post
date: 2014-09-15T05:26:04+00:00
url: /archives/1203
wordtwit_post_info:
  - 'O:8:"stdClass":13:{s:6:"manual";b:0;s:11:"tweet_times";s:1:"1";s:5:"delay";s:1:"0";s:7:"enabled";s:1:"1";s:10:"separation";i:60;s:7:"version";s:3:"3.7";s:14:"tweet_template";b:0;s:6:"status";i:2;s:6:"result";a:0:{}s:13:"tweet_counter";i:5;s:13:"tweet_log_ids";a:4:{i:0;i:1212;i:1;i:1213;i:2;i:1214;i:3;i:1215;}s:9:"hash_tags";a:0:{}s:8:"accounts";a:1:{i:0;s:6:"skd_nw";}}'
wordtwit_posted_tweets:
  - 'a:4:{i:0;i:1212;i:1;i:1213;i:2;i:1214;i:3;i:1215;}'
categories:
  - クリエイティブ
tags:
  - WordPress

---
大学で所属している団体のサイトを運営しているのですが、そこでイベントの情報を発信していました。その情報はイベントの期間が過ぎたら消したかったのですが、どうすればいいかという問題がなかなか解決出来ず、そんな感じの事をされていた<a href="http://juso-coworking.com/" target="_blank">JUSO Coworking</a>オーナーの<a href="https://twitter.com/witch_doktor" target="_blank">@witch_doktor</a>さんに聞いてみました。

<!--more-->

### 管理画面側の設定

これどうやって消す(非表示)んだろうなーってずっと考えていたんですが、表示したものを消すのではなく、そもそも**期間外のデータを引っ張ってこない**というのが正解でした。(多分)

判別するために投稿にカスタムフィールドで値をもたせます。
  
<img src="https://i0.wp.com/peng-note.com/images/2014/09/a578fbf4defb9b145c63f2c986bf68ad.png?fit=346%2C109" alt="カスタムフィールドで値を入力" class="aligncenter size-full wp-image-1206" srcset="https://i0.wp.com/peng-note.com/images/2014/09/a578fbf4defb9b145c63f2c986bf68ad.png?w=346 346w, https://i0.wp.com/peng-note.com/images/2014/09/a578fbf4defb9b145c63f2c986bf68ad.png?resize=300%2C94 300w" sizes="(max-width: 346px) 100vw, 346px" data-recalc-dims="1" />
  
<small>※<a href="https://ja.wordpress.org/plugins/custom-field-suite/" target="_blank">CustomFieldSuite</a>を使用しています。</small>
  
画像のように開催日をハイフンなどを抜きで入力しました。
  
開催日を判別するので、key は invent にしてあります。

### テーマ側での処理

カスタムフィールドで設定した値をmeta_queryに指定し該当するものだけ取得する処理を書きます。

参考：<a href="http://elearn.jp/wpman/column/c20110915_01.html" target="_blank">query_posts（WP_Queryクラス）でカスタムフィールドを使う:WordPress私的マニュアル</a>

    
    <?php
    // 現在の日付け
    $now = date('Ymd');
    
    // 引き出す情報の指定(inventの値が現在の時間より大きい(今日から先)のもの)
    $args = array(
            'meta_query' => array(
                array( 
    　　　　　　　　　　　　　　　　　　　　　　　　　　'key' => 'invent',
                 'value' => $now,
                 'compare' => '>=',
                 'type' => 'NUMERIC'
                )
            )
    );
    
    $the_query = new WP_Query( $args );
    
    if($the_query->have_posts()) :
    　　while($the_query->have_posts() ) :
    　　　　$the_query->the_post();
    　　　　// 以下表示したい記事のテンプレートとか
    　　endwhile;
    endif;
    ?>
    

これで期日が過ぎたものは表示されなくなります。