---
title: UEFI環境でLinuxマニュアルインストールしてみた
date: 2014-06-30 20:13 JST
tags: Linux
category: Linux
published: false
---

[先日の記事](/雑記/ラップトップの購入を検討中.html)でぐだぐだと好き勝手言っていましたが，結局ThinkPadのT440sという機種を購入しました．
OS無しが選べて少しでも安く購入できれば嬉しかったのですがスペック的には満足できるものを選べたので良かったです．

で，インストールするディストリを何にするか迷っていたんですが，結局[Arch linux](https://www.archlinux.org/)にすることにしました．
最小構成からいじれるのは勉強になりますし，やはり楽しいです．
Gentooも少し考えたのですが今回はCPUが超低電圧版なのでやめときました．

現在環境構築中なのですが，モバイル用途の環境構築とか，最早新しいと言えるか怪しいUEFI環境でのインストールとか，自分にとって初めて経験が多くて結構苦戦しています．

作業しててコンピュータのブート周りの知識が貧弱だと改めて感じたので，今回はインストール作業時に色々と調べて回った知識を文章にして整理してみようと思う．具体的にはUEFIとこれまでのBIOSとの対比をブート時の時系列に沿って行ってみる．果たして自分にそんなレベル高いことが出来るのかどうか．

READMORE

### UEFIとは

詳しいは

今回は大きく分けて2箇所でハマりました．

1. UEFIのセキュアブートのせいでArchのインストールディスクが起動しない
2. マスターブートレコード(MBR)とGUIDパーティションテーブル(GPT)の設定法の違い

まず最初にセキュアブートについて．
今回のインストールではArchの Bootable USB を利用してインストールを行ったのですが，

今見れば些細なショボいミスなんですが，調子に乗って英語マニュアル読みながら導入したりしてたので大事な所サラッと見落としてて大変めんどくさい事になってしまいました．
