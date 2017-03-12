---
title: concrete5 で任意のタグ選択時に一覧を表示するページを作る
author: コニタン
type: post
date: 2017-02-05T22:40:47+00:00
url: /archives/2039
wordtwit_post_info:
  - 'O:8:"stdClass":13:{s:6:"manual";b:0;s:11:"tweet_times";i:1;s:5:"delay";s:1:"0";s:7:"enabled";b:1;s:10:"separation";s:3:"270";s:7:"version";s:3:"3.7";s:14:"tweet_template";b:0;s:6:"status";i:4;s:6:"result";a:0:{}s:13:"tweet_counter";i:1;s:13:"tweet_log_ids";a:0:{}s:9:"hash_tags";a:0:{}s:8:"accounts";a:1:{i:0;s:6:"skd_nw";}}'
categories:
  - クリエイティブ
tags:
  - concrete5

---
ブログシステムでよくある、記事に設置したタグを選択するとそのタグが含まれた他のページの一覧を表示するページに遷移するあれを作るときの覚書です。
  
※WordPressの経験がある方なら、あれのタグ機能のイメージ。

## 環境

concrete5 の以下のバージョンで動作確認しています。
  
v5.7.5.13

## タグを作成 & 設置

タグ自体は管理画面のページとテーマ > 属性 > カスタム属性で作れます。
  
ハンドル名は色んなページや書籍を参考に tags に。

concrete5のタグの機能はブロックを置くだけで設置できます。ただ、単に設置するだけだとタグ自体にリンクはつかず、措定の動きは出来ません。

## 選択されたタグを含んだページを一覧出力するページを作成

一覧を出力する用のページを新たに作成し、ページリストを設置します。

ページリストのブロックでは以下の設定にチェックを付けます。
  
その他の絞り込み
  
「他のブロックからこのページリストの絞り込みを有効にする。」

ページ付けや表示件数はお好みで。

## 一覧ページへのリンクを作る

タグブロックの設定で、「タグからページリストにリンクして絞り込む」という項目があり、ここに先程作成した一覧表示用のページを指定します。これでタグを押した時に一覧ページに遷移することが出来るようになりました。

これで別ページで出力出来るようになりました。