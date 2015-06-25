title: 'Hello Hexo!'
date: 2015-06-25 09:43:57
tags:
- javascript
- blog
- hexo
categories:
- web
date: 2015-06-25
---

ブログをWordpressからHexoに移行しました〜
<!-- more-->

Wordpress用に鯖を借りていましたが, ブログもそんなに書かないから
「オカネモッタイナイ」ってことで, gh-pagesを使ってブログ構築しました.

移行するにあたっては, migrateのツールがあったのでめちょ簡単に, 移行できました.(詳細はggr!)
(なおWordpressのMarkdownの記法を, ちょっと特殊な記法にしていたせいで色々面倒だったけどそれは愛嬌)

# Q.なぜHexo?

## A. HexoがNodeJSでできていたから

gh-pagesで使われるのは大抵, 「Jekyll」とか「Octopress」とか「Hexo」みたいな雰囲気を
このページ↓から感じ取ったため.
- [Static Site Generators](https://staticsitegenerators.net/)

Jekyllは使ったことがあったのですが,
あまりにもユーザが多そうだから**おれはHexoを選ぶぜ的な天邪鬼な思想**と,
なんとなく**NodeJSに興味**あるという理由からHexoを選択しました.

# よくわからんかったこと

Deployする際にタイトル部分のリンクが
- `http://shamison258.github.io/blog`
ではなく
- `http://shamison258.github.io/`
になってしまって, どうにかこうにかやってもうまくいかなかった...

ので,

解決するために,
`header.ejs`に`blog/[URL]`みたいに書き加えて
ゴリ押しで解決してます.(とても悲しい(´･\_･\`))

まぁとりあえずは動いたしいいかな()

# 参考にしたサイト
- [所要時間3分!? Github PagesとHEXOで爆速ブログ構築してみよう！ | 株式会社LIG](http://liginc.co.jp/web/programming/server/104594)
- [Hexo](https://hexo.io/)
- [hexojs/hexo-theme-landscape](https://github.com/hexojs/hexo-theme-landscape)
- [HexoでGitHubにブログをつくる | Crack the Game, Win a Jackpot](http://yukiyamashina.github.io/blog/2014/09/19/blog-at-github-using-hexo/)
- [Deployment | Hexo](https://hexo.io/docs/deployment.html)
