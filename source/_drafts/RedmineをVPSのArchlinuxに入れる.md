title: RedmineをVPSのArchlinuxに入れる.
tags:
  - ArchLinux
  - MariaDB
  - Redmine
id: 122
categories:
  - 未分類
---

# MariaDBの導入

pacman でいれたら下記が書いてあった.
```
:: You need to initialize the MariaDB data directory prior to starting
   the service. This can be done with mysql_install_db command, e.g.:
   mysql_install_db --user=mysql --basedir=/usr --datadir=/var/lib/mysql

```
よってこれをやる

```
mysql_install_db --user=mysql --basedir=/usr --datadir=/var/lib/mysql
```


なんか言われたから一応メモ

```
To start mysqld at boot time you have to copy
support-files/mysql.server to the right place for your system

PLEASE REMEMBER TO SET A PASSWORD FOR THE MariaDB root USER !
To do so, start the server, then issue the following commands:

'/usr/bin/mysqladmin' -u root password 'new-password'
'/usr/bin/mysqladmin' -u root -h vps password 'new-password'

Alternatively you can run:
'/usr/bin/mysql_secure_installation'

which will also give you the option of removing the test
databases and anonymous user created by default.  This is
strongly recommended for production servers.

See the MariaDB Knowledgebase at http://mariadb.com/kb or the
MySQL manual for more instructions.

You can start the MariaDB daemon with:
cd '/usr' ; /usr/bin/mysqld_safe --datadir='/var/lib/mysql'

You can test the MariaDB daemon with mysql-test-run.pl
cd '/usr/mysql-test' ; perl mysql-test-run.pl

Please report any problems at http://mariadb.org/jira

The latest information about MariaDB is available at http://mariadb.org/.
You can find additional information about the MySQL part at:
http://dev.mysql.com
Support MariaDB development by buying support/new features from MariaDB
Corporation Ab. You can contact us about this at sales@mariadb.com.
Alternatively consider joining our community based development effort:
http://mariadb.com/kb/en/contributing-to-the-mariadb-project/

```

よくわからんがサービスを開始

```
sudo systemctl start mysqld.service
```

これをやると良いっぽいらしいのでする.パスワードを決められる.

```
mysql_secure_installation
```

Redmine用ユーザの作成のために下記

```
mysql -u root -p
```

でRedmine用のユーザと, データベースの作成

```
CREATE DATABASE redmine CHARACTER SET UTF8;
CREATE USER 'redmine'@'localhost' IDENTIFIED BY 'my_password';
GRANT ALL PRIVILEGES ON redmine.* TO 'redmine'@'localhost';
```

# Remineの設定

```
cd /usr/share/webapps/redmine/
cp database.yml.example database.yml
```

で, databaese.ymlを編集

```
production:
  adapter: mysql2
  database: redmine
  host: localhost
  port: &lt;ポート番号&gt;
  username: redmine
  password: "&lt;パスワード&gt;"
  encoding: utf8
```

## 参考

*   [wiki](https://archlinuxjp.kusakata.com/wiki/MySQL?rdfrom=https%3A%2F%2Fwiki.archlinux.org%2Findex.php%3Ftitle%3DMySQL_%28%25E6%2597%25A5%25E6%259C%25AC%25E8%25AA%259E%29%26redirect%3Dno#.E3.83.A6.E3.83.BC.E3.82.B6.E3.83.BC.E3.82.92.E8.BF.BD.E5.8A.A0.E3.81.99.E3.82.8B)
*   [Archlinuxでredmineを動かしてみた - opamp_sando's blog](http://bit.ly/1DADiyr)
