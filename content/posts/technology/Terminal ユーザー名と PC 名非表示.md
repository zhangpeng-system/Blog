---
title: "Terminal ユーザー名と PC 名非表示"

date: 2023-12-30T13:53:18+09:00

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

## シンプルなターミナル画面

> Macbook に標準で付属している UNIX 端末エミュレータ「ターミナル」は便利で、エンジンニアにとって、多分一番よく見る画面です。ターミナル自体のデザインはシンプルでとても素敵と思っていますが、ユーザー名とPC名が毎回表示されるのは不便と思っています。

- ユーザー名とPC名が表示されている状態です。

![元の画面](./MacOS%20%E3%81%AE%20Terminal%20%E3%81%A6%E3%82%99%E3%83%A6%E3%83%BC%E3%82%B5%E3%82%99%E3%83%BC%E5%90%8D%E3%81%A8%20PC%20%E5%90%8D%E3%82%92%E9%9D%9E%E8%A1%A8%E7%A4%BA%E3%81%AB%E3%81%99%E3%82%8B/%E5%85%83%E3%81%AE%E7%94%BB%E9%9D%A2.png)

- ユーザー名と PC 名を隠して見やすくなりました。

![エンド](./MacOS%20%E3%81%AE%20Terminal%20%E3%81%A6%E3%82%99%E3%83%A6%E3%83%BC%E3%82%B5%E3%82%99%E3%83%BC%E5%90%8D%E3%81%A8%20PC%20%E5%90%8D%E3%82%92%E9%9D%9E%E8%A1%A8%E7%A4%BA%E3%81%AB%E3%81%99%E3%82%8B/%E3%82%A8%E3%83%B3%E3%83%88%E3%82%99.png)

## 設定方法

- まずは下記コマンドを入力して、今使用している Shell を確認します。筆者の Macbook は Ventura 13.1 を使っていますので、zsh です。

```shell
echo $SHELL
```

![echo](./MacOS%20%E3%81%AE%20Terminal%20%E3%81%A6%E3%82%99%E3%83%A6%E3%83%BC%E3%82%B5%E3%82%99%E3%83%BC%E5%90%8D%E3%81%A8%20PC%20%E5%90%8D%E3%82%92%E9%9D%9E%E8%A1%A8%E7%A4%BA%E3%81%AB%E3%81%99%E3%82%8B/echo.png)

- zsh の設定ファイルをVimで開きます。

```shell
vim /etc/zshrc
```

![Vimopen](./MacOS%20%E3%81%AE%20Terminal%20%E3%81%A6%E3%82%99%E3%83%A6%E3%83%BC%E3%82%B5%E3%82%99%E3%83%BC%E5%90%8D%E3%81%A8%20PC%20%E5%90%8D%E3%82%92%E9%9D%9E%E8%A1%A8%E7%A4%BA%E3%81%AB%E3%81%99%E3%82%8B/Vimopen.png)

- 実行したら下記の zshrc ファイルの中身が表示されます。![zsh中身](./MacOS%20%E3%81%AE%20Terminal%20%E3%81%A6%E3%82%99%E3%83%A6%E3%83%BC%E3%82%B5%E3%82%99%E3%83%BC%E5%90%8D%E3%81%A8%20PC%20%E5%90%8D%E3%82%92%E9%9D%9E%E8%A1%A8%E7%A4%BA%E3%81%AB%E3%81%99%E3%82%8B/zsh%E4%B8%AD%E8%BA%AB.png)

- 下まで移動すると、`# Default prompt`と言う項目が出てきます。



```shell
PS1 : 表示するスタイル
n   : ユーザー名
m   : PC名
```

- ユーザー名とPC名を隠すには、ここの`nとm`を削除します。「i」を押して挿入モードに入ります。元の設定をコメントアウトして下記の一行を追加します。

```
PS1="%1~ %# "
```

![PS1](./MacOS%20%E3%81%AE%20Terminal%20%E3%81%A6%E3%82%99%E3%83%A6%E3%83%BC%E3%82%B5%E3%82%99%E3%83%BC%E5%90%8D%E3%81%A8%20PC%20%E5%90%8D%E3%82%92%E9%9D%9E%E8%A1%A8%E7%A4%BA%E3%81%AB%E3%81%99%E3%82%8B/PS1.png)

> 設定ファイルは readonly ですので、一度警告が出ますが無視して編集を続きます。

![編集](./MacOS%20%E3%81%AE%20Terminal%20%E3%81%A6%E3%82%99%E3%83%A6%E3%83%BC%E3%82%B5%E3%82%99%E3%83%BC%E5%90%8D%E3%81%A8%20PC%20%E5%90%8D%E3%82%92%E9%9D%9E%E8%A1%A8%E7%A4%BA%E3%81%AB%E3%81%99%E3%82%8B/%E7%B7%A8%E9%9B%86.png)

- 「esc」を押して挿入モードからノーマルモードへ切り替えます。sudu 命令で変更を保存します。

> 一度パソコンのパスワードが要求されます。自分のパスワードを入力してください。

![SUDO](./MacOS%20%E3%81%AE%20Terminal%20%E3%81%A6%E3%82%99%E3%83%A6%E3%83%BC%E3%82%B5%E3%82%99%E3%83%BC%E5%90%8D%E3%81%A8%20PC%20%E5%90%8D%E3%82%92%E9%9D%9E%E8%A1%A8%E7%A4%BA%E3%81%AB%E3%81%99%E3%82%8B/SUDO.png)

- 緑色の警告を無視して、続いて下記コマンドを入力して強制的Vimを閉じます。こうやって上書きができました。

```shell
:q!
```

![q！](./MacOS%20%E3%81%AE%20Terminal%20%E3%81%A6%E3%82%99%E3%83%A6%E3%83%BC%E3%82%B5%E3%82%99%E3%83%BC%E5%90%8D%E3%81%A8%20PC%20%E5%90%8D%E3%82%92%E9%9D%9E%E8%A1%A8%E7%A4%BA%E3%81%AB%E3%81%99%E3%82%8B/q%EF%BC%81.png)

- ターミナルを再起動して、ユーザー名とPC名がなくなりました。

![エンド](./MacOS%20%E3%81%AE%20Terminal%20%E3%81%A6%E3%82%99%E3%83%A6%E3%83%BC%E3%82%B5%E3%82%99%E3%83%BC%E5%90%8D%E3%81%A8%20PC%20%E5%90%8D%E3%82%92%E9%9D%9E%E8%A1%A8%E7%A4%BA%E3%81%AB%E3%81%99%E3%82%8B/%E3%82%A8%E3%83%B3%E3%83%88%E3%82%99.png)

## 最後

ターミナルがすっきりになる事で気持ちいいだけではなく、色んな作業の効率向上にも繋がります。

この記事を参考して皆さんが楽しみにしていただければと思っています。