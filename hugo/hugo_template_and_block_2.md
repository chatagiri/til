---
title: "Hugoのtemplatingを理解したい"
date: 2023-05-03T00:00:00+09:00
categories:
  - hugo
tags:
  - hugo
bookComments: false
bookSearchExclude: false
---

# Hugoのtemplatingを理解したい(1: Basic Syntax, Variables, Functions, Includes)
- https://gohugo.io/templates/introduction/ を読む

## Basic Syntax
- Hugo builtin Variables(https://gohugo.io/variables/)の呼び出し
```
{{ .Title }}
```

- ユーザ定義変数の呼び出し
```
{{ $address }}
```

- 関数呼び出し時の引数はスペース区切り
```
{{ FUNCTION ARG1 ARG2 .. }}
{{ add 1 2 }}
```

- 各ページのfront matterからの値取り出し
```
{{ .Params.bar }}
```
```
---
title: "記事Title"
date: 2023-05-01T00:00:00+09:00
categories:
  - categoryName
tags:
  - tagName
---
```
```
{{ .Params.categories }}
{{ .Params.tags }}
```

- 括弧を使って式のグルーピング(ステートメント内は改行可)
```
{{ if or (isset .Params "alt") (isset .Params "caption") }} Caption {{ end }}

{{ if or
  (isset .Params "alt")
  (isset .Params "caption")
}}
```

- String型のリテラルには改行を含めて良い
```
{{ $msg := `Line one.
Line two.` }}
```

## Variables
- 変数呼び出し
```
<title>{{ Pages.Title }}</title>
```

- templateのスコープ内であれば、Prefixとしてドットを付けるだけで良い(例: page template配下)
```
<title>{{ .Title }}</title>
```

- カスタム変数($)の宣言(:=)と呼び出し
```
{{ $address := "123 Main St." }}
<ul>{{ $address }}</ul>
```

- カスタム変数の再定義(=)
```
{{ $var := "Hugo Page" }}
{{ if .IsHome }}
    {{ $var = "Hugo Home" }}
{{ end }}
Var is {{ $var }}
```

## Functions
- [template function](https://gohugo.io/functions/)を参照のこと
- 数値の足し算結果を表示
```
{{ add 1 2 }}
// 3 が表示される
```
- 数値の比較結果(bool)を表示
```
{{ lt 1 2}}
// true が表示される
```

## Includes
- Includeするテンプレートの格納ディレクトリは、必ずHugoが読むディレクトリのうち `layouts/` を読む。
- current contextを渡す際は、末尾にドット (.) を含めること
- `partial関数`と、`template関数`でのInclude方法がある。
- partial関数でのテンプレート読み込み
```
// layouts/partials/header.htmlを読み込む例
{{ partial "header.html" . }}
```
- template関数での[Internalテンプレート](https://gohugo.io/templates/internal/)読み込み
```
// internal template opengraphの読み込み例
{{ template "_internal/opengraph.html" . }}
```