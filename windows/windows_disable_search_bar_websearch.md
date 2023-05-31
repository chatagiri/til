---
title: "Windows10の検索Boxを無効にする"
date: 2023-05-31T00:00:00+09:00
categories:
  - windows
tags:
  - windows
bookComments: false
bookSearchExclude: false
---

# Windows10の検索Boxを無効にする
- ソフトウェア実行の為に、windowsキーを降下したメニューの画面で文字列を入れての検索をよくやる
- Typo等で該当するソフトウェアが無い状態でEnterキーを押すと、入力単語をキーにしてEdgeでWeb検索されちゃう
- 要らないので切る
## regeditする
- `Win+R` して `regedit` 実行
- `HKEY_LOCAL_MACHINE>SOFTWARE>Microsoft>Windows>CurrentVersion>Search`を探す
- `Search`を右クリックして、`新規` -> `DWORD(32ビット)値(D)`
- `新しい値#1`を`BingSearchEnabled`に変更、値を`0`にする
- `Search`配下の`CortanaConsent`を探して値を`0`に修正する
  - もし無ければ同名のキーをDWORD(32bit)で作成する
- 再起動