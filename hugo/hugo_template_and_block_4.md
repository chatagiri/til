---
title: "Hugoのtemplatingを理解したい(4)"
date: 2023-05-10T00:00:00+09:00
categories:
  - hugo
tags:
  - hugo
bookComments: false
bookSearchExclude: false
---

# Hugoのtemplatingを理解したい(4: Hugo Parameters, Use Content Parameters, Use Site Configuration Parameters)
- https://gohugo.io/templates/introduction/ を読む

## Hugo Parameters
- Hugo管理下全体に与えたいraw parameterは、defaultのconfigファイルや、`hugo --config config_hoge.yml`で指定する設定ファイルに記載すること
- ページ単位でparameterを与えたい場合は、Page毎にFront matterで与えること
  - `--- ---` 囲いのアレ

## Use Content Parameters
- ページ単位でparameterを与えたい場合は、Page毎にFront matterで与えること
  - `--- ---` 囲いのアレ
```
---
notoc: true
title: Example
---

{{ if not .Params.notoc }}
<aside>
  <header>
    <a href="#{{ .Title | urlize }}">
    <h3>{{ .Title }}</h3>
    </a>
  </header>
  {{ .TableOfContents }}
</aside>
<a href="#" id="toc-toggle"></a>
{{ end }}
```
## Use Site Configuration Parameters
- Hugo管理下全体に与えたいraw parameterは、defaultのconfigファイルや、`hugo --config config_hoge.yml`で指定する設定ファイルに記載すること
- config.yaml
```
params:
  copyrighthtml: Copyright &#xA9; 2017 John Doe. All Rights Reserved.
  sidebarrecentlimit: 5
  twitteruser: spf13
```
```
{{ if .Site.Params.copyrighthtml }}
    <footer>
        <div class="text-center">{{ .Site.Params.CopyrightHTML | safeHTML }}</div>
    </footer>
{{ end }}
```
```
{{ with .Site.Params.twitteruser }}
    <div>
        <a href="https://twitter.com/{{ . }}" rel="author">
        <img src="/images/twitter.png" width="48" height="48" title="Twitter: {{ . }}" alt="Twitter"></a>
    </div>
{{ end }}
```
```
<nav>
  <h1>Recent Posts</h1>
  <ul>
  {{- range first .Site.Params.SidebarRecentLimit .Site.Pages -}}
      <li><a href="{{ .RelPermalink }}">{{ .Title }}</a></li>
  {{- end -}}
  </ul>
</nav>
```
