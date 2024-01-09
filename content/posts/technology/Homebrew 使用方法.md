---
title: "Homebrew 使用方法"

date: 2023-01-26T00:24:54+09:00

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
tags: ["MacBook", "Homebrew", "初期設定"]

description: "「追いかけ続ける勇気さえあれば、夢は必ず叶います」"

weight:

cover:
    image: "posts/technology/Homebrew 使用方法/Homebrew で MacOS のソフトウェアを管理する.001.png"
    alt: ""
    caption: ""
    relative: false # when using page bundles set this to true
    hidden: false # only hide on current single page
# ＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝🔼編集必要🔼＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝
---

# Homebrew Apple silicon M1 版

新しいMacbookを手に入れた事で、一番早めに導入したいのが`Homebrew`と言うパッケージマネジメントシステムです。HomebrewはMacOS上で最も流行ってるパッケージマネージャーとも言えるでしょう。Homebrewを使用する事で、ソフトウェアの管理や開発環境の構築がコマンド一行で済む事になります。

ダウンロードした物があっちこっちに散らばるより、やはり一つの何かで統一して管理した方がスッキリです。

![IMG_5231のコピー](https://peridot-wood-05b.notion.site/image/https%3A%2F%2Fprod-files-secure.s3.us-west-2.amazonaws.com%2F9eac8f3d-2b0a-48f1-890e-bf2567cf11ae%2F0e45a989-8a73-41b1-8afe-97257594787a%2FUntitled.png?table=block&id=9fbe24c9-15fa-4551-b929-7ca26e25eeb5&spaceId=9eac8f3d-2b0a-48f1-890e-bf2567cf11ae&width=2000&userId=&cache=v2)


## 導入方法

ターミナルを開き、下記コマンドをコピペしたらインストールができます。

Apple silicon Mac のインストール先は`/opt/homebrew/`です。

コマンドが無効の場合は[公式サイト](https://brew.sh/index_ja)から最新のインストール用コマンドを入手できます。

```
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
```

インストールは何回も中断しますが、中断時のスクリプトに従って操作します。主にパスワードの入力とパスの設定です。

パスワード入力要請 ↓

```zsh
==> Checking for `sudo` access (which may request your password)...
Password:
```

パス設定の要請  ↓

```zsh
==> Next steps:

- Run these three commands in your terminal to add Homebrew to your PATH:
  echo '# Set PATH, MANPATH, etc., for Homebrew.' >> /Users/admin/.zprofile
  echo 'eval "$(/opt/homebrew/bin/brew shellenv)"' >> /Users/admin/.zprofile
  eval "$(/opt/homebrew/bin/brew shellenv)"´
- Run brew help to get started
- Further documentation:
  https://docs.brew.sh
```

## コマンド

### 基本コマンド

使用する内、自然に覚えるほど使用頻度が高い基本コマンドです。

| コマンド               | 説明                             |
| ---------------------- | :------------------------------- |
| brew -v                | Homebrew バージュン情報          |
| brew update            | Homebrew 更新                    |
| brew doctor            | Homebrew 問題検査                |
| brew search package    | パッケージ探す                   |
| brew info package      | パッケージ確認                   |
| brew install package   | パッケージインストール           |
| brew uninstall package | パッケージアンインストール       |
| brew list              | 導入済みパッケージ一覧           |
| brew list package      | パッケージ位置＆サイズ情報を確認 |
| brew outdated          | 導入済みパッケージ更新確認       |
| brew upgrade package   | パッケージ更新                   |

### 上級コマンド

特定の場面に役にたつコマンドです。

| コマンド                     | 説明                           |
| ---------------------------- | ------------------------------ |
| brew deps --tree --install   | 全てパッケージと依存           |
| brew deps --tree cocoapods   | パッケージと依存               |
| brew rmtree package --force  | パッケージと依存削除           |
| brew --cache                 | ダウンロード先                 |
| brew cleanup --prune 0       | 古いパッケージ削除             |
| brew list --pinned           | ロック済みパッケージ一覧       |
| brew pin package             | パッケージバージュンロック     |
| brew unpin package           | パッケージバージュンロック解除 |
| brew install A B C D E F G H | A ~ H 一気導入                 |

## 拡張機能


新しいマウスを買って、マウスのドライブソフトウエアをインストールしようとしたら、Homebrewには見つからなかった。Homebrewにそのソフトウエアがないではなく、別のソフトウエア倉庫にあります。メモとしてその倉庫の導入過程を記録します。

![IMG_5231のコピー](https://peridot-wood-05b.notion.site/image/https%3A%2F%2Fprod-files-secure.s3.us-west-2.amazonaws.com%2F9eac8f3d-2b0a-48f1-890e-bf2567cf11ae%2Fd7a92dd9-597c-4699-b108-6315b9718c12%2FUntitled.jpeg?table=block&id=d1a2e480-d98c-4b8d-baca-5469869544c2&spaceId=9eac8f3d-2b0a-48f1-890e-bf2567cf11ae&width=2000&userId=&cache=v2)

```zsh
欲しいソフトウエア　：Logi Options+
目標 Homebrew 倉庫：homebrew-cask-drivers
```
コマンド`brew tap`を使って倉庫を導入する

```zsh
~ % brew tap homebrew/cask-drivers
Running `brew update --auto-update`...
==> Tapping homebrew/cask-drivers
Cloning into '/opt/homebrew/Library/Taps/homebrew/homebrew-cask-drivers'...
remote: Enumerating objects: 14931, done.
remote: Counting objects: 100% (4/4), done.
remote: Compressing objects: 100% (4/4), done.
remote: Total 14931 (delta 0), reused 0 (delta 0), pack-reused 14927
Receiving objects: 100% (14931/14931), 2.99 MiB | 3.78 MiB/s, done.
Resolving deltas: 100% (10396/10396), done.
Tapped 224 casks (255 files, 3.7MB).
~ % 
```

コマンド`brew install`を使ってソフトウエアをダウンロードする

```zsh
~ % brew info logi-options-plus   
==> logi-options-plus: 1.30.0.7349 (auto_updates)
https://www.logitech.com/en-us/software/logi-options-plus.html
Not installed
From: https://github.com/Homebrew/homebrew-cask-drivers/blob/HEAD/Casks/logi-options-plus.rb
==> Name
Logitech Options+
==> Description
Software for Logitech devices
==> Artifacts
logioptionsplus_installer.app (Installer)
==> Caveats
You must reboot for the installation of logi-options-plus to take effect.

~ % brew install logi-options-plus
==> Caveats
You must reboot for the installation of logi-options-plus to take effect.

==> Downloading https://download01.logi.com/web/ftp/pub/techsupport/optionsplus/
######################################################################## 100.0%
Warning: No checksum defined for cask 'logi-options-plus', skipping verification.
==> Installing Cask logi-options-plus
To complete the installation of Cask logi-options-plus, you must also
run the installer at:
  /opt/homebrew/Caskroom/logi-options-plus/1.30.0.7349/logioptionsplus_installer.app
🍺  logi-options-plus was successfully installed!
~ % 

```

`Finder`の隠しファイルを表示させる

```zsh
＃隠しファイル表示ショットカット
command + shift + .
```

ダウンロード先まで進む

```zsh
/opt/homebrew/Caskroom/logi-options-plus/1.30.0.7349/logioptionsplus_installer.app
```

ダブルクリックして`Logi Options+`をインストールし、完了です。
