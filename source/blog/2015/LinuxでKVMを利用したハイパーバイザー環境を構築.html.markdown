---
title: LinuxのKVMを利用したハイパーバイザー環境を作成
date: 2015-04-09 18:27 JST
tags: GNU/Linux,Arch,KVM 
category: linux
---
[Linux From Scrach](http://www.linuxfromscratch.org/)というプロジェクトがあります.
「最小構成のLinuxを全ソースコンパイルしながら構築しよう」という非常に興味深いやつです.
こいつの完走を密かに今年の目標の1つと立てています。

時間があるうちに少しずつ進めていこうということで,今回は作業用の仮想環境の準備までをやっていきたいと思います.
VirtualBoxとかでも良かったんですが,せっかくの勉強なのでLinuxのKVM機能を使ってやってみようと思い立ちました.
環境構築の手順を本記事にまとめたいと思います.<br>
※ホスト環境はArchLinuxを利用しています.

READMORE

### ハードウェアサポートとLinuxカーネルモジュールの確認

まずは前提条件の確認をします.
以下の2つが必要です.

1. CPUの仮想化サポート機能がONになっていること
2. KVMとvirtioモジュールがロードされていること

1についてはlscpuコマンドの結果を確認.
Virtualizationという項目があり,VT-x等と記載があればOKです.
もし,存在していないようであれば利用しているCPUがそもそもサポートしていないか,もしくはBIOSの設定で切られている可能性があります.

続いて2の方ですが,こちらはlsmodコマンドで確認可能です.
結構出力が多いので「kvm」や「virtio」でgrepをかけてやってロードされているかを確認して下さい.
もし,いないようであれば以下の確認を

1. /lib/moduleの配下にそれらしきファイルがある　→　手動ロードしてやるか起動時ロード設定を入れてやる
2. それらしきファイルがない　→　モジュールをインストールして下さい
3. そもそもカーネルのバージョンが低くて対応していないORコンパイルオプションがOFFになってた　→　生きろ

ここまでで事前確認終了です.

### 必要パッケージのインストール

今回は「qemu」「libvirt」パッケージをインストールします.
libvirtの方はqemuのGUIフロントエンドのためにインストールしているだけなので,別パッケージで代替可能です.
今回は特に利用予定は無いですが便利なCUIツール何かもまとめて提供してくれるらしくlibvirtを選択しています.

<pre class="brush: shell" title="pacman install">
# pacman -S qemu libvirt
</pre>

### 仮想マシンの作成

まずはおもむろに仮想ディスクを用意.
とりあえず5GB程度を指定してみる.

<pre class="brush: shell" title="create_disk-image">
$ qemu-img create -f raw test_image 5G
</pre>

そして,用意しておいたDebianのminimal-isoイメージを使ってインストールを開始.

<pre class="brush: shell" title="install_v-machine">
$ qemu-system-x86_64 -cdrom debian-7.8.0-amd64-netinst.iso -boot order=d test_img
</pre>

ここからはDebianの通常のインストールなので省略.
次回以降の起動も同じコマンドからです.

<pre class="brush: shell" title="running_v-machine">
$ qemu-system-x86_64 -m 512M -cpu host -smp 2 -net nic,model=virtio -enable-kvm test_img
</pre>

色々つけているオプションはリソース割り当てのオプション.
詳細は各自で…


### おわり

とりあえず以上で最低限は終わりでしょうか.
ここまでやるとVagrantとかも触れてみたい気分になるな.
