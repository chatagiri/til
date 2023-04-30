---
title: "my.cnfのキーはアンダースコアとハイフンどちらが正しいのか"
date: 2023-04-30T00:00:00+09:00
# bookComments: false
# bookSearchExclude: false
---
# my.cnfのキーはアンダースコアとハイフンどちらが正しいのか?
## tl;dr
- ハイフンでもアンスコでもどっちでも良い。
- mariadb側で良しなに[解釈してくれる](https://mariadb.com/kb/en/configuring-mariadb-connectorc-with-option-files/#option-file-syntax)。
- 正し、公式docではアンダースコア繋がりで書かれているので、アンダースコアにしておくのが健全そう。
---
## my.cnfのキー表記ブレ問題
mariadbやmysqlの設定ファイル my.cnf を弄っていると、キーがハイフン繋がりだったりアンスコ繋がりだったり、疎らであることが多い。
 
設定は解釈してくれるし、使用上は問題無いが、なんとなく気持ち悪い。
```console
[client]                           
port=3306
socket=/tmp/mysql.sock

[mysqld]
port=3306
socket=/tmp/mysql.sock
key_buffer_size=16M
max_allowed_packet=8M

[mysqld_safe]
log-error=/var/log/mysqld.log
pid-file=/var/run/mysqld/mysqld.pid
```
---
## 公式ドキュメントを読む
Mariadbは公式ドキュメントに[ココ](https://mariadb.com/kb/en/configuring-mariadb-connectorc-with-option-files/#option-file-syntax)に書いてあった。
> Dashes (-) and underscores (_) in options are interchangeable in MariaDB Connector C 3.1.1 and later. In versions before that, options must be specified exactly as they are defined. See CONC-395 for more information.

が、MySQLのドキュメントでsyntaxについて明確に記載されている箇所は見つけられなかった。

一方、mysql/mariadbともに、[my.cnfの設定例ドキュメント](https://mariadb.com/kb/en/mysqld_safe/#configuring-the-open-files-limit)ではアンダースコア繋がりのものが多い。
> ```
> [mysqld_safe]
> core_file_size=unlimited
> ```

公式docがそう言っているのであれば、ハイフン繋がりよりはアンスコ繋がりの方がbetterなのだろう。

