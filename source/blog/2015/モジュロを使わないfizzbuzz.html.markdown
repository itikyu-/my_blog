---
title: 剰余演算子を使わないFizzBuzz
date: 2015-04-29 17:20 JST
tags: Ruby
category: Ruby
---

先日,転職活動の際にこの問題を出されて回答しました。
FizzBuzz自体は非常に有名ですし簡単なので問題ないです.
ただ,剰余(モジュロ)を利用せずに書けというのは初挑戦だったため少し考えさせられてしまいました.

普通はどんな回答が多いのかなと思って軽くググったんですが,この派生問題も有名なんですね.
ググった範囲の中では自分と同じアイデアがありませんでしたので,お手軽な記事にしてみました。

READMORE

言語はRubyで書いています.
Gistのテストも兼ねてGistを使った埋め込みでコードを埋め込んでみています.

<script src="https://gist.github.com/132e44bc9bb2dae0e3c7.js"></script>

読んでのごとく,アイデアは非常に単純です.

1. 3や5で割り切れるということは小数はない.
2. 小数が無いのであれば,計算結果が整数型でも浮動小数点型でも値が一致するはず.

Rubyの仕様を利用して型を暗黙的に変換して比較しているので,Java等の別言語の場合は注意が必要ですね.
