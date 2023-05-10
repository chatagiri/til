---
title: "Hugoのtemplatingを理解したい(2)"
date: 2023-05-03T00:00:00+09:00
categories:
  - hugo
tags:
  - hugo
bookComments: false
bookSearchExclude: false
---

# Hugoのtemplatingを理解したい(2: Logic, Conditionals, Pipes)
- https://gohugo.io/templates/introduction/ を読む

## Logic
- block内での変数の取り出し
```
{{ range $array }}
    {{ . }}
{{ end }}
```

- 配列要素名の指定と取り出し
```
{{ range $elem_val := $array }}
    {{ $elem_val }}
{{ end }}
```

- index-valueでの配列アクセス
```
{{ range $elem_index, $elem_val := $array }}
   {{ $elem_index }} -- {{ $elem_val }}
{{ end }}
```

- key-valueでの配列アクセス
```
{{ range $elem_key, $elem_val := $map }}
   {{ $elem_key }} -- {{ $elem_val }}
{{ end }}
```

- 要素が空の配列へのアクセス
```
{{ range $array }}
    {{ . }}
{{ else }}
    <!-- $arrayが空の時のみ -->
{{ end }}
```

## Conditionals 
- with: 変数が定義されている or True であるかどうかを判定
```
{{ with .Params.title }}
    <h4>{{ . }}</h4>
{{ end }}
```

- with else: 変数が定義されている or True であるかどうかを判定
```
{{ with .Param "description" }}
    {{ . }}
{{ else }}
    {{ .Summary }}
{{ end }}
```

- if: 条件判定型with
```
{{ if isset .Params "title" }}
    <h4>{{ index .Params "title" }}</h4>
{{ end }}
```

- if else: 条件判定型 with else
```
{{ if (isset .Params "description") }}
    {{ index .Params "description" }}
{{ else }}
    {{ .Summary }}
{{ end }}
```

- if, else if, else
```
{{ if (isset .Params "description") }}
    {{ index .Params "description" }}
{{ else if (isset .Params "summary") }}
    {{ index .Params "summary" }}
{{ else }}
    {{ .Summary }}
{{ end }}
```

- and, or: 条件式を連結
```
{{ if (and (or (isset .Params "title") (isset .Params "caption")) (isset .Params "attr")) }}
```

## Pipes
- shellよろしく関数の値引き渡しをpipeで実行できる。
```
{{ shuffle (seq 1 5) }}
---
{{ (seq 1 5) | shuffle }}
```

```
{{ if or (or (isset .Params "title") (isset .Params "caption")) (isset .Params "attr") }}
Stuff Here
{{ end }}
---
{{ if isset .Params "caption" | or isset .Params "title" | or isset .Params "attr" }}
Stuff Here
{{ end }}
```