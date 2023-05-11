---
title: "bash/shellscriptのリダイレクト構文を復習しておく"
date: 2023-05-11T00:00:00+09:00
categories:
  - shellscript
tags:
  - shellscript
  - bash
bookComments: false
bookSearchExclude: false
---
# bash/shellscriptのリダイレクト構文を復習しておく
## 構文例
| 構文名 | 説明 | 使用例 |
|---|---|---|
| `>` | 標準出力をファイルにリダイレクトする。 | `echo "Hello, world!" > file.txt` |
| `>>` | 標準出力をファイルに追記する。 | `echo "Hello, again!" >> file.txt` |
| `<` | ファイルから標準入力をリダイレクトする。 | `cat < file.txt` |
| `2>` | 標準エラー出力をファイルにリダイレクトする。 | `ls /nonexistentdir 2> error.txt` |
| `2>>` | 標準エラー出力をファイルに追記する。 | `ls /nonexistentdir 2>> error.txt` |
| `&>` | 標準出力と標準エラー出力の両方を同じファイルにリダイレクトする。 | `ls /nonexistentdir &> output.txt` |
| `&>>` | 標準出力と標準エラー出力の両方を同じファイルに追記する。 | `ls /nonexistentdir &>> output.txt` |
| `<()` | プロセス置換で、コマンドの出力を一時的なファイルにリダイレクトする。 | `diff <(ls dir1) <(ls dir2)` |
| `>()` | プロセス置換で、コマンドの入力を一時的なファイルにリダイレクトする。 | `echo "Hello, world!" > >(cat)` |
| `<<` | ヒアドキュメントで、標準入力に直接マルチライン文字列を供給する。 | `cat << EOF\nHello,\nThis is a multi-line text.\nEOF` |
| `<<<` | ヒアストリングで、標準入力に直接文字列を供給する。 | `cat <<< "Hello, world!"` |
| `>!` | 強制的に出力をリダイレクトする。 | `echo "Hello, world!" >! file.txt` |
| `<>` | ファイルを読み書きの両方のために開く。 | `command <> file.txt` |
| `>|` | noclobberオプションが設定されていても、ファイルを強制的に上書きする。 | `echo "Hello, world!" >| file.txt` |
| `{var}>` and `{var}<` | ファイルディスクリプタを開き、その番号を変数に保存する。 | `exec {fd}>file.txt\necho "Hello, world!" >&$fd\nexec {fd}>&-` |
| `n>&m` and `n<&m` | ファイルディスクリプタnをmにコピーする。これにより、標準入力、標準出力、標準エラー以外のファイルディスクリプタの出力をリダイレクトできる。 | `command 3>&1 1>&2 2>&3` |
| `1>&2` | 標準出力を標準エラー出力にリダイレクトする。 | `echo "This is an error" 1>&2` |
| `2>&1` | 標準エラー出力を標準出力にリダイレクトする。 | `command 2>&1` |
| `0< FILE` or `< FILE` | ファイルから標準入力をリダイレクトする。 | `0< file.txt` or `< file.txt` |
| `1> FILE` or `> FILE` | 標準出力をファイルにリダイレクトする。 | `1> file.txt` or `> file.txt` |
| `2> FILE` | 標準エラー出力をファイルにリダイレクトする。 | `2> file.txt` |
| `n> FILE` | ファイルディスクリプタnをファイルにリダイレクトする。 | `3> file.txt` |
| `n< FILE` | ファイルからファイルディスクリプタnへリダイレクトする。 | `3< file.txt` |
| `n>&-` | ファイルディスクリプタnをクローズする。 | `3>&-` |
| `n<&-` | ファイルディスクリプタnからの入力をクローズする。 | `3<&-` |
| `n>&m-` | ファイルディスクリプタnをmにコピーし、その後mを閉じる。 | `command 3>&1-` |
| `n<&m-` | ファイルディスクリプタnをmにコピーし、その後mを閉じる。 | `command 3<&1-` |
