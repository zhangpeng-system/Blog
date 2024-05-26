---
title: "Cortana 削除する方法"

date: 2023-01-18T00:58:56+09:00

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
tags: ["Windows 10", "Cortana", "PowerShell"]

description: "「追いかけ続ける勇気さえあれば、夢は必ず叶います」"

weight:

cover:
    image: "posts/technology/Cortana 削除する方法/Windows 10 の Cortana をアンインストールする（削除）方法.001.png.001.jpeg"
    alt: ""
    caption: ""
    relative: false # when using page bundles set this to true
    hidden: false # only hide on current single page
# ＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝🔼編集必要🔼＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝
---
# CortanaをPowerShellを使ってアンインストールする

CortanaをPowerShellを使ってアンインストールするは高度な操作であり、注意深く行う必要があります。誤ったコマンドの実行はシステムに損傷を与える可能性がありますので、慎重に手順を実行してください。

## Windows PowerShellを管理者権限で実行します。

スタートメニューで「PowerShell」と入力し、右クリックして「管理者として実行」を選択します。

![](https://peridot-wood-05b.notion.site/image/https%3A%2F%2Fprod-files-secure.s3.us-west-2.amazonaws.com%2F9eac8f3d-2b0a-48f1-890e-bf2567cf11ae%2F5662d3d3-a4a3-454d-b157-7bcb95fd6930%2FUntitled.png?table=block&id=97393e21-f516-4724-b028-8845ab13a281&spaceId=9eac8f3d-2b0a-48f1-890e-bf2567cf11ae&width=1380&userId=&cache=v2)

## 下記のコマンドをコピペして実行します。

```shell
Get-AppxPackage -allusers Microsoft.549981C3F5F10 | Remove-AppxPackage
```

このコマンドは、システムからCortanaをアンインストールします。このコマンドを実行すると、Cortanaが削除されます。

## 実行完了↓

![](https://peridot-wood-05b.notion.site/image/https%3A%2F%2Fprod-files-secure.s3.us-west-2.amazonaws.com%2F9eac8f3d-2b0a-48f1-890e-bf2567cf11ae%2F7b986988-2e22-4ed4-8cb7-bffc91ac0776%2FUntitled.png?table=block&id=27d930a1-7338-45df-b408-778a331555e4&spaceId=9eac8f3d-2b0a-48f1-890e-bf2567cf11ae&width=2000&userId=&cache=v2)

ctrl + C で Cortana を起動して見ると、何も出てきません、これで削除はできました。

これで、Cortanaはアンインストールされるはずですが、システムに影響を与える可能性があるため、慎重に操作してください。また、Cortanaをアンインストールすることで、検索機能やその他の関連する機能に影響を及ぼす場合があることにも注意してください。