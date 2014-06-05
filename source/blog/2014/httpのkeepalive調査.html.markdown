---
title: HTTPのKeep-Aliveを調査
date: 2014-05-19 21:09 JST
tags: HTTP
category: HTTP 
published: false
---

先日参加した勉強会にて、HTTPの仕様にあるKeep-Aliveについての知識が曖昧だなと感じる場面があったので調べて記事にまとめてみました。


READMORE

## Keep-Aliveとは

前述の通りKeep-AliveとはWebの高速化のための仕組みとして、HTTPプロトコル仕様に組み込まれている機能です。
ちなみに(Keep-Aliveの仕様)[https://tools.ietf.org/html/rfc2616#section-8.1]はこちらにあります。

以前のWebHTTPリクエスト1つに対して1つのTCPコネクションを張っていたいたそうです。
これでは効率が悪いので1つのTCPコネクションを複数のHTTPリクエストで使いまわせるようにしよう、というのがKeep-Aliveの基本的なアイデアになります。

### KeepAlive設定例
## KeppAliveのメリット 
### 3wayハンドシェイク
### tcp スロースタートについて
##http2.0について
