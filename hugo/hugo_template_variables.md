---
title: "Hugo(v0.111.3) のtempateで使える変数まとめをGPT-4にやってもらった"
date: 2023-05-01T00:00:00+09:00
# bookComments: false
# bookSearchExclude: false
---
## Site variables
- https://gohugo.io/variables/site/

| Variables | Description |
|---|---|
| `.Site.AllPages`| すべてのページの配列(region問わず)。 |
| `.Site.BaseURL` | サイト設定で定義されているサイトの基本URL。 |
| `.Site.BuildDrafts` | サイト設定で定義されているドラフトをビルドするかどうかを示すブール値（デフォルト: false）。 |
| `.Site.Copyright` | サイト設定で定義されているウェブサイトの著作権を表す文字列。 |
| `.Site.Data` | カスタムデータ。Data templateを参照。 |
| `.Site.DisqusShortname` | サイト設定で定義されているDisqus shortcode の　shortnameの文字列。 |
| `.Site.GoogleAnalytics` | サイト設定で定義されているGoogle Analyticsのトラッキングコードの文字列。 |
| `.Site.Home` | ホームページのページオブジェクトへの参照。 |
| `.Site.IsMultiLingual` | サイト内で複数の言語が使用されているかどうか。詳細は多言語を参照。 |
| `.Site.IsServer` | サイトがHugoの組み込みサーバーで提供されているかどうかを示すブール値。hugo serverを参照。 |
| `.Site.Language.Lang` | 現在のロケールの言語コード（例: en）。 |
| `.Site.Language.LanguageName` | 言語のフルネーム（例: English）。 |
| `.Site.Language.Weight` | `.Site.Languages`リスト内の順序を決定する重み。 |
| `.Site.Language` | ウェブサイトのレンダリングに使用されている言語を示す。このオブジェクトの属性は、サイト設定の言語定義で設定されます。 |
| `.Site.LanguageCode` | サイト設定で定義されている言語タグを表す文字列。 |
| `.Site.LanguagePrefix` | URLにプレフィックスを付けて正しい言語を指すために使用できます。定義された言語が1つだけでも機能します。absLangURLおよびrelLangURLの関数も参照。 |
| `.Site.Languages` | 言語の順序付けリスト（定義された重みによって順序付け）。 |
| `.Site.LastChange` | サイトに対する最も最近の変更の日時を表す文字列。この文字列は、コンテンツページのフロントマター内の日付変数に基づいています。 |
| `.Site.Menus` | サイト内のすべてのメニュー。 |
| `.Site.Pages`| 日付順に並べられたすべてのコンテンツの配列で、最新のものが最初に来ます。この配列には、現在の言語のページのみが含まれます。`.Site.Pages`を参照。 |
| `.Site.RegularPages`| 通常のページコレクションへのショートカット。`.Site.RegularPages`は、`where .Site.Pages "Kind" "page"`と同等です。`.Site.Pages`を参照。 |
| `.Site.Sections` | サイトのトップレベルのディレクトリ。 |
| `.Site.Taxonomies` | サイト全体のタクソノミー。任意のテンプレートからタクソノミーデータにアクセスするセクションも参照。 |
| `.Site.Title` | サイトのタイトルを表す文字列。 |

## Page Variables
- https://gohugo.io/variables/page/

| Variables | Description |
|---|---|
| `.Page.AlternativeOutputFormats` | 与えられたページのすべての代替フォーマットを含みます。サイトの<head>内のリンクリストに役立ちます。(出力フォーマットを参照) |
| `.Page.Aliases` | このページのエイリアス |
| `.Page.Ancestors` | 各ページの先祖を取得し、パンくずリストナビゲーションの実装複雑さを簡略化します。 |
| `.Page.BundleType` | バンドルタイプ: leaf、branch、またはページがバンドルでない場合は空の文字列。 |
| `.Page.Content` | フロントマターの下で定義されたコンテンツ自体。 |
| `.Page.Data` | このタイプのページに固有のデータ。 |
| `.Page.Date` | ページに関連する日付。.Page.Dateは、コンテンツのフロントマターの日付フィールドから引き出します。 |
| `.Page.Description` | ページの説明。 |
| `.Page.Draft` | 真偽値で、フロントマターにドラフトとしてマークされている場合はtrue。 |
| `.Page.ExpiryDate` | コンテンツが期限切れになる予定の日付。.Page.ExpiryDateは、コンテンツのフロントマターのexpirydateフィールドから引き出します。 |
| `.Page.File` | このコンテンツファイルに関連するファイルシステムのデータ。ファイル変数も参照してください。 |
| `.Page.Fragments` | このページのフラグメントを返します。ページフラグメントを参照。 |
| `.Page.FuzzyWordCount` | コンテンツ内のおおよその単語数。 |
| `.Page.IsHome` | ホームページのコンテキストでtrue。 |
| `.Page.IsNode` | 通常のコンテンツページでは常にfalse。 |
| `.Page.IsPage` | 通常のコンテンツページでは常にtrue。 |
| `.Page.IsSection` | .Page.Kindがセクションの場合はtrue。 |
| `.Page.IsTranslated` | 表示する翻訳がある場合はtrue。 |
| `.Page.Keywords` | コンテンツのメタキーワード。 |
| `.Page.Kind` | ページの種類。返される可能性のある値は、ページ、ホーム、セクション、タクソノミー、または用語です。 |
| `.Page.Language` | サイトの設定で言語の定義を指す言語オブジェクト。.Page.Language.Langは、言語コードを提供します。 |
| `.Page.Lastmod` | コンテンツが最後に変更された日付。.Page.Lastmodは、コンテンツのフロントマターのlastmodフィールドから引き出します。 |
| `.Page.LinkTitle` | コンテンツへのリンクを作成する際にアクセスします。設定されている場合、Hugoはフロントマターのlinktitleをtitleの前に使用します。 |
| `.Page.Next` | 次の通常のページを指します（Hugoのデフォルトソート順）。例：{{ with `.Page.Next `}}{{ .Permalink }}{{ end }}。最初のページから.Nextを呼び出すと、nilが返されます。|
| `.Page.NextInSection` | 同じトップレベルセクション（/blogなど）以下の次の通常ページを指します。ページはHugoのデフォルトソート順で並べられます。例：{{ with `.Page.NextInSection`}}{{ .Permalink }}{{ end }} |
| `.Page.OutputFormats` | このページに対して生成される出力フォーマットのスライス。.Page.OutputFormats.Getを使用して、特定の出力フォーマットのリンクを取得できます。 |
| `.Page.Params` | ページのフロントマターで定義されたパラメータ。 |
| `.Page.Path` | ページへの相対パス。 |
| `.Page.Permlink` | ページへの絶対URL。 |
| `.Page.Plain` | Markdownから生成されたHTMLを除く、コンテンツ内のプレーンテキスト。 |
| `.Page.PlainWords` | コンテンツ内のプレーンテキスト単語のスライス。 |
| `.Page.Prev` | 前の通常ページを指します（Hugoのデフォルトソート順）。例：{{ with `.Page.Prev `}}{{ .Permalink }}{{ end }}。最後のページから.Prevを呼び出すと、nilが返されます。 |
| `.Page.PrevInSection` | 同じトップレベルセクション（/blogなど）以下の前の通常ページを指します。ページはHugoのデフォルトソート順で並べられます。例：{{ with `.Page.PrevInSection`}}{{ .Permalink }}{{ end }} |
| `.Page.PublishDate` | コンテンツが公開された予定の日付。.Page.PublishDateは、コンテンツのフロントマターのpublishdateフィールドから引き出します。 |
| `.Page.RSSLink` | このページのRSSリンク。 |
| `.Page.RawContent` | 未処理のコンテンツテキスト。 |
| `.Page.ReadingTime` | コンテンツの推定読書時間（分）。 |
| `.Page.RelPermalink` | ページへの相対URL。 |
| `.Page.Related` | 関連性の高いページを返します。関連ページを参照。 |
| `.Page.Scratch` | ページ専用の一時変数ストア。.Scratchに対する変更は、ページのレンダリングの間のみ持続します。 |
| `.Page.Section` | このページのトップレベルセクション。 |
| `.Page.Site` | サイト全体に関連する情報のアクセスポイント。.Site変数も参照してください。 |
| `.Page.Section` | このページのトップレベルセクション。 |
| `.Page.Site` | サイト全体に関連する情報のアクセスポイント。.Site変数も参照してください。 |
| `.Page.Sitemap` | このページに関連するサイトマップの情報。 |
| `.Page.Summary` | コンテンツ内の自動要約。 |
| `.Page.TableOfContents` | ページの目次をHTML形式で提供します。 |
| `.Page.Title` | ページのタイトル。フロントマターで定義されている場合、その値が使用されます。それ以外の場合、ファイル名から生成されます。 |
| `.Page.Translations` | このページの翻訳を含むページの配列。 |
| `.Page.Type` | コンテンツのタイプ。デフォルトでは、このページのセクションになります。フロントマターでタイプを定義することもできます。 |
| `.Page.URL` | ページの相対URL。 |
| `.Page.Weight` | ページのソート順序に影響する重み。フロントマターで定義されている場合、その値が使用されます。それ以外の場合、0になります。 |
| `.Page.WordCount` | コンテンツ内の正確な単語数。 |

## Shortcode Variables
- https://gohugo.io/variables/shortcodes/

| Variables | Description |
|---|---|
| `.Shortcodes.Name` | ショートコード名 |
| `.Shortcodes.Ordinal` | 親に対するゼロベースの順序 |
| `.Shortcodes.Page` | 所有する `Page` |
| `.Shortcodes.Parent` | 入れ子のショートコードで親のショートコードコンテキストにアクセスする |
| `.Shortcodes.Position` | ページ内のショートコードのファイル名と位置 |
| `.Shortcodes.IsNamedParams` | 名前付きパラメータを使用する場合はtrueを返す |
| `.Shortcodes.Inner` | 開始と終了のショートコードタグ間のコンテンツ |
| `.Shortcodes.Scratch` | データを格納・操作するための書き込み可能なScratch |
| `.Shortcodes.InnerDeindent` | インデントが削除された.Innerを取得する |

## Taxonomy templates
- https://gohugo.io/variables/taxonomy/#term-templates

| Variables | Description |
|---|---|
| `.Taxonomy.Data.Singular` | タクソノミーの単数名 (例: tags => tag) |
| `.Taxonomy.Data.Plural` | タクソノミーの複数名 (例: tags => tags) |
| `.Taxonomy.Data.Pages` | このタクソノミーに関連する項目ページのコレクション |
| `.Taxonomy.Data.Terms` | このタクソノミーに関連する項目と加重ページのマップ |
| `.Taxonomy.Data.Terms.Alphabetical` | 昇順でアルファベット順に並べたタクソノミー関連の項目と加重ページのマップ .Taxonomy.Data.Terms.Alphabetical.Reverseで降順に並べることができる |
| `.Taxonomy.Data.Terms.ByCount` | 昇順でカウント順に並べたタクソノミー関連の項目と加重ページのマップ .Taxonomy.Data.Terms.ByCount.Reverseで降順に並べることができる |
| `.Taxonomy.Kind` | taxonomyテンプレートで描画されるページでは、.Kindはtaxonomyに設定される |
| `.Taxonomy.Type` | taxonomyテンプレートで描画されるページでは、.Typeはタクソノミー名に設定される |


## Term templates
- https://gohugo.io/variables/taxonomy/#term-templates

| Variables | Description |
|---|---|
| `.Term.Data.Singular` | タクソノミーの単数名 (例: tags => tag) |
| `.Term.Data.Plural` | タクソノミーの複数名 (例: tags => tags) |
| `.Term.Data.Pages` | このタクソノミーに関連するコンテンツページのコレクション |
| `.Term.Kind` | termテンプレートで描画されるページでは、.Kindはtermに設定される |
| `.Term.Type` | termテンプレートで描画されるページでは、.Typeはタクソノミー名に設定される |
| `.Term.Data.Term` | termそのもの (例: tag-one) |

## File Variables
- https://gohugo.io/variables/files/

| Variables | Description (日本語訳) |
|---|---|
| `.File.Path` | (string) コンテンツディレクトリに対する相対ファイルパス |
| `.File.Dir` | (string) ファイル名を除く、コンテンツディレクトリに対する相対ファイルパス |
| `.File.LogicalName` | (string) ファイル名 |
| `.File.BaseFileName` | (string) 拡張子を除いたファイル名 |
| `.File.TranslationBaseName` | (string) 拡張子と言語識別子を除いたファイル名 |
| `.File.Ext` | (string) ファイル拡張子 |
| `.File.Lang` | (string) 与えられたファイルに関連する言語 |
| `.File.ContentBaseName` | (string) ページがブランチまたはリーフバンドルの場合は、含まれているディレクトリ名、それ以外の場合は.TranslationBaseName |
| `.File.Filename` | (string) 絶対ファイルパス |
| `.File.UniqueID` | (string) .File.PathのMD5ハッシュ |

## Menu Variables
- https://gohugo.io/variables/menus/#variables

| Variables | Description |
|---|---|
| `.Menu.Children` | (menu) 現在のメニューエントリの下にある、子メニューエントリのコレクション（もしあれば） |
| `.Menu.Identifier` | (string) メニューエントリの識別子プロパティ。メニューエントリを自動定義する場合、ページの .Section。 |
| `.Menu.KeyName` | (string) メニューエントリの識別子プロパティ。それ以外の場合は、名前プロパティ。 |
| `.Menu.Menu` | (string) メニューエントリを含むメニューの識別子。 |
| `.Menu.Name` | (string) メニューエントリの名前プロパティ。メニューエントリを自動定義する場合、ページの .LinkTitle。それ以外の場合は、ページの .Title。 |
| `.Menu.Page` | (page) メニューエントリに関連するページへの参照。 |
| `.Menu.Params` | (map) メニューエントリのparamsプロパティ。 |
| `.Menu.Parent` | (string) メニューエントリの親プロパティ。 |
| `.Menu.Post` | (template.HTML) メニューエントリのpostプロパティ。 |
| `.Menu.Pre` | (template.HTML) メニューエントリのpreプロパティ。 |
| `.Menu.Title` | (string) メニューエントリのタイトルプロパティ。メニューエントリを自動定義する場合、ページの .LinkTitle。それ以外の場合は、ページの .Title。 |
| `.Menu.URL` | (string) メニューエントリに関連するページの .RelPermalink。外部リソースを指すメニューエントリの場合、メニューエントリのurlプロパティ。 |
| `.Menu.Weight` | (int) メニューエントリのweightプロパティ。メニューエントリを自動定義する場合、ページの .Weight。それ以外の場合は、ページの .Weight。 |

## Menu Methods
- https://gohugo.io/variables/menus/#methods

| Variables | Description |
|---|---|
| `.Menu.HasChildren` | (bool) .Childrenがnilでない場合、trueを返す。 |
| `.Menu.IsEqual` | (bool) メニューエントリが同じメニューエントリを表す場合、trueを返す。 |
| `.Menu.IsSameResource` | (bool) メニューエントリが同じリソースを指す場合、trueを返す。 |
| `.Menu.Page.HasMenuCurrent` | (bool) アクティブなメニューエントリの先祖を判断する。 |
| `.Menu.Page.IsMenuCurrent` | (bool) アクティブなメニューエントリを判断する。 |

## Git Info Variables
- https://gohugo.io/variables/git/

| Variables | Description |
|---|---|
| `.GitInfo.AbbreviatedHash` | 短縮されたコミットハッシュ（例：866cbcc） |
| `.GitInfo.AuthorName` | .mailmapに従った著者の名前 |
| `.GitInfo.AuthorEmail` | .mailmapに従った著者のメールアドレス |
| `.GitInfo.AuthorDate` | 著者の日付 |
| `.GitInfo.Hash` | コミットハッシュ（例：866cbccdab588b9908887ffd3b4f2667e94090c3） |
| `.GitInfo.Subject` | コミットメッセージの件名（例：tpl: Add custom index function） |
| `.GitInfo.Lastmod` | .GitInfo機能が有効な場合、.Lastmod（ページ上）はGitから取得される（.GitInfo.AuthorDate）。この動作は、日付のフロントマター設定を追加することで変更可能。|

## Git Info Variables
- https://gohugo.io/variables/git/

| Variables | Description |
|---|---|
| `.Sitemap.ChangeFreq` | ページの変更頻度 |
| `.Sitemap.Priority` | ページの優先度 |
| `.Sitemap.Filename` | サイトマップのファイル名 |
