title: PostgreSQLでCURD
tags:
  - postgresql
id: 78
categories:
  - データベース
date: 2015-03-25 19:05:41
---

「7つのデータベース 7つの世界」でいろんなデータベースで遊んでみよう企画, PostgreSQL編 part.2
<!--more-->

CURDとは基本的なデータベース操作のこと
* Create, Read, Update, Delete
* CURDができれば何だってできる(？)

# PostgreSQLの特徴

*   RDBMS(リレーショナルデータベースマネジメントシステム)である.
    *   [関係データベース管理システム - Wikipedia](http://bit.ly/19OAKX7)
    *   [関係データベース - Wikipedia](http://bit.ly/19OAx6h)
    *   [関係代数 (関係モデル) - Wikipedia](http://bit.ly/19OEJTv)
    *   リレーショナルデータベースは数学的なリレーション(テーブル)を使っていることからそう呼ばれる.
    *   RDBMSは集合論から派生した関係代数をもとにして構築されている.
*   SQL文を使うことで中身をいじる.
    *   SQL(= Structured Query Language)は構造化問い合わせ言語のこと.

# 事前準備

任意のユーザで
```
$ createdb book
$ psql book
```

をして, bookというデータベースをいじるよ.

# Create

作る流れ
* `create table &lt;table名&gt;`でテーブルとテーブルの構造を定義.
* `insert into &lt;tabale名&gt;`でテーブルに実際にデータを入れる.

テーブル作成.今回は2つの列を持つcountriesテーブルを作成した.

```
create table countries (
  country_code char(2) PRIMARY KEY,
  country_name text UNIQUE
);
```

2つの列には制約がありそれぞれ,

* `country_code`には`PRIMARY KEY`の制約
* `country_name`には`UNIQUE`の制約

がかけられている.
また, SQL文の最後には`;`をつける.

次に,実際にデータを入れてみる.

```
insert into countries (country_code, country_name)
values ('us', 'United Status'),
       ('jp', 'Japan'),
       ('mc', 'Mecha Cool'),
       ('ck', 'Chou kawaii'),
       ('fr', 'France'),
       ('cz', 'Czech');
```

6つの国を入れた.

2つの列には制約があるので,
重複したデータを入れると制約に引っかかり,
挿入できない.
```
-- countiriesのあとの(country_code , country_name)は二回目以降省略可
insert into countries values ('ck', 'chou kakkoii');
ERROR:  重複キーが一意性制約"countries_pkey"に違反しています
DETAIL:  キー (country_code)=(ck) はすでに存在します

insert into countries values ('mk', 'Mecha Cool');
ERROR:  重複キーが一意性制約"countries_country_name_key"に違反しています
DETAIL:  キー (country_name)=(Mecha Cool) はすでに存在します
```

この制約を一意性制約と呼ぶ.

* [一意性制約 - Wikipedia](http://bit.ly/19OMY1U)

`PRIMARY KEY`制約は一意性制約(`UNIQUE`制約)に加え`NOT NULL`制約が追加されたもの,
と考えることもできる.

* PRIMARY KEYについて詳しくは→ [主キー - Wikipedia](http://bit.ly/19ONJrM)

# Read

データを見る流れ

* `select ... from`を使う.

```
select * from countries;

 country_code | country_name  
--------------+---------------
 us           | United Status
 jp           | Japan
 mc           | Mecha Cool
 ck           | Chou kawaii
 fr           | France
 cz           | Czech
(6 行)

```

もう少し分解して見てみる.

```
select  *              -- すべての列のデータ( * )をみる
from    countries      -- countriesテーブルから
```

といった具合である.

# Delete

消す流れ
- `delete from &lt;table名&gt; where &lt;検索条件&gt;`
- DELETE文が削除可能なのは行単位での削除のみ.
- すべての行が削除されても、テーブルそのものは削除されることはない.
- 参考 → [さらっと覚えるSQL＆T-SQL入門（8）：SQL文でデータを追加・更新・削除する方法 (2/2) - ＠IT](http://www.atmarkit.co.jp/ait/articles/0709/27/news143_2.html)

今回はチェコを消してみる.

```
delete from countries
where country_code = 'cz';
```

確認↓

```
select * from public.countries ;
 country_code | country_name  
--------------+---------------
 us           | United Status
 jp           | Japan
 mc           | Mecha Cool
 ck           | Chou kawaii
 fr           | France
(5 行)
```

消えてる.

# Update

* `update &lt;table名&gt; set &lt;列名&gt; = &lt;値&gt; where &lt;検索条件&gt;`

一旦insertで適当な値を入れる.
```
insert INTO countries values ('hh', 'hogehoge');
```

確認↓

```
select * from countries;

 country_code | country_name  
--------------+---------------
 us           | United Status
 jp           | Japan
 mc           | Mecha Cool
 ck           | Chou kawaii
 fr           | France
 hh           | hogehoge
```

updateする.

```
update countries set country_name = 'homuhomu' where country_code = 'hh';
```

確認↓

```
select * from countries;

 country_code | country_name  
--------------+---------------
 us           | United Status
 jp           | Japan
 mc           | Mecha Cool
 ck           | Chou kawaii
 fr           | France
 hh           | homuhomu
```

これでCURDできた！
