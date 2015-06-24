title: 人として最低限のLinuxの知識が無い
id: 117
categories:
  - 未分類
tags:
---

ので「Linuxシステム実践入門」を読んでみるよ.
気になった部分しか書かないのであしからず
<!--more-->

# ディレクトリ構造

<table>
<thead>
<tr>
  <th align="center">場所</th>
  <th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr>
  <td align="center">/</td>
  <td align="left">トップディレクトリ. Linuxカーネル本体vmlinuzがあったりする.</td>
</tr>
<tr>
  <td align="center">/boot</td>
  <td align="left">ブートローダが入ってたりする. Grubとか.vmlinuzがここにある場合もある(筆者の環境ではそうだった)</td>
</tr>
<tr>
  <td align="center">/etc</td>
  <td align="left">設定ファイル格納場所. NetworkManagerとかsslとか大体ここに設定ファイルある.</td>
</tr>
<tr>
  <td align="center">/bin</td>
  <td align="left">コマンドが配置される. これをbashやらzshやらが読み込んでいろいろ使える.</td>
</tr>
<tr>
  <td align="center">/sbin</td>
  <td align="left">システム管理者用コマンドが配置される.</td>
</tr>
<tr>
  <td align="center">/usr</td>
  <td align="left">ユーザで共有するデータ保持に使われる.</td>
</tr>
<tr>
  <td align="center">/usr/local</td>
  <td align="left">ローカル環境用ディレクトリ. ディストリで用意されていないものをここで展開してビルドしたりとかする.</td>
</tr>
<tr>
  <td align="center">/home</td>
  <td align="left">ホームディレクトリ</td>
</tr>
<tr>
  <td align="center">/var</td>
  <td align="left">variable(変わりやすい)からこの名前になっている. ログや一時ファイル等がここに置かれる.</td>
</tr>
<tr>
  <td align="center">/proc</td>
  <td align="left">システム情報を処理するための手段を提供する擬似ファイルシステム. (pseudoファイルシステム)</td>
</tr>
<tr>
  <td align="center">/sys</td>
  <td align="left"></td>
</tr>
</tbody>
</table>