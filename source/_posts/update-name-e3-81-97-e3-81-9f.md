title: 'update_nameした[v1.0]'
tags:
  - ArchLinux
  - scala
  - systemd
  - twitter4j
  - update_name
id: 19
categories:
  - 未分類
date: 2015-02-16 18:43:02
---

出来ました → [github](https://github.com/shamison258/update_name_sc "github")

<!--more-->

躓いたところはtwitter4jの仕様を忘れてしまった部分.

update_nameするときはtwitter apiの[update_profile](https://dev.twitter.com/rest/reference/post/account/update_profile "update_profile")を使う感じなのですが,
その際にuserのname以外にurlとlocationとdescriptionが必要のようです.
(nullに指定したら変更されないとかだったらもう知らん)

よってuserの情報を取らなきゃいけない.(その場所がわからなかった...)

使ったのはtwitterクラスのshowIdメソッドでした.
ググって探してなるほどなって感じ.
あとは難なくいけました.

しかし今回初めてscalaで書いたんですが,
多分全くscalaのいいところを活かせてないです...
もともとJavaを書いていたので,JavaっぽくてちょっとNo Senceかも...
あとscalaを書いていてTry Catchを一回も書いていないけど,
いいのかなって気分ですね.Java書いてると書かないとダメやでって言われるので.

update_nameは現状VPS(Arch)で動いてます.
いつも稼働させるためにGnu Screenを使っていたのですが,
せっかくなのでということでSystemdを使う感じでやりました.
(名前としてSystemdを使うという表現が適切であるかは理解していません><)

参考にしました↓

[ArchLinuxでminecraft serverを運営するとか](http://opamp.hatenablog.jp/entry/20121201/1354356322 "ArchLinuxでminecraft serverを運営するとか")
[ArchWiki](https://wiki.archlinux.org/index.php/Systemd_%28%E6%97%A5%E6%9C%AC%E8%AA%9E%29#.E3.82.AB.E3.82.B9.E3.82.BF.E3.83.A0_.service_.E3.83.95.E3.82.A1.E3.82.A4.E3.83.AB.E3.82.92.E6.9B.B8.E3.81.8F "ArchWiki")

記事ではminecraftだったので適宜変えて,
ちょちょっと改変してやったらすんなりいけました.

Systemdは神.はっきりわかりました.