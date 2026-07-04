---
title: "Hugoで作る、長く使い続けられる個人ブログ"

date: 2026-07-04T00:14:54+09:00

author: ["ZHANG PENG"]

hidemeta: false

draft: false

UseHugoToc: true

showToc: true

TocOpen: true

showbreadcrumbs: true

comments: true

canonicalURL: "https://zhangpeng-system.github.io/Blog/"

searchHidden: true

hideSummary: false

disableHLJS: false

disableShare: false

ShowReadingTime: true

ShowPostNavLinks: true

ShowWordCount: true

ShowRssButtonInSectionTermList: true
# ＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝🔽編集必要🔽＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝
tags: ["Hugo", "Blog", "GitHub Pages"]

description: "「追いかけ続ける勇気さえあれば、夢は必ず叶います」"

weight:

cover:
    image: "posts/technology/Hugoで作る、長く使い続けられる個人ブログ/Hugoで作る、長く使い続けられる個人ブログ.001.jpeg"
    alt: ""
    caption: ""
    relative: false # when using page bundles set this to true
    hidden: false # only hide on current single page
# ＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝🔼編集必要🔼＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝
---
# Hugoで作る、長く使い続けられる個人ブログ

## はじめに

このブログは、約3年前に Hugo を利用して構築しました。

当時は「とにかく公開すること」を目的に環境を構築していましたが、その後しばらく更新する機会がなく、今回あらためてブログ全体を見直すことにしました。

久しぶりに環境を構築し直してみると、Hugo 本体やテーマ、GitHub Actions などの周辺環境は大きく変化しており、以前の設定ではそのまま動作しない箇所もありました。

今回の見直しでは、単にバージョンを更新するだけではなく、ディレクトリ構成やテーマ管理、CI/CD の構成なども含めて整理し直しました。

この記事では、現在のブログ構成を紹介するとともに、長く運用していくために意識したポイントについてまとめます。

## Hugoとは

Hugo は Go 言語で開発された静的サイトジェネレーター（Static Site Generator）です。

Markdown で記事を書くと、HTML・CSS・JavaScript による静的サイトを高速に生成できます。

WordPress のような CMS と異なり、データベースやサーバーサイドプログラムを必要としないため、構成が非常にシンプルです。また、表示速度が速く、セキュリティ面でもメリットがあります。

個人ブログだけでなく、技術ドキュメントやポートフォリオサイト、プロジェクトのドキュメントサイトなどでも広く利用されています。

私が Hugo を選んだ理由は次のとおりです。

- Markdown だけで記事を書ける
- ビルド速度が非常に速い
- GitHub Pages と相性が良い
- Git によるバージョン管理がしやすい
- 豊富なテーマが利用できる
- GitHub Actions を利用した CI/CD を簡単に構築できる

一度環境を構築してしまえば、あとは記事を書いて GitHub に Push するだけでブログを更新できます。

「記事を書くこと」に集中できるシンプルな運用こそ、Hugo の大きな魅力だと感じています。

## Hugo Modulesとは

このブログでは、テーマとして **PaperMod** を利用しています。

現在は Git Submodule ではなく、**Hugo Modules** を利用してテーマを管理しています。

`hugo.yaml` では、次のようにテーマを読み込んでいます。

```yaml
module:
  imports:
    - path: github.com/adityatelange/hugo-PaperMod
```

以前は Git Submodule を利用する方法が一般的でした。

しかし Git Submodule は、リポジトリを Clone したあとに初期化が必要であり、新しい PC で環境を構築する際に初期化を忘れてしまうと、テーマが読み込めずビルドに失敗することがあります。

Hugo Modules を利用すると、テーマも Go Modules の依存関係として管理されます。

そのため、新しい環境でも必要なモジュールを自動的に取得でき、環境構築が非常にシンプルになります。

個人ブログのように長期間運用するプロジェクトでは、環境の再現性を高められる点も大きなメリットだと感じています。

## Hugoのディレクトリ構成

Hugo では、役割ごとにディレクトリが分かれています。

| ディレクトリ | 役割                                            |
| ------------ | ----------------------------------------------- |
| content/     | Markdown 記事を配置する                         |
| static/      | 画像やアイコンなどの静的ファイル                |
| layouts/     | テンプレートやカスタムレイアウト                |
| assets/      | CSS や画像などビルド対象となるリソース          |
| archetypes/  | 新規記事作成時のテンプレート                    |
| public/      | Hugo が生成する公開用ファイル（Git 管理対象外） |

普段の記事作成でよく利用するのは **content/** と **static/** の2つです。

このブログでは、記事をカテゴリごとに管理しやすいように、以下のような構成にしています。

```text
content/
└── posts/
    ├── technology/
    ├── aws/
    ├── cloud/
    └── life/
```

画像についても記事ごとに管理できるよう、`static/` 配下へ配置しています。

```text
static/
└── posts/
    ├── technology/
    ├── aws/
    └── life/
```

記事と画像を同じカテゴリ構成で管理しておくことで、あとから見返した際にも分かりやすくなります。

## 記事作成の流れ

### 新規記事を作成する

新しい記事は次のコマンドで作成します。

```bash
hugo new posts/technology/example.md
```

このコマンドを実行すると、`archetypes/default.md` をもとに Front Matter が自動生成されます。

記事を書くたびに毎回同じ設定を書く必要がないため、入力ミスを減らすことができます。

### Front Matter

このブログでは、以下のような Front Matter を利用しています。

```yaml
---
title: "記事タイトル"
date: 2026-07-04T00:00:00+09:00
author: ["ZHANG PENG"]

draft: false

showToc: true
TocOpen: true

ShowReadingTime: true
ShowWordCount: true

tags:
  - Hugo
  - Blog

cover:
  image: "default-cover/default-cover.png"
  hidden: false
---
```

Front Matter は記事のメタデータを管理するための設定です。

ここで設定した内容は、PaperMod 側でも利用され、タイトルやタグ、目次、読了時間、カバー画像などの表示に反映されます。

記事を書く際には本文よりも先に読み込まれるため、Front Matter の最後には必ず `---` を記述する必要があります。

この区切りを忘れてしまうと、本文まで設定ファイルとして解釈され、ビルドエラーになることがあります。

小さな記述ですが、初心者がつまずきやすいポイントの一つです。

### ローカルで確認する

記事を書いたあとは、まずローカル環境で表示を確認します。

```bash
hugo server
```

ブラウザから次の URL にアクセスすると、ローカル環境でブログを確認できます。

```text
http://localhost:1313/
```

下書き記事も確認したい場合は、`-D` オプションを指定します。

```bash
hugo server -D
```

`draft: true` に設定した記事も表示されるため、公開前の確認に便利です。

公開用の HTML を生成する場合は、次のコマンドを利用します。

```bash
hugo --gc --minify
```

それぞれのオプションには以下の役割があります。

- `--gc`：不要になったキャッシュや生成物を整理する
- `--minify`：HTML・CSS・JavaScript を圧縮して出力する

GitHub Pages 用にビルドする場合は、`baseURL` を指定しています。

```bash
hugo \
  --gc \
  --minify \
  --baseURL "https://zhangpeng-system.github.io/Blog/"
```

ローカル環境と公開環境で URL が異なる場合は、`baseURL` を適切に設定しておくことが重要です。

## ブログ機能設定

Hugo では、多くの機能を `hugo.yaml` から設定できます。

このブログで有効にしている主な設定を紹介します。

### CJK 言語対応

```yaml
hasCJKLanguage: true
```

日本語・中国語・韓国語などの CJK 文字を利用する場合は、この設定を有効にしておくことをおすすめします。

文字数や読了時間の計算がより自然になります。

---

### robots.txt の生成

```yaml
enableRobotsTXT: true
```

検索エンジン向けの `robots.txt` を自動生成します。

GitHub Pages で公開する場合でも、SEO を考えるなら有効にしておきたい設定です。

---

### Emoji 対応

```yaml
enableEmoji: true
```

Markdown 内で GitHub と同じように絵文字を利用できるようになります。

技術記事では使用頻度はそれほど高くありませんが、必要に応じて利用できるよう有効化しています。

### コードハイライト

技術ブログではコードブロックを掲載する機会が多いため、シンタックスハイライトも設定しています。

```yaml
markup:
  highlight:
    codeFences: true
    lineNos: true
    noClasses: false
    style: monokai
```

行番号を表示しておくことで、コードを説明する際にも位置を示しやすくなります。

また、テーマ全体で統一されたハイライトスタイルを利用することで、記事全体の読みやすさも向上します。

検索機能

このブログでは、PaperMod の検索機能を利用するために、ホームページの出力形式へ JSON を追加しています。

```yaml
outputs:
  home:
    - HTML
    - RSS
    - JSON
```

この設定により、検索用のインデックスファイルが自動生成され、ブラウザ上で記事を検索できるようになります。

検索対象は `fuseOpts` で細かく設定しています。

```yaml
fuseOpts:
  isCaseSensitive: false
  shouldSort: true
  threshold: 0.4
  keys:
    - title
    - permalink
    - summary
    - content
```

現在は以下の情報を検索対象にしています。

- 記事タイトル
- URL
- 記事概要
- 本文

記事数が増えてくると、過去に書いた内容を探す機会も多くなります。

検索機能を用意しておくことで、読者だけでなく、自分自身が技術メモを振り返る際にも役立っています。

## カバー画像の管理

記事のカバー画像は `static/` 配下で管理しています。

例えば、次のような画像を配置した場合、

```text
static/
└── default-cover/
    └── default-cover.png
```

Front Matter では以下のように指定できます。

```yaml
cover:
  image: "default-cover/default-cover.png"
```

`static/` は公開時にサイトのルートディレクトリとして扱われるため、Front Matter 側では `static/` を記述する必要はありません。

現在は記事ごとに個別のカバー画像を設定できるようにしつつ、画像を用意していない記事については共通のデフォルト画像を利用しています。

このようにしておくことで、記事一覧のデザインにも統一感を持たせることができます。


## GitHub Actionsによる自動デプロイ（CI/CD）

このブログでは GitHub Pages を利用して公開しています。

記事を更新したら GitHub の `main` ブランチへ Push するだけで、自動的にビルドとデプロイが実行されます。

CI/CD には GitHub Actions を利用しています。

ローカル環境でビルドした成果物を手動でアップロードする必要がないため、更新作業は非常にシンプルです。

Workflow では Hugo のバージョンを固定しています。

```yaml
env:
  HUGO_VERSION: 0.161.1
```

今回ブログを見直した際、以前は問題なく動いていた Workflow が正常に動作しなくなっていました。

原因を調べてみると、Hugo 本体やテーマ、GitHub Actions の仕様変更によって互換性が変化していたことが分かりました。

個人ブログは一度構築すると数年間放置してしまうことも少なくありません。

そのため、「今動いているから大丈夫」ではなく、「数年後でも再現できる環境」を意識して構成を管理することが重要だと改めて感じました。

現在は Hugo のバージョンを固定するとともに、テーマ管理も Hugo Modules に変更し、できるだけ長期間安定して運用できる構成を目指しています。

## よく使うHugoコマンド

普段よく利用しているコマンドをまとめます。

| コマンド                | 説明                          |
| ----------------------- | ----------------------------- |
| `hugo version`          | Hugo のバージョン確認         |
| `hugo server`           | ローカルサーバー起動          |
| `hugo server -D`        | 下書き記事も表示              |
| `hugo new posts/xxx.md` | 新規記事作成                  |
| `hugo --gc --minify`    | 本番用ビルド                  |
| `hugo mod tidy`         | Hugo Modules の依存関係を整理 |
| `hugo mod clean`        | Module キャッシュの削除       |

特によく利用するのは次の3つです。

- `hugo new`
- `hugo server`
- `hugo --gc --minify`

この3つだけでも、記事作成から公開までの一連の流れを十分に進めることができます。

---

## Hugoを使って感じたこと

Hugo は最初の環境構築こそ少し学習コストがありますが、一度構成を整えてしまえば、その後の運用は非常にシンプルです。

記事は Markdown で作成し、GitHub に Push するだけで公開できます。

CMS のように管理画面へログインしたり、データベースのバックアップを気にしたりする必要もありません。

今回あらためてブログを見直したことで、単に Hugo の使い方を学び直しただけではなく、長期間ソフトウェアを保守することの難しさも改めて実感しました。

3年前に構築した環境は、その当時は問題なく動作していました。

しかし時間の経過とともに、ライブラリやテーマ、GitHub Actions などの周辺技術は少しずつ更新され、以前の環境をそのまま再現することは簡単ではありませんでした。

今回の作業では AI も活用しながら過去のコードを読み直し、一つひとつ設定の意味を理解し直しました。

その結果、以前よりも Hugo の構成や GitHub Actions、Hugo Modules の仕組みについて深く理解できたと感じています。

ブログは記事を書くためのツールであると同時に、自分自身の学習記録でもあります。

定期的に環境を見直し、その時点で最適な構成へ改善していくことも、エンジニアとして大切な経験の一つだと思います。

## まとめ

このブログでは、Hugo、PaperMod、GitHub Pages、GitHub Actions を組み合わせて運用しています。

今回の見直しでは、ブログ全体の構成を整理し、長期間運用しやすい構成へ改善しました。

今回見直したポイントは次のとおりです。

- Hugo による高速な静的サイトの構築
- PaperMod を利用したシンプルなデザイン
- Hugo Modules によるテーマ管理
- Front Matter と Archetype を利用した記事作成の効率化
- GitHub Actions による CI/CD の自動化
- Hugo バージョンの固定による長期運用性の向上

個人ブログは、技術をアウトプットする場であるだけでなく、自分自身の知識や経験を積み重ねていく場所でもあります。

数年後にもう一度見返したとき、「なぜこのような構成にしたのか」を自分自身が理解できるようにしておくことも、保守性の高いブログを作る上で大切な考え方だと思います。

これからも Hugo をベースに環境を少しずつ改善しながら、新しく学んだ技術や日々の気付きを記録していきたいと思います。