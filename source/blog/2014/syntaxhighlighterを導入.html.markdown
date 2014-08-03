---
title: ブログ内のシンタックスハイライトにsyntaxHighlighterを導入
date: 2014-08-03 16:16 JST
tags: HTML/CSS, JavaScript
category: blog
---

ブログの環境改善の一環として，この筋で非常によく利用されているというsyntaxHighlighterを導入してみた．

<pre class="brush: ruby" title="hello_world.rb">  
p "Hello, World!"
</pre>

<pre class="brush: java" title="HelloWorld.java">  
public calss Main{
    public static void main(String[] args){
        System.out.println("Hello, World!");
    }
}
</pre>

こういうやつです．

Gistとか使えば比較的楽にシンタックスハイライトしてくれるらしいんだけど「Scriptタグによる動的な埋め込みだとSEO的に問題あるんじゃないの？」とか無用な心配をしてしまったのでこちらの静的に埋め込める方式を採用してみた．

今回はこれの導入作業履歴をまとめてみる．

READMORE

### 必要ファイルのダウンロード
まずは[SyntaxHighlighterのダウンロードページ](http://alexgorbatchev.com/SyntaxHighlighter/download/)から最新版のコードを落としてくる．

今回利用するファイルはこんなところ，

* scripts/shCore.js
* scripts/shAutoLoader.js
* scriptsディレクトリ内の自分の必要な言語用のファイル(shBrushXxx.js)
* styles/shCoreXxx.cssから好きなハイライトスタイルを1つ

<small>※Xxx部分はお好みで．</small><br>
<small>※[ハイライトスタイルのデモ](http://alexgorbatchev.com/SyntaxHighlighter/manual/themes/)はこちら．</small>

これらを自分のサイトのcssやJavaScript置き場に放り込んでおく．

### 読み込み処理の記述
まずは放り込んだファイルたちを読み込む．

<pre class="brush: xml" title="headタグの中">
  &lt;head&gt;
    &lt;link rel="stylesheet" href="/stylesheets/syntaxHighlighter/shCoreXxx.css" /&gt;
    &lt;script src="/javascripts/syntaxHighlighter/shCore.js"&gt;&lt;/script&gt;
    &lt;script src="/javascripts/syntaxHighlighter/shAutoloader.js"&gt;&lt;/script&gt;
  &lt;/head&gt;
</pre>
<small>※Xxx部分はお好みで．</small>

続いてbodyの終了タグの直前にこんな感じのスクリプトを書いてやる．
ちゃんと直前に書かないとうまく動かないことがあるかもしれないので注意．

<pre class="brush: javascript" title="syntaxHighlighterの実行">
  &lt;script&gt;
      SyntaxHighlighter.autoloader
      (
       "bash shell      [自分の環境のパス]/shBrushBash.js",
       "css             [自分の環境のパス]/shBrushCss.js",
       "java            [自分の環境のパス]/shBrushJava.js",
       "javascript      [自分の環境のパス]/shBrushJScript.js",
       "Ruby ruby       [自分の環境のパス]/shBrushRuby.js",
       "xml             [自分の環境のパス]/shBrushXml.js"
      );
      SyntaxHighlighter.all();
  &lt;/script&gt;
  &lt;/body&gt;
</pre>

自分が必要だった言語用のJSファイルのパスをautoloaderに登録してやる．

### 動作確認
これで準備は整ったので，ブログ内でこういうふうに書いてやれば

<pre class="brush: xml" title="デモ">
<pre class="brush: java" title="HelloWorld.java">  
public calss Main{
    public static void main(String[] args){
        System.out.println("Hello, World!");
    }
}
</pre>
</pre>

こうなる

<pre class="brush: java" title="HelloWorld.java">  
public calss Main{
    public static void main(String[] args){
        System.out.println("Hello, World!");
    }
}
</pre>

めでたし
