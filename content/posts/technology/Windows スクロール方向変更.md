---
title: "Windows スクロール方向変更"

date: 2023-02-11T12:18:51+09:00

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
tags: ["Windows", "Shell", "初期設定"]

description: "「追いかけ続ける勇気さえあれば、夢は必ず叶います」"

weight:

cover:
    image: "posts/technology/Windows スクロール方向変更/cover/cover.001.png"
    alt: ""
    caption: "Windows スクロール方向変更"
    relative: false # when using page bundles set this to true
    hidden: false # only hide on current single page
# ＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝🔼編集必要🔼＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝
---

# MacBook 自然方向 

MacBook の自然スクロール方向に慣れたら、何年間も使いし続けて来た Windows のスクロースに違和感を感じて、もし Windows のマウス方向が MacBook と同じようにできたらいいなぁと思って調べました。

## PowerShell

下記のコマンドをコピペして、`Enter`を押して何も表示されなかったら設定が完了です。

```
Get-ItemProperty HKLM:\SYSTEM\CurrentControlSet\Enum\HID\*\*\Device` Parameters FlipFlopWheel -EA 0 | ForEach-Object { Set-ItemProperty $_.PSPath FlipFlopWheel 1 }
```

## PC 再起動
Windows を再起動したら自動的適応されます。
これで、Windows 上でのスクロール方向が Mac のようになります。

この手順は Windows 10 用ですが、Windows 11 にも使えます。
設定によってはオプションの位置や名前が異なる場合があるので、適宜ご自身の Windows バージョンに合わせて調整してください。