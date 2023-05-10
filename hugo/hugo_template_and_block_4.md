---
title: "Hugoのtemplatingを理解したい(3)"
date: 2023-05-09T00:00:00+09:00
categories:
  - hugo
tags:
  - hugo
bookComments: false
bookSearchExclude: false
---

# Hugoのtemplatingを理解したい(3: context, whitespace, comments)
- https://gohugo.io/templates/introduction/ を読む

## Context(Alias: ドット ".")
- ドットは常にcurrent contextを参照する。
- 但し、ループ内におけるドットは、ループ内の現在の値が参照される。
- ループ内からPageレベルのデータにアクセスする
  1. コンテキストに依存しない変数をrange ループ外で宣言する
  ```
  {{ $title := .Site.Title }}
  <ul>
  {{ range .Params.tags }}
      <li>
          <a href="/tags/{{ . | urlize }}">{{ . }}</a>
          - {{ $title }}
      </li>
  {{ end }}
  </ul>
   ```

  2. "$"prefixを使用して、global contextにアクセスする
  ```
  <ul>
    {{ range .Params.tags }}
    <li>
      <a href="/tags/{{ . | urlize }}">{{ . }}</a>
              - {{ $.Site.Title }}
    </li>
  {{ end }}
  </ul>
  ```

## Whitespace
- whitespace入り出力
```
<div>
  {{ .Title }}
</div>
```
```
<div>
  Hello, World!
</div>
```

- 空白, 水平タブ, CR, 改行を出力から削除する
```
<div>
  {{- .Title -}}
</div>
```
```
<div>Hello, World!</div>
```

## Comments
- テンプレートでのコメントアウト"/* */"
```
Bonsoir, {{/* {{ add 0 + 2 }} */}}Eliott.

```

- html comment out
```
{{ "<!-- This is an HTML comment -->" | safeHTML }}

{{ printf "<!-- Our website is named: %s -->" .Site.Title | safeHTML }}

```

- コメントアウト内は描画こそされないが、変数展開は実施される。
```
<!-- {{ $author := "Emma Goldman" }} was a great woman. -->
{{ $author }}

---
Emma Goldman
```