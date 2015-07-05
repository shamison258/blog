title: play_meet_up_2
date: 2015-07-05 14:54:57
tags:
- scala
- playframework
categories:
- Scala
---

Scala全く分からないのに行ってきました〜.
せっかくなので頑張ってまとめたい！(無理)

[Play meetup 2 - 日本Playframeworkユーザー会 | Doorkeeper](http://bit.ly/1Cim9QK)

<!--more-->
---

## Play 2.3 から 2.4 へアップデートした話\(@ussy00 さん\)
- 資料: [Play 2.3 から 2.4 へアップデートした話](http://bit.ly/1CiqByK)

#### 変更について
- DI -> Dependency Injection
  - [依存性の注入 - Wikipedia](http://bit.ly/1CimZNh)
  - 2.4のスタイルでは
- i18n
  - 国際化対応の際ハマる感\(?\)
- 設定キーの変更はあるものの警告のみで動くっちゃ動く
- plugins は modules へ
- controllerはobjectからclassへ
  - 2.3からの移行には`routesGenerator := InjectedRoutesGenerator`(?)
  - 少しずつやるならroutesで\@をつかう
- GlobalSettingは分解される
  - DIをつかう...(?)

#### 変更の現状, 移行
- 3〜4人運用
- まずはPlay2.3スタイルでコンパイルを通し, 徐々に2.4に変えてく
- Redis
- ScalikeJDBC + (scalikejdbc-play-adapter ) + HikariCPを使用している
  - HikariCPがデフォ
  - BoneCPはオワコン\(みたいな?\)
  - BoneCPも使える

#### いつごろまでに移行したほうが良さ気？
- Play3.0.0 は来年の6月予定
  - `Remove global state`
  - Play2.5.0 時点で`global state`は消える予定
- 来年の3月までには移行したい？
- Play2.4は3.0に向けたスタート地点
  - 新規は古い情報に惑わされないようにしよう☆

#### 感想
- DIが分からないつらい

---

## なぜPlayのコントローラで継続モナドを使うと便利なのか？ -ドワンゴアカウントシステム新機能開発事例より-\(@pab_tech さん\)

- 資料: [なぜPlayのコントローラで継続モナドを使うと便利なのか？](http://bit.ly/1Ciozie)


- モナディック関数
  - 引数 をもらい モナドを返す
- 関数合成すると

資料に書いてあるなーって思ってたら書くことが消えていた...
\(単純に理解が及んでない\(=残念理解力\&圧倒的知識不足\)というのが8割はある\)

#### 感想
- モナド分からないつらい
- でもコード綺麗不思議

---

## play2-auth-social の紹介\(@gakuzzzz さん\)
- スライドはナシ
  - github [play2-auth](https://github.com/t2v/play2-auth)
- 認証周りのライブラリ
  - 現状Facebook, Github, Twitter, Slackに対応
- 現状ドキュメントは無いのでサンプルをみよう
  - 日本語だ！ -> [日本語版README](https://github.com/t2v/play2-auth/blob/master/README.ja.md)
- こんなのもあるよ -> [action-zipper](https://github.com/t2v/action-zipper)

#### 感想
- Scalaやろう\(´･\_･\`\) ...

---

## Reactive Streams 入門\(@okapies さん\)
- 資料: [Reactive Streams 入門 #jjug](http://bit.ly/1GZ3GoG)
- 補足資料: [Play and Reactive Streams #play_ja](http://bit.ly/1GZ3LZB)

- Reactive Streamとは
  - `Back-Pressure付きの非同期ストリーム処理`の標準を定める仕様
  - 最終目標はJava9に入れること(!)

#### Reactive \#とは
3つに分けて考える
- Reactive Programming
-
#### プログラミングモデル(Reactive Programming)
- 手続き型
  - 上から下にだだーっと
  - 変更が合ったら再度実行
- データフローを考える
  - 関数と関数をつなぎ合わせたもの
  - 変更の伝播
- 1. データフローを記述するためのプログラミングモデル
- 2. 変更の伝播をプログラムがやってくれる
- 見てる感じすごい関数型って感じ???
- FRP
  - composability
- Future/Promise
  - Not RP(仲間ーって感じ)
  - 変更の伝播はない

#### アーキテクチャ(Reactive Manifesto)
- Reactive Manifestoとは
  - Reactive Systemsへの支持を呼びかける文書
- 時代は小規模システム -> 大規模システム
- 大規模システムの構築を知ろう
  - 実際の大規模システムの設計原則を考察
  - -> システムの設計原則をReactive Systemsと呼ぼう
- 具体例は??
  - 挙げられてない...
  - マイクロサービスと親和性高そう
    - でかいサービスを一気にやらずに小さいサービスを非同期でつなげることで分割(ってこと?)

#### ランタイム(Reactive Streams)
- 非同期ストリーム処理 + `Non-blocking back pressure`
- Publisherはリクエストされた分だけSubscriberに渡す
  - Back-Pressureは伝播するのでいい感じの**流れ**ができる
- 実装
  - Akka Streams
  - RxJava
  - etc...
- DBアクセスライブラリ
  - Slick 3.0
  - ReactiveMongo
  - etc...
    - これいる？
    - -> 例えばJDBCとか同期APIだしつらみ...
    - -> 全てがReactiveに(!)
- Reactive Streamsの今後
  - Java9で標準
  - JSにも欲しい
- Akka Streams
  - AkkaベースのReactive Streamsの実装
  - ゆくゆくはPlay Frameworkの基盤に

#### まとめ
- 並行処理とか非同期プログラミングは恐れる必要はない!

#### 感想
- すごい！
- わかりやすい\(分かったとは言ってない\)
- Twitterから: [JJUG ナイトセミナーで Reactive Streams について発表しました](http://okapies.hateblo.jp/entry/2015/06/26/024505)

---

## LT
- 多分まとめられる力などない
- 資料等抜けがあります...

#### pixivにおけるPlayとThrift
- [pixivにおけるPlayとThrift](http://bit.ly/1LLTzsS)
- Playを社内ツールで導入
- ThriftはRPCフレームワーク
- はえぇ...

#### 例外のlogを快適に
- 資料: [例外のlogを快適に](http://bit.ly/1LLTsxv)
- Playの例外のLogながい〜〜〜
- conf/logger.xmlいじればおｋ？
- logbackはいい感じにかける〜〜?
  - -> Play 2.4からはいる(というかlogbackをアプデすればOK)
- 使う〜〜
  - 文字列マッチングじゃーん(！？)
- よっていい感じに作った

#### 小規模開発でのPlay
- evolution ではなく Flyway
- 便利ライブラリ
  - scalacashe

#### iterateeつらい
- つらいの？
- つらそうだ...

#### i18nの話
- 資料: [Play 2 (Scala) i18n Patterns](http://krrrr38.github.io/slides/play2-i18n-patterns/#0)

#### Play+Scalaはハッカソンに向くか
- 実際はハッカソンではRubyとかnodeとか
- フレームワークならRuby or Node(ちらちらPython)
- コンパイル待つのがストレス?
- Rubyとかだと結構コンパイル通っちゃう的な
- Play!なら安全(語弊がある)に開発できる〜

#### Secure Cookieへの道のり
- mackarel
  - Playでできてる
- Play 2.4なら簡単だよ

---

## 総括
- 行ってみるかってノリで行ってみたら結構楽しかったので良さがあった
- Playを趣味や, 大学で使う上で, まだ設定等が甘々でしか無いことに気づいた
  - CPとか使ってない...
  - そもそもScalaじゃないヾ(\*ﾟｰﾟ)ｼ
- S c a l a つ か っ て な い や ん わ た し
- Scalaを使おうと思った
- 次回(？)等にしっかりとした理解ができるようになりたい...

---

### 参考にしたもの

- [ScalaのPlay Framework 2.4で変更されたっぽい点 - Qiita](http://qiita.com/yoshikyoto/items/f789527c5674d2c80d6c)
- [play2-authの認可設定部分のカスタマイズ（自分の場合） | つかびーの技術日記](http://bit.ly/1GZ2m53)
