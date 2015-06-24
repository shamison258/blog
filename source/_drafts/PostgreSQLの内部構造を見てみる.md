title: PostgreSQLの内部構造を見てみる
id: 101
categories:
  - 未分類
tags:
---

なんか読む
<!--more-->

ざっくり読んで気になったことまとめ

## 他のRDBMSとデータ領域の構造が異なる

Oracle, MySQLのInnoDBストレージエンジンは,
データ領域をいくつかの巨大なファイルとして確保し,
複数のテーブルデータをファイル内部で一括管理.

ぽすぐれは, テーブル毎にファイル確保.
DBの物理的な正体はディレクトリ.
テーブルファイルはDBに対応するディレクトリに置かれる.

*   InnoDB - Wikipedia http://bit.ly/1IpxKib

## 実際のデータの場所は？

自分の環境だと以下にある

```
/var/lib/pgsql/data
```

以下の場合もある

```
/usr/local/pgsql/data
```

## どれだけのデータベースがあるの？

`psql`でシェル起動して

```
select datname, oid from pg_database;
```

を実行すると, oidといまあるデータベースが確認できる.

```
postgres=# select datname, oid from pg_database;
datname  |  oid  
----------+-------
template1 |     1
template0 | 12137
postgres  | 12142
book      | 16396
(4 行)
```

bookは以前テストで追加したもの.

データベースは`/var/lib/pgsql/data`内の
`base`ディレクトリに入っていて,
実際に`book`とかの名前で管理しておらず,
`oid`で管理してある.

```
[postgres@arch data]$ ls base/
    1  12137  12142  16396
```


1はtemplate1, 16396はbookに対応している.

なおテーブルは

```
[postgres@arch data]$ psql book
  psql (9.4.1)
  "help" でヘルプを表示します.

book=# select relname, relfilenode from pg_class;
                   relname                 | relfilenode
  -----------------------------------------+-------------
   pg_statistic                            |       11874
   pg_type                                 |           0
   pg_toast_16397                          |       16400
   pg_toast_16397_index                    |       16402
   countries                               |       16397  -- 自分で定義したテーブル
   pg_toast_2619                           |       11876
   pg_toast_2619_index                     |       11878
  ...
  省略
```

のようにしたら見れた.
