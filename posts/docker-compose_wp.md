---
layout: post
title: Docker compose + Wordpress
excerpt: 本日（2020/03/02）より、「今から本気出すブログを開設することを宣言します！」
tags: blog
---

見出し見出し見出し見出し見出し見出し見出し見出し見出し見出し見出し見出し見出し見出し見出し

-----

## 概要
たいぶ乗り遅れていますが、Docker（compose）を使用して、Wordpressのローカル開発環境を整えようと思い立ったので、備忘録的な記事を投稿します。

Dockerはやってみようとずっと思っていましたが、フロントエンドの技術を追っているうちに後回しとなってしまっていました。

とりあえず表示する＋永続化？くらいしかしていないので、随時更新のスタイルをとると思います。

## Docker compose
Dockerの管理を容易にする機能…くらいの理解度・解釈です。

## 手順
dockerの公式に書いてあるんです。  
<a href="https://docs.docker.com/compose/wordpress/">docker docs</a>
```
version: '3.3'

services:
   db:
     image: mysql:5.7
     volumes:
       - db_data:/var/lib/mysql
     restart: always
     environment:
       MYSQL_ROOT_PASSWORD: somewordpress
       MYSQL_DATABASE: wordpress
       MYSQL_USER: wordpress
       MYSQL_PASSWORD: wordpress

   wordpress:
     depends_on:
       - db
     image: wordpress:latest
     ports:
       - "8000:80"
     restart: always
     environment:
       WORDPRESS_DB_HOST: db:3306
       WORDPRESS_DB_USER: wordpress
       WORDPRESS_DB_PASSWORD: wordpress
       WORDPRESS_DB_NAME: wordpress
volumes:
    db_data: {}
```
閲覧
```
 localhost:8000
```
ポイントとしては mysql は latest を使用しないところ。なんかうまくいかないらしい。  
要件として盛り込まれない限りはこの設定で立てる事にする。

この状態だと永続化というかローカルにファイルが保持されないので、ホストPCにマウントするように volumes の設定をする。

```
wordpress:
  volumes:
    - ./html:/var/www/html
```
