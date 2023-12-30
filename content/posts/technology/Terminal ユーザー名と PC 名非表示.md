---
title: "Terminal ユーザー名と PC 名非表示"

date: 2023-01-14T13:53:18+09:00

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
tags: ["MacBook", "Terminal", "初期設定"]

description: "「追いかけ続ける勇気さえあれば、夢は必ず叶います」"

weight:

cover:
    image: "posts/technology/Terminal ユーザー名と PC 名非表示/Terminal ユーザー名と PC 名非表示.png/Terminal ユーザー名と PC 名非表示.png.001.png"
    alt: ""
    caption: ""
    relative: false # when using page bundles set this to true
    hidden: false # only hide on current single page
# ＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝🔼編集必要🔼＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝
---

# シンプルなターミナル画面

Macbook に標準で付属している UNIX 端末エミュレータ「ターミナル」は便利で、エンジンニアにとって、多分一番よく見る画面です。

ターミナル自体のデザインはシンプルでとても素敵と思っていますが、ユーザー名とPC名が毎回表示されるのは不便と思っています。

画像のように、これはユーザー名とPC名が表示されている状態です。

![元の画面](https://peridot-wood-05b.notion.site/image/https%3A%2F%2Fprod-files-secure.s3.us-west-2.amazonaws.com%2F9eac8f3d-2b0a-48f1-890e-bf2567cf11ae%2F72b6fb77-8baa-42e5-86e9-e81a04e9d74d%2F%25E5%2585%2583%25E3%2581%25AE%25E7%2594%25BB%25E9%259D%25A2.png?table=block&id=925fe71d-920b-4627-b5b4-b169322d3718&spaceId=9eac8f3d-2b0a-48f1-890e-bf2567cf11ae&width=2000&userId=&cache=v2)

工夫して、ユーザー名と PC 名を非表示にしたら、シンプルになり見やすくなります。

![エンド](https://peridot-wood-05b.notion.site/image/https%3A%2F%2Fprod-files-secure.s3.us-west-2.amazonaws.com%2F9eac8f3d-2b0a-48f1-890e-bf2567cf11ae%2Ff6395597-d708-4e31-9ba6-253fd57a1f38%2F%25E3%2582%25A8%25E3%2583%25B3%25E3%2583%2588%25E3%2582%2599.png?table=block&id=9133235e-d9a7-4b5a-a4d8-8ecfb6675994&spaceId=9eac8f3d-2b0a-48f1-890e-bf2567cf11ae&width=2000&userId=&cache=v2)

## 設定方法

### 今の SHELL を確認

まずは下記コマンドを入力して、今使用している Shell を確認します。

```shell
echo $SHELL
```

![echo](https://peridot-wood-05b.notion.site/image/https%3A%2F%2Fprod-files-secure.s3.us-west-2.amazonaws.com%2F9eac8f3d-2b0a-48f1-890e-bf2567cf11ae%2F0b8d698f-cc4c-4fac-ad57-3916cb542512%2Fecho.png?table=block&id=2b993703-ea7e-428b-8188-b62d2f006922&spaceId=9eac8f3d-2b0a-48f1-890e-bf2567cf11ae&width=2000&userId=&cache=v2)

Ventura 13.1 を使っていますので、zsh の確認ができました。

### zsh ファイルを編集

zsh の設定ファイルをVimで開きます。中身を編集します。

```shell
vim /etc/zshrc
```

![Vimopen](https://peridot-wood-05b.notion.site/image/https%3A%2F%2Fprod-files-secure.s3.us-west-2.amazonaws.com%2F9eac8f3d-2b0a-48f1-890e-bf2567cf11ae%2Fd10a5b8c-7a1f-494e-acf6-5b0cd391e14e%2FVimopen.png?table=block&id=5be3d05c-013e-4fe0-907f-91426764d093&spaceId=9eac8f3d-2b0a-48f1-890e-bf2567cf11ae&width=2000&userId=&cache=v2)

実行したら下記の zshrc ファイルの中身が表示されます。

![zsh中身](https://peridot-wood-05b.notion.site/image/https%3A%2F%2Fprod-files-secure.s3.us-west-2.amazonaws.com%2F9eac8f3d-2b0a-48f1-890e-bf2567cf11ae%2F8148c188-a156-40a1-a62b-5c712cef26d7%2Fzsh%25E4%25B8%25AD%25E8%25BA%25AB.png?table=block&id=2fcb932a-cf0b-456f-80d6-84bdc8816c25&spaceId=9eac8f3d-2b0a-48f1-890e-bf2567cf11ae&width=2000&userId=&cache=v2)

下まで移動すると、`# Default prompt`と言う項目が出てきます。

ここの内容を編集したら、ターミナルで表示されるユーザー名と PC 名も適応して変更します。

まずは内容を説明します。

```shell
PS1 : 表示するスタイル
n   : ユーザー名
m   : PC名
```

ユーザー名とPC名を隠すには、ここの`nとm`を削除します。

「i」を押して挿入モードに入ります。

元の設定をコメントアウトして下記の一行を追加します。

```
PS1="%1~ %# "
```

![PS1](https://peridot-wood-05b.notion.site/image/https%3A%2F%2Fprod-files-secure.s3.us-west-2.amazonaws.com%2F9eac8f3d-2b0a-48f1-890e-bf2567cf11ae%2F3d6d3d9b-d625-4105-a82b-36805f1fca4d%2F%25E7%25B7%25A8%25E9%259B%2586.png?table=block&id=370151f2-2a70-437d-8c8b-a1b683326a53&spaceId=9eac8f3d-2b0a-48f1-890e-bf2567cf11ae&width=2000&userId=&cache=v2)

### 編集を保存

編集が出来たら、「esc」を押して挿入モードからノーマルモードへ切り替えます。
sudu 命令で変更を保存します。
一度パソコンのパスワードが要求されます。自分のパスワードを入力してください。

![SUDO](https://peridot-wood-05b.notion.site/image/https%3A%2F%2Fprod-files-secure.s3.us-west-2.amazonaws.com%2F9eac8f3d-2b0a-48f1-890e-bf2567cf11ae%2F51efebc9-6bcf-45c0-b3b5-597363a6ce84%2FSUDO.png?table=block&id=edcb5d6b-5957-4914-ad3c-06188317cbd2&spaceId=9eac8f3d-2b0a-48f1-890e-bf2567cf11ae&width=2000&userId=&cache=v2)

ターミナルを再起動して、ユーザー名とPC名がなくなります。

## 最後

ターミナルがすっきりになる事で気持ちいいだけではなく、色んな作業の効率向上にも繋がります。

この記事を参考して皆さんが楽しみにしていただければと思っています。