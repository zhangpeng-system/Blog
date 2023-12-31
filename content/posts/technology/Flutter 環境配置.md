---
title: "Flutter 環境配置"

date: 2023-02-01T17:01:07+09:00

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
tags: ["Android", "Flutter", "環境配置"]

description: "「追いかけ続ける勇気さえあれば、夢は必ず叶います」"

weight:

cover:
    image: "posts/technology/Fluuter 環境配置/cover/cover.001.png"
    alt: ""
    caption: ""
    relative: false # when using page bundles set this to true
    hidden: false # only hide on current single page
# ＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝🔼編集必要🔼＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝
---

# はじめに

Flutter 公式からも環境設定の説明を用意していますが、実際に着手してみると、初めてなので色々トラブルが発生しました。

本記事では 、私が踏んだ落穴を経験として、M1 Macbook をターゲットに導入中の注意点と導入順番を改善しました。
M1 Macbook であれば、公式より本記事の方が詳しくてわかりやすいと思っています。

また、Uinx like（macOS）で開発環境の設定やソフトウエアの管理を便利にできるのが `Homebrew`を使用するのが定番です。

本記事の環境設定も、面倒なパス設定をスッキプするために`Homebrew`を利用しています。

## STEP 1 : Rosetta 2

> Rosetta（ロゼッタ）とは ？
>
> Rosetta（ロゼッタ）は、特定のアーキテクチャのプログラムコードを持つバイナリを、別のアーキテクチャに適宜変換 (en:Dynamic recompilation) することでバイナリの互換性を維持する Apple の技術。

Apple Silicon Mac に Flutter を 導入する場合 Rosetta（ロゼッタ）が必要です。

ターミナルを開き、下記のコマンドで Rosetta 2 を導入します。

```zsh
sudo softwareupdate --install-rosetta --agree-to-licensea
```

sudo 命令を実行するには Mac のパスワードが要求されますが、入力して実行を続きます。

```zsh
~ % sudo softwareupdate --install-rosetta --agree-to-licensea
Password:
softwareupdate: unrecognized option `--agree-to-licensea'
usage: softwareupdate <cmd> [<args> ...]

** Manage Updates:
	-l | --list		List all appropriate update labels (options:  --no-scan, --product-types)
	-d | --download		Download Onlyƒ
	-i | --install		Instal
		<label> ...	specific updates
		-a | --all		All appropriate updates
		-R | --restart		Automatically restart (or shut down) if required to complete installation.
		-r | --recommended	Only recommended updates
		     --os-only	Only OS updates
		     --safari-only	Only Safari updates
		     --stdinpass	Password to authenticate as an owner. Apple Silicon only.
		     --user	Local username to authenticate as an owner. Apple Silicon only.
	--list-full-installers		List the available macOS Installers
	--fetch-full-installer		Install the latest recommended macOS Installer
		--full-installer-version	The version of macOS to install. Ex: --full-installer-version 10.15
	--install-rosetta	Install Rosetta 2
	--background		Trigger a background scan and update operation

** Other Tools:
	--dump-state		Log the internal state of the SU daemon to /var/log/install.log
	--evaluate-products	Evaluate a list of product keys specified by the --products option 
	--history		Show the install history.  By default, only displays updates installed by softwareupdate.  

** Options:
	--no-scan		Do not scan when listing or installing updates (use available updates previously scanned)
	--product-types <type>		Limit a scan to a particular product type only - ignoring all others
		Ex:  --product-types macOS  || --product-types macOS,Safari 
	--products		A comma-separated (no spaces) list of product keys to operate on. 
	--force			Force an operation to complete.  Use with --background to trigger a background scan regardless of "Automatically check" pref 
	--agree-to-license		Agree to the software license agreement without user interaction.

	--verbose		Enable verbose output
	--help			Print this help

~ % 
```

## STEP 2 : Xcode


> なぜ`Xcode`を導入しますか？
>
> 主に iOS シミュレーターを使用するため、いわば iOS 用の Flutter アプリを開発するためです。
> 後は Xcode コマンド ライン ツール を使用するためです。
> Xcode と Xcode コマンド ライン ツールの関係や利用方法についてはここで展開しません。

Apple Store を開き、`Xcode`と言うソフトウエアをインストールします。

![image-20230126225646874](https://peridot-wood-05b.notion.site/image/https%3A%2F%2Fprod-files-secure.s3.us-west-2.amazonaws.com%2F9eac8f3d-2b0a-48f1-890e-bf2567cf11ae%2F22708a18-5690-45a3-8e1e-e74191b1b6e0%2Fimage-20230126225646874.png?table=block&id=389afe54-7a39-4ad3-a9ae-af770f27c3a0&spaceId=9eac8f3d-2b0a-48f1-890e-bf2567cf11ae&width=2000&userId=&cache=v2)

ターミナルを開き、下記コマンドで Xcode コマンド ライン ツールを最新にします。

> sudo 命令はパスワードの入力が必要です。

```zsh
sudo xcode-select --switch /Applications/Xcode.app/Contents/Developer
```

- 最新バージュンへの自動化設定を下記コマンドで設定します。

```zsh
sudo xcodebuild -runFirstLaunch
```

## STEP ３ : Cocoapods

> Cocoapods とは
>
> CocoaPods は、Swift および Objective-C プロジェクトの依存関係マネージャーです。93,000 以上のライブラリがあり、300 万以上のアプリで使用されています。CocoaPods は、プロジェクトをエレガントにスケーリングするのに役立ちます。

macOS デスクトップ開発とプラグインの使用は Cocoapods が必要となります。

ターミナルを開き、下記のコマンドで Cocoapods を導入します。

```zsh
brew install cocoapods
```

すると、Cocoapods とその依存ソフトウエアもインストールしてくれます。

```zsh
~ % brew install cocoapods
Warning: Treating cocoapods as a formula. For the cask, use homebrew/cask/cocoapods
==> Fetching dependencies for cocoapods: libyaml, ca-certificates, openssl@1.1, readline and ruby
==> Fetching libyaml
==> Downloading https://ghcr.io/v2/homebrew/core/libyaml/manifests/0.2.5
Already downloaded: /Users/admin/Library/Caches/Homebrew/downloads/5f6b0af1730aa1bc02f8021c90ed7ffe988eeba95eec83e6c828f77332ba6406--libyaml-0.2.5.bottle_manifest.json
==> Downloading https://ghcr.io/v2/homebrew/core/libyaml/blobs/sha256:11239e8f50
Already downloaded: /Users/admin/Library/Caches/Homebrew/downloads/e0517d2d58c7c4228dbcf2255911eba0daed268ba29ef96b91cb8a391276afb7--libyaml--0.2.5.arm64_ventura.bottle.tar.gz
==> Fetching ca-certificates
==> Downloading https://ghcr.io/v2/homebrew/core/ca-certificates/manifests/2023-
Already downloaded: /Users/admin/Library/Caches/Homebrew/downloads/927414ed081d996b84d938be6af4d2639403b4d2bee3cc29268d0844999da180--ca-certificates-2023-01-10.bottle_manifest.json
==> Downloading https://ghcr.io/v2/homebrew/core/ca-certificates/blobs/sha256:11
Already downloaded: /Users/admin/Library/Caches/Homebrew/downloads/ca2448928ab98c455b5e46d4a6604247a151ab0f4e60553dbb5c6aecd2e1df3c--ca-certificates--2023-01-10.all.bottle.tar.gz
==> Fetching openssl@1.1
==> Downloading https://ghcr.io/v2/homebrew/core/openssl/1.1/manifests/1.1.1s
Already downloaded: /Users/admin/Library/Caches/Homebrew/downloads/0bd540a808ade4448d977fc4dc9711d8ea9a9b36a677e29a00f8ef821f7be88b--openssl@1.1-1.1.1s.bottle_manifest.json
==> Downloading https://ghcr.io/v2/homebrew/core/openssl/1.1/blobs/sha256:3a7812
Already downloaded: /Users/admin/Library/Caches/Homebrew/downloads/e8543caa6f3e3171f22c63c8c0d13b610724889a6afa8fd27fb93e52c29d6274--openssl@1.1--1.1.1s.arm64_ventura.bottle.tar.gz
==> Fetching readline
==> Downloading https://ghcr.io/v2/homebrew/core/readline/manifests/8.2.1
Already downloaded: /Users/admin/Library/Caches/Homebrew/downloads/ab483c9a913ae82f3a2b3ae20918791bc3bd6825c7122a29cd4f1e0c65413759--readline-8.2.1.bottle_manifest.json
==> Downloading https://ghcr.io/v2/homebrew/core/readline/blobs/sha256:fba42a9bd
Already downloaded: /Users/admin/Library/Caches/Homebrew/downloads/1d2d645220a91b8ac8869d09ddf0206070cd2f4278dddcfcc106eefb86be3c6c--readline--8.2.1.arm64_ventura.bottle.tar.gz
==> Fetching ruby
==> Downloading https://ghcr.io/v2/homebrew/core/ruby/manifests/3.2.0
Already downloaded: /Users/admin/Library/Caches/Homebrew/downloads/c360900acacef49e831b0f640b0e175180c181ef83afbcd24d4d6609fbf146fe--ruby-3.2.0.bottle_manifest.json
==> Downloading https://ghcr.io/v2/homebrew/core/ruby/blobs/sha256:a6e42d4316b36
Already downloaded: /Users/admin/Library/Caches/Homebrew/downloads/f8c7a256304b340959edf73bac57e21419bc36bbe0516866c954c7a027677ded--ruby--3.2.0.arm64_ventura.bottle.tar.gz
==> Fetching cocoapods
==> Downloading https://ghcr.io/v2/homebrew/core/cocoapods/manifests/1.11.3_1-1
Already downloaded: /Users/admin/Library/Caches/Homebrew/downloads/37d01c4861dfd4fb2ee665333db56c3652606c9c61ab9500929f9b29bfd1f467--cocoapods-1.11.3_1-1.bottle_manifest.json
==> Downloading https://ghcr.io/v2/homebrew/core/cocoapods/blobs/sha256:0a0e088c
Already downloaded: /Users/admin/Library/Caches/Homebrew/downloads/3a6ec835295692a730e0c900240d3b6c720b759591f2207c3ef4585e5a8469de--cocoapods--1.11.3_1.arm64_ventura.bottle.1.tar.gz
==> Installing dependencies for cocoapods: libyaml, ca-certificates, openssl@1.1, readline and ruby
==> Installing cocoapods dependency: libyaml
==> Pouring libyaml--0.2.5.arm64_ventura.bottle.tar.gz
🍺  /opt/homebrew/Cellar/libyaml/0.2.5: 10 files, 351.3KB
==> Installing cocoapods dependency: ca-certificates
==> Pouring ca-certificates--2023-01-10.all.bottle.tar.gz
==> Regenerating CA certificate bundle from keychain, this may take a while...
🍺  /opt/homebrew/Cellar/ca-certificates/2023-01-10: 3 files, 216.9KB
==> Installing cocoapods dependency: openssl@1.1
==> Pouring openssl@1.1--1.1.1s.arm64_ventura.bottle.tar.gz
🍺  /opt/homebrew/Cellar/openssl@1.1/1.1.1s: 8,101 files, 18MB
==> Installing cocoapods dependency: readline
==> Pouring readline--8.2.1.arm64_ventura.bottle.tar.gz
🍺  /opt/homebrew/Cellar/readline/8.2.1: 50 files, 1.7MB
==> Installing cocoapods dependency: ruby
==> Pouring ruby--3.2.0.arm64_ventura.bottle.tar.gz
🍺  /opt/homebrew/Cellar/ruby/3.2.0: 16,574 files, 46.8MB
==> Installing cocoapods
==> Pouring cocoapods--1.11.3_1.arm64_ventura.bottle.1.tar.gz
🍺  /opt/homebrew/Cellar/cocoapods/1.11.3_1: 13,476 files, 27.9MB
==> Running `brew cleanup cocoapods`...
Disable this behaviour by setting HOMEBREW_NO_INSTALL_CLEANUP.
Hide these hints with HOMEBREW_NO_ENV_HINTS (see `man brew`).
~ % 
```

こんな感じで、Cocoapods を利用するための必要なもの全てがインストールできた。

![image-20230126233605059](https://peridot-wood-05b.notion.site/image/https%3A%2F%2Fprod-files-secure.s3.us-west-2.amazonaws.com%2F9eac8f3d-2b0a-48f1-890e-bf2567cf11ae%2F815d189b-c186-41d4-b7fa-2a3df32a56cd%2Fimage-20230126233605059.png?table=block&id=ed6c1a2f-f6a9-46e6-ae74-1fb0b59ee821&spaceId=9eac8f3d-2b0a-48f1-890e-bf2567cf11ae&width=2000&userId=&cache=v2)

## STEP 4 : Flutter SDK

続いて、ターミナルを開き、下記のコマンドで Flutter SDK を導入します。

```
brew install flutter
```

この`🍺  flutter was successfully installed! `を確認出来たら、Flutter SDK のインストールが成功です。

```zsh
~ % brew install flutter
Running `brew update --auto-update`...
==> Auto-updated Homebrew!
Updated 2 taps (homebrew/core and homebrew/cask).

==> Downloading https://storage.googleapis.com/flutter_infra_release/releases/st
Already downloaded: /Users/admin/Library/Caches/Homebrew/downloads/18fd0ad2115d4c8b910546eee9d8df2c41d37b327355bd47dca81bbf52227d37--flutter_macos_arm64_3.3.10-stable.zip
==> Installing Cask flutter
==> Linking Binary 'dart' to '/opt/homebrew/bin/dart'
==> Linking Binary 'flutter' to '/opt/homebrew/bin/flutter'
🍺  flutter was successfully installed!
```

## STEP 5 : Java

Android 用の Flutter アプリを開発するためJavaが必要です。

ターミナルを開き、下記のコマンドで Open JDK、いわゆる Java を導入します。

```zsh
brew install openjdk
```

Open JDK をインストールしてくれます。

```zsh
~ % brew install openjdk
==> Fetching dependencies for openjdk: giflib, libpng, freetype, fontconfig, pcre2, gettext, glib, xorgproto, libxau, libxdmcp, libxcb, libx11, libxext, libxrender, lzo, pixman, cairo, graphite2, icu4c, harfbuzz, jpeg-turbo, lz4, xz, zstd, libtiff and little-cms2
==> Fetching giflib
==> Downloading https://ghcr.io/v2/homebrew/core/giflib/manifests/5.2.1
Already downloaded: /Users/admin/Library/Caches/Homebrew/downloads/51910e68b838a5c62c91c9352172d516e77a3c3c1a59a2cebaffc3f64f46adf4--giflib-5.2.1.bottle_manifest.json
==> Downloading https://ghcr.io/v2/homebrew/core/giflib/blobs/sha256:ced5a24b12f
Already downloaded: /Users/admin/Library/Caches/Homebrew/downloads/5b08b896fd26dcbaf618db0a80e50fcdb4378ad1e9b292ccbe82d468a4b86713--giflib--5.2.1.arm64_ventura.bottle.tar.gz
==> Fetching libpng
==> Downloading https://ghcr.io/v2/homebrew/core/libpng/manifests/1.6.39
Already downloaded: /Users/admin/Library/Caches/Homebrew/downloads/7d87285418cf2481c559b19433f1a0c0d5117b0b7b302f8829a798d8730a8556--libpng-1.6.39.bottle_manifest.json
==> Downloading https://ghcr.io/v2/homebrew/core/libpng/blobs/sha256:5fcb6945c7f
Already downloaded: /Users/admin/Library/Caches/Homebrew/downloads/e32f180ed45feb68fa9a81fcd47a14e455d898251281904dbc7233b2afc60d53--libpng--1.6.39.arm64_ventura.bottle.tar.gz
==> Fetching freetype
==> Downloading https://ghcr.io/v2/homebrew/core/freetype/manifests/2.12.1
Already downloaded: /Users/admin/Library/Caches/Homebrew/downloads/908428437764929aa268ec3967d2d4c58d2c0cdcb971555c98cd45ab6b7e3368--freetype-2.12.1.bottle_manifest.json
==> Downloading https://ghcr.io/v2/homebrew/core/freetype/blobs/sha256:f91e2b53f
Already downloaded: /Users/admin/Library/Caches/Homebrew/downloads/125fbddee3a1f447ed0dbd14f2841920882cf5902aa21d6dbd29469f38582e98--freetype--2.12.1.arm64_ventura.bottle.tar.gz
==> Fetching fontconfig
==> Downloading https://ghcr.io/v2/homebrew/core/fontconfig/manifests/2.14.1
Already downloaded: /Users/admin/Library/Caches/Homebrew/downloads/036ba3fd551c50827023705bb986c6b60c648ba36d68f4465eb9291a391e122a--fontconfig-2.14.1.bottle_manifest.json
==> Downloading https://ghcr.io/v2/homebrew/core/fontconfig/blobs/sha256:d0dc5e1
Already downloaded: /Users/admin/Library/Caches/Homebrew/downloads/7d7783ffb4d87127e3dcca9c6a3bbb5ef3c6795c485eb0fad73b61f1bf7416d4--fontconfig--2.14.1.arm64_ventura.bottle.tar.gz
==> Fetching pcre2
==> Downloading https://ghcr.io/v2/homebrew/core/pcre2/manifests/10.42
Already downloaded: /Users/admin/Library/Caches/Homebrew/downloads/6a53794fcaabc5cc5e05b19c02ca9c4c5f2cb9a4d65a5790a6841146465b040f--pcre2-10.42.bottle_manifest.json
==> Downloading https://ghcr.io/v2/homebrew/core/pcre2/blobs/sha256:8423a338c590
Already downloaded: /Users/admin/Library/Caches/Homebrew/downloads/20ad76b6ed64ec2235a96dfdd8b8b933d84eb616a5b9c2cd8b94768eabe220f5--pcre2--10.42.arm64_ventura.bottle.tar.gz
==> Fetching gettext
==> Downloading https://ghcr.io/v2/homebrew/core/gettext/manifests/0.21.1
Already downloaded: /Users/admin/Library/Caches/Homebrew/downloads/1c2f2c62faee672530e8e8e2695f99d26d1b606e74b289d1914dfa13c732c500--gettext-0.21.1.bottle_manifest.json
==> Downloading https://ghcr.io/v2/homebrew/core/gettext/blobs/sha256:28c5b06e66
Already downloaded: /Users/admin/Library/Caches/Homebrew/downloads/e802c20093535dc4a2cb11b0279b8c26f8c920746bd2fdcddcd50faf461f7c3f--gettext--0.21.1.arm64_ventura.bottle.tar.gz
==> Fetching glib
==> Downloading https://ghcr.io/v2/homebrew/core/glib/manifests/2.74.5
Already downloaded: /Users/admin/Library/Caches/Homebrew/downloads/35e2321bdf789440a78d6bb6ae383a7ca1e0c48997a5356d05c94a91d8f6a531--glib-2.74.5.bottle_manifest.json
==> Downloading https://ghcr.io/v2/homebrew/core/glib/blobs/sha256:dbc8e8fdf0da9
Already downloaded: /Users/admin/Library/Caches/Homebrew/downloads/0eb58575f9374924f2e6765590c5bb04fa63651bd3937cbfbbf8292cd8e987b9--glib--2.74.5.arm64_ventura.bottle.tar.gz
==> Fetching xorgproto
==> Downloading https://ghcr.io/v2/homebrew/core/xorgproto/manifests/2022.2
Already downloaded: /Users/admin/Library/Caches/Homebrew/downloads/9d0741febb29dfbb4f0e845adaa75d44fa0f9498bd1862f77d52561a8cb87300--xorgproto-2022.2.bottle_manifest.json
==> Downloading https://ghcr.io/v2/homebrew/core/xorgproto/blobs/sha256:d6deb2e4
Already downloaded: /Users/admin/Library/Caches/Homebrew/downloads/3d716cdc6955831613e02fb92d11ae81ba05df7ea0153f2e633a6b7834898dc2--xorgproto--2022.2.arm64_ventura.bottle.tar.gz
==> Fetching libxau
==> Downloading https://ghcr.io/v2/homebrew/core/libxau/manifests/1.0.11
Already downloaded: /Users/admin/Library/Caches/Homebrew/downloads/7faff26297b2e07682655beaa529cff7b3de0ad1abc013863ca3d03602b79ee7--libxau-1.0.11.bottle_manifest.json
==> Downloading https://ghcr.io/v2/homebrew/core/libxau/blobs/sha256:d8cc440c580
Already downloaded: /Users/admin/Library/Caches/Homebrew/downloads/a1f8411236b667139ee1ecc1a4802559f26ff128c1b693516ca2ac8f9d2a3413--libxau--1.0.11.arm64_ventura.bottle.tar.gz
==> Fetching libxdmcp
==> Downloading https://ghcr.io/v2/homebrew/core/libxdmcp/manifests/1.1.4
Already downloaded: /Users/admin/Library/Caches/Homebrew/downloads/1af80edced252b5f690f78a3805b785cbf689dc947cd5f45dced60c97640a9c9--libxdmcp-1.1.4.bottle_manifest.json
==> Downloading https://ghcr.io/v2/homebrew/core/libxdmcp/blobs/sha256:2fb2d55b8
Already downloaded: /Users/admin/Library/Caches/Homebrew/downloads/7167772f3e11cc89a6e578d955ee39fa57cfc0f160bb8812f56dac6fbde59246--libxdmcp--1.1.4.arm64_ventura.bottle.tar.gz
==> Fetching libxcb
==> Downloading https://ghcr.io/v2/homebrew/core/libxcb/manifests/1.15-2
Already downloaded: /Users/admin/Library/Caches/Homebrew/downloads/2a03b564f5bf826409537340998275531408c914e311e9eb031f9642f3bd0402--libxcb-1.15-2.bottle_manifest.json
==> Downloading https://ghcr.io/v2/homebrew/core/libxcb/blobs/sha256:2a2826a150a
Already downloaded: /Users/admin/Library/Caches/Homebrew/downloads/c1d866f28662d35b0395548e4002a442440dda8898c7ebc679d03488283acb7f--libxcb--1.15.arm64_ventura.bottle.2.tar.gz
==> Fetching libx11
==> Downloading https://ghcr.io/v2/homebrew/core/libx11/manifests/1.8.3
Already downloaded: /Users/admin/Library/Caches/Homebrew/downloads/67ef12ca0e3bcdbd6d11db4f5dfd9c80922ff1b81313073ff4a8650e5b65a2a6--libx11-1.8.3.bottle_manifest.json
==> Downloading https://ghcr.io/v2/homebrew/core/libx11/blobs/sha256:7371880b013
Already downloaded: /Users/admin/Library/Caches/Homebrew/downloads/6f681e9465ec7e452f4a94cccb4b07165fb951fc03e8deaaed26a1e5834bbde5--libx11--1.8.3.arm64_ventura.bottle.tar.gz
==> Fetching libxext
==> Downloading https://ghcr.io/v2/homebrew/core/libxext/manifests/1.3.5
Already downloaded: /Users/admin/Library/Caches/Homebrew/downloads/36b14aebd45b8fbf0f965d846bbc5126adbe882c0775c9936edb0432b347b9a1--libxext-1.3.5.bottle_manifest.json
==> Downloading https://ghcr.io/v2/homebrew/core/libxext/blobs/sha256:36ef533356
Already downloaded: /Users/admin/Library/Caches/Homebrew/downloads/f4c84f25a99b1eae8afd8436f9c47f3a4806aa9ecc36a7dbb9cdf5d32fe0d151--libxext--1.3.5.arm64_ventura.bottle.tar.gz
==> Fetching libxrender
==> Downloading https://ghcr.io/v2/homebrew/core/libxrender/manifests/0.9.11
Already downloaded: /Users/admin/Library/Caches/Homebrew/downloads/134c11be8346a1b116e04983c2da6366f29c4f4c2abc17604dcdb80d0475ae9d--libxrender-0.9.11.bottle_manifest.json
==> Downloading https://ghcr.io/v2/homebrew/core/libxrender/blobs/sha256:510d0cd
Already downloaded: /Users/admin/Library/Caches/Homebrew/downloads/cf4e6f27b41ee48304dfa7f1d20e9d72b3eac55c61bb7ab02360c9b46df078f1--libxrender--0.9.11.arm64_ventura.bottle.tar.gz
==> Fetching lzo
==> Downloading https://ghcr.io/v2/homebrew/core/lzo/manifests/2.10
Already downloaded: /Users/admin/Library/Caches/Homebrew/downloads/d4aa5b0c239912c53bc857d1012c6b7feb4acb509618f5e100f95bf8521f08e7--lzo-2.10.bottle_manifest.json
==> Downloading https://ghcr.io/v2/homebrew/core/lzo/blobs/sha256:a565c627b13f2d
Already downloaded: /Users/admin/Library/Caches/Homebrew/downloads/b859e0c335f31f15545d4cf698238a5ca6a91e4fccc88bda29d2763941acf9a6--lzo--2.10.arm64_ventura.bottle.tar.gz
==> Fetching pixman
==> Downloading https://ghcr.io/v2/homebrew/core/pixman/manifests/0.42.2
Already downloaded: /Users/admin/Library/Caches/Homebrew/downloads/602e44a110e6f967b5cfe6d79dd70688902fd411336d18ad05ef992a90aa7a4b--pixman-0.42.2.bottle_manifest.json
==> Downloading https://ghcr.io/v2/homebrew/core/pixman/blobs/sha256:f98b74948d7
Already downloaded: /Users/admin/Library/Caches/Homebrew/downloads/0d8ebf45d80d3bfbadd97677d94a9b798713c9fb7c025a8010c12d2de4777036--pixman--0.42.2.arm64_ventura.bottle.tar.gz
==> Fetching cairo
==> Downloading https://ghcr.io/v2/homebrew/core/cairo/manifests/1.16.0_5
Already downloaded: /Users/admin/Library/Caches/Homebrew/downloads/f9e86ee818c57a136b1c1c82caecdf07bb8eaad8e31f5e59e456a10d6d1a1cc5--cairo-1.16.0_5.bottle_manifest.json
==> Downloading https://ghcr.io/v2/homebrew/core/cairo/blobs/sha256:4a0f5f55a331
Already downloaded: /Users/admin/Library/Caches/Homebrew/downloads/d2b099dbaabd6975ebf10144287691e611ff445acfd25a95787f9aa5c238064b--cairo--1.16.0_5.arm64_ventura.bottle.tar.gz
==> Fetching graphite2
==> Downloading https://ghcr.io/v2/homebrew/core/graphite2/manifests/1.3.14
Already downloaded: /Users/admin/Library/Caches/Homebrew/downloads/bbb4dd2ef1846301d1eb08053e19e11ca9c780f93f4d3b2d638fd94a9bf54a0c--graphite2-1.3.14.bottle_manifest.json
==> Downloading https://ghcr.io/v2/homebrew/core/graphite2/blobs/sha256:3ec77041
Already downloaded: /Users/admin/Library/Caches/Homebrew/downloads/9f2bba1173f565d3d7ef1ab53da317f9a8b737a7f47f0a71d58c0ddec1e7f899--graphite2--1.3.14.arm64_ventura.bottle.tar.gz
==> Fetching icu4c
==> Downloading https://ghcr.io/v2/homebrew/core/icu4c/manifests/72.1
Already downloaded: /Users/admin/Library/Caches/Homebrew/downloads/adaa2fd48ef337b5bfee51ed8902dab61120bb41bd18f98eb20e744fdd5548c1--icu4c-72.1.bottle_manifest.json
==> Downloading https://ghcr.io/v2/homebrew/core/icu4c/blobs/sha256:0666e999875e
Already downloaded: /Users/admin/Library/Caches/Homebrew/downloads/b5387eff20f2e005df75fb220c2329237da248d0e23fcebd7f2227dad21d27e8--icu4c--72.1.arm64_ventura.bottle.tar.gz
==> Fetching harfbuzz
==> Downloading https://ghcr.io/v2/homebrew/core/harfbuzz/manifests/6.0.0_1
Already downloaded: /Users/admin/Library/Caches/Homebrew/downloads/23bde2902b8c68f92c86128d4e1b4e429bc7b3ed06d59da254a8f01ee3000c59--harfbuzz-6.0.0_1.bottle_manifest.json
==> Downloading https://ghcr.io/v2/homebrew/core/harfbuzz/blobs/sha256:469d30da7
Already downloaded: /Users/admin/Library/Caches/Homebrew/downloads/aadd90e6bd0224e5c488e089465e1e0ba2025eca6779eb2f9fc14465cb7870fa--harfbuzz--6.0.0_1.arm64_ventura.bottle.tar.gz
==> Fetching jpeg-turbo
==> Downloading https://ghcr.io/v2/homebrew/core/jpeg-turbo/manifests/2.1.4
Already downloaded: /Users/admin/Library/Caches/Homebrew/downloads/3f8a9083cce3533af8c64d8ddacc9dfa2efd55703d44b226b7c5214e7575a794--jpeg-turbo-2.1.4.bottle_manifest.json
==> Downloading https://ghcr.io/v2/homebrew/core/jpeg-turbo/blobs/sha256:692e1da
Already downloaded: /Users/admin/Library/Caches/Homebrew/downloads/5fa4b69320fbb62fd44bfb888fd918fe2a68789b6d5b7d8072c2488ede5b61bc--jpeg-turbo--2.1.4.arm64_ventura.bottle.tar.gz
==> Fetching lz4
==> Downloading https://ghcr.io/v2/homebrew/core/lz4/manifests/1.9.4
Already downloaded: /Users/admin/Library/Caches/Homebrew/downloads/379e59b981667f9585b33a2ff318769d8edca3ce6fd2e9a67ed291ae3e0cc872--lz4-1.9.4.bottle_manifest.json
==> Downloading https://ghcr.io/v2/homebrew/core/lz4/blobs/sha256:cd29e40287b0a2
Already downloaded: /Users/admin/Library/Caches/Homebrew/downloads/bdbca4231a01d687e54f87627b47f5209cd836fcba5f58353597bb599bea9cbe--lz4--1.9.4.arm64_ventura.bottle.tar.gz
==> Fetching xz
==> Downloading https://ghcr.io/v2/homebrew/core/xz/manifests/5.4.1
Already downloaded: /Users/admin/Library/Caches/Homebrew/downloads/50832bf13dbc3fee17aae88a9a1b882971b78b8ae6377608d664d7b3eb5f2314--xz-5.4.1.bottle_manifest.json
==> Downloading https://ghcr.io/v2/homebrew/core/xz/blobs/sha256:26ede511c3cc726
Already downloaded: /Users/admin/Library/Caches/Homebrew/downloads/39ec5af2e89811503c1164a2ebbf12601c2b4bad117d93dac404b9f05550824a--xz--5.4.1.arm64_ventura.bottle.tar.gz
==> Fetching zstd
==> Downloading https://ghcr.io/v2/homebrew/core/zstd/manifests/1.5.2-3
Already downloaded: /Users/admin/Library/Caches/Homebrew/downloads/f1226cb81ee54df46f1bb53da8118ca107a4f229ac63dc9405f2519c9f6fb45e--zstd-1.5.2-3.bottle_manifest.json
==> Downloading https://ghcr.io/v2/homebrew/core/zstd/blobs/sha256:92f953ed8a8c7
Already downloaded: /Users/admin/Library/Caches/Homebrew/downloads/893cae214d78e425489725f69f44aac6b1932784c93ccea84256a7df3bf75d49--zstd--1.5.2.arm64_ventura.bottle.3.tar.gz
==> Fetching libtiff
==> Downloading https://ghcr.io/v2/homebrew/core/libtiff/manifests/4.4.0_1-1
Already downloaded: /Users/admin/Library/Caches/Homebrew/downloads/045dd09de65fc836bebea86293526922ac74e8a456e721108460c2dc19495594--libtiff-4.4.0_1-1.bottle_manifest.json
==> Downloading https://ghcr.io/v2/homebrew/core/libtiff/blobs/sha256:4f8764b4cf
Already downloaded: /Users/admin/Library/Caches/Homebrew/downloads/928077e2d0153a000e1fa6ba0c25def27896e6bf8a8b00978a818f1623e4ec91--libtiff--4.4.0_1.arm64_ventura.bottle.1.tar.gz
==> Fetching little-cms2
==> Downloading https://ghcr.io/v2/homebrew/core/little-cms2/manifests/2.14
Already downloaded: /Users/admin/Library/Caches/Homebrew/downloads/80b5fe6f3594d3a3980e60bcef3a3479a20d05ec96378f3df8c6003ed86c50f3--little-cms2-2.14.bottle_manifest.json
==> Downloading https://ghcr.io/v2/homebrew/core/little-cms2/blobs/sha256:f65e00
Already downloaded: /Users/admin/Library/Caches/Homebrew/downloads/1e40d172a52d03f38e9032fed3faf2be3b1e3a615cd0eb793cea6bf444322db4--little-cms2--2.14.arm64_ventura.bottle.tar.gz
==> Fetching openjdk
==> Downloading https://ghcr.io/v2/homebrew/core/openjdk/manifests/19.0.1-1
Already downloaded: /Users/admin/Library/Caches/Homebrew/downloads/c7246ceb366faabcf9dd032058533f2e54a55b52e0baf1e45630280826b0f013--openjdk-19.0.1-1.bottle_manifest.json
==> Downloading https://ghcr.io/v2/homebrew/core/openjdk/blobs/sha256:f8f4e32243
Already downloaded: /Users/admin/Library/Caches/Homebrew/downloads/d30c3ae95667c7dca55fe53e44498b9cedb05fc647c30d70bef3a8aa42b4275a--openjdk--19.0.1.arm64_ventura.bottle.1.tar.gz
==> Installing dependencies for openjdk: giflib, libpng, freetype, fontconfig, pcre2, gettext, glib, xorgproto, libxau, libxdmcp, libxcb, libx11, libxext, libxrender, lzo, pixman, cairo, graphite2, icu4c, harfbuzz, jpeg-turbo, lz4, xz, zstd, libtiff and little-cms2
==> Installing openjdk dependency: giflib
==> Pouring giflib--5.2.1.arm64_ventura.bottle.tar.gz
🍺  /opt/homebrew/Cellar/giflib/5.2.1: 19 files, 540.2KB
==> Installing openjdk dependency: libpng
==> Pouring libpng--1.6.39.arm64_ventura.bottle.tar.gz
🍺  /opt/homebrew/Cellar/libpng/1.6.39: 27 files, 1.3MB
==> Installing openjdk dependency: freetype
==> Pouring freetype--2.12.1.arm64_ventura.bottle.tar.gz
🍺  /opt/homebrew/Cellar/freetype/2.12.1: 67 files, 2.3MB
==> Installing openjdk dependency: fontconfig
==> Pouring fontconfig--2.14.1.arm64_ventura.bottle.tar.gz
==> Regenerating font cache, this may take a while
==> /opt/homebrew/Cellar/fontconfig/2.14.1/bin/fc-cache -frv
🍺  /opt/homebrew/Cellar/fontconfig/2.14.1: 88 files, 2.4MB
==> Installing openjdk dependency: pcre2
==> Pouring pcre2--10.42.arm64_ventura.bottle.tar.gz
🍺  /opt/homebrew/Cellar/pcre2/10.42: 230 files, 6.2MB
==> Installing openjdk dependency: gettext
==> Pouring gettext--0.21.1.arm64_ventura.bottle.tar.gz
🍺  /opt/homebrew/Cellar/gettext/0.21.1: 1,983 files, 20.9MB
==> Installing openjdk dependency: glib
==> Pouring glib--2.74.5.arm64_ventura.bottle.tar.gz
🍺  /opt/homebrew/Cellar/glib/2.74.5: 449 files, 21.9MB
==> Installing openjdk dependency: xorgproto
==> Pouring xorgproto--2022.2.arm64_ventura.bottle.tar.gz
🍺  /opt/homebrew/Cellar/xorgproto/2022.2: 268 files, 3.9MB
==> Installing openjdk dependency: libxau
==> Pouring libxau--1.0.11.arm64_ventura.bottle.tar.gz
🍺  /opt/homebrew/Cellar/libxau/1.0.11: 21 files, 123.5KB
==> Installing openjdk dependency: libxdmcp
==> Pouring libxdmcp--1.1.4.arm64_ventura.bottle.tar.gz
🍺  /opt/homebrew/Cellar/libxdmcp/1.1.4: 11 files, 130.4KB
==> Installing openjdk dependency: libxcb
==> Pouring libxcb--1.15.arm64_ventura.bottle.2.tar.gz
🍺  /opt/homebrew/Cellar/libxcb/1.15: 2,461 files, 7.3MB
==> Installing openjdk dependency: libx11
==> Pouring libx11--1.8.3.arm64_ventura.bottle.tar.gz
🍺  /opt/homebrew/Cellar/libx11/1.8.3: 1,054 files, 7MB
==> Installing openjdk dependency: libxext
==> Pouring libxext--1.3.5.arm64_ventura.bottle.tar.gz
🍺  /opt/homebrew/Cellar/libxext/1.3.5: 87 files, 445.8KB
==> Installing openjdk dependency: libxrender
==> Pouring libxrender--0.9.11.arm64_ventura.bottle.tar.gz
🍺  /opt/homebrew/Cellar/libxrender/0.9.11: 12 files, 213.9KB
==> Installing openjdk dependency: lzo
==> Pouring lzo--2.10.arm64_ventura.bottle.tar.gz
🍺  /opt/homebrew/Cellar/lzo/2.10: 31 files, 566.3KB
==> Installing openjdk dependency: pixman
==> Pouring pixman--0.42.2.arm64_ventura.bottle.tar.gz
🍺  /opt/homebrew/Cellar/pixman/0.42.2: 11 files, 842.5KB
==> Installing openjdk dependency: cairo
==> Pouring cairo--1.16.0_5.arm64_ventura.bottle.tar.gz
🍺  /opt/homebrew/Cellar/cairo/1.16.0_5: 126 files, 6.4MB
==> Installing openjdk dependency: graphite2
==> Pouring graphite2--1.3.14.arm64_ventura.bottle.tar.gz
🍺  /opt/homebrew/Cellar/graphite2/1.3.14: 18 files, 281.2KB
==> Installing openjdk dependency: icu4c
==> Pouring icu4c--72.1.arm64_ventura.bottle.tar.gz
🍺  /opt/homebrew/Cellar/icu4c/72.1: 263 files, 78.4MB
==> Installing openjdk dependency: harfbuzz
==> Pouring harfbuzz--6.0.0_1.arm64_ventura.bottle.tar.gz
🍺  /opt/homebrew/Cellar/harfbuzz/6.0.0_1: 69 files, 8MB
==> Installing openjdk dependency: jpeg-turbo
==> Pouring jpeg-turbo--2.1.4.arm64_ventura.bottle.tar.gz
🍺  /opt/homebrew/Cellar/jpeg-turbo/2.1.4: 44 files, 2.5MB
==> Installing openjdk dependency: lz4
==> Pouring lz4--1.9.4.arm64_ventura.bottle.tar.gz
🍺  /opt/homebrew/Cellar/lz4/1.9.4: 22 files, 680.1KB
==> Installing openjdk dependency: xz
==> Pouring xz--5.4.1.arm64_ventura.bottle.tar.gz
🍺  /opt/homebrew/Cellar/xz/5.4.1: 95 files, 1.7MB
==> Installing openjdk dependency: zstd
==> Pouring zstd--1.5.2.arm64_ventura.bottle.3.tar.gz
🍺  /opt/homebrew/Cellar/zstd/1.5.2: 31 files, 2.2MB
==> Installing openjdk dependency: libtiff
==> Pouring libtiff--4.4.0_1.arm64_ventura.bottle.1.tar.gz
🍺  /opt/homebrew/Cellar/libtiff/4.4.0_1: 249 files, 4.8MB
==> Installing openjdk dependency: little-cms2
==> Pouring little-cms2--2.14.arm64_ventura.bottle.tar.gz
🍺  /opt/homebrew/Cellar/little-cms2/2.14: 21 files, 1.4MB
==> Installing openjdk
==> Pouring openjdk--19.0.1.arm64_ventura.bottle.1.tar.gz
==> Caveats
For the system Java wrappers to find this JDK, symlink it with
  sudo ln -sfn /opt/homebrew/opt/openjdk/libexec/openjdk.jdk /Library/Java/JavaVirtualMachines/openjdk.jdk

openjdk is keg-only, which means it was not symlinked into /opt/homebrew,
because macOS provides similar software and installing this software in
parallel can cause all kinds of trouble.

If you need to have openjdk first in your PATH, run:
  echo 'export PATH="/opt/homebrew/opt/openjdk/bin:$PATH"' >> ~/.zshrc

For compilers to find openjdk you may need to set:
  export CPPFLAGS="-I/opt/homebrew/opt/openjdk/include"

==> Summary
🍺  /opt/homebrew/Cellar/openjdk/19.0.1: 639 files, 320.0MB
==> Running `brew cleanup openjdk`...
Disable this behaviour by setting HOMEBREW_NO_INSTALL_CLEANUP.
Hide these hints with HOMEBREW_NO_ENV_HINTS (see `man brew`).
==> Caveats
==> openjdk
For the system Java wrappers to find this JDK, symlink it with
  sudo ln -sfn /opt/homebrew/opt/openjdk/libexec/openjdk.jdk /Library/Java/JavaVirtualMachines/openjdk.jdk

openjdk is keg-only, which means it was not symlinked into /opt/homebrew,
because macOS provides similar software and installing this software in
parallel can cause all kinds of trouble.

If you need to have openjdk first in your PATH, run:
  echo 'export PATH="/opt/homebrew/opt/openjdk/bin:$PATH"' >> ~/.zshrc

For compilers to find openjdk you may need to set:
  export CPPFLAGS="-I/opt/homebrew/opt/openjdk/include"

~ % sudo ln -sfn /opt/homebrew/opt/openjdk/libexec/openjdk.jdk /Library/Java/JavaVirtualMachines/openjdk.jdk
Password:
~ % echo 'export PATH="/opt/homebrew/opt/openjdk/bin:$PATH"' >> ~/.zshrc
~ % export CPPFLAGS="-I/opt/homebrew/opt/openjdk/include"
~ % 
```

Homebrew はいつも最新なバージョンをインストールしてくれます。
`java -version`コマンドを使ってバージュンを確認して安心します。

```zsh
~ % java -version
openjdk version "19.0.1" 2022-10-18
OpenJDK Runtime Environment Homebrew (build 19.0.1)
OpenJDK 64-Bit Server VM Homebrew (build 19.0.1, mixed mode, sharing)
~ % 
```

これで Java のインストールが完了です。

## STEP 6 : Android Studio

ターミナルを開き、下記のコマンドで Android Studio 導入します。

```zsh
brew install android-studio
```

インストール完了したら、`Android Studio`を開きます。

```zsh
==> Installing Cask android-studio
==> Moving App 'Android Studio.app' to '/Applications/Android Studio.app'
🍺  android-studio was successfully installed!
```

![スクリーンショット 2023-02-01 20.01.55](https://peridot-wood-05b.notion.site/image/https%3A%2F%2Fprod-files-secure.s3.us-west-2.amazonaws.com%2F9eac8f3d-2b0a-48f1-890e-bf2567cf11ae%2F565c913d-d908-4df5-919d-a6a30e528199%2F%25E3%2582%25B9%25E3%2582%25AF%25E3%2583%25AA%25E3%2583%25BC%25E3%2583%25B3%25E3%2582%25B7%25E3%2583%25A7%25E3%2583%2583%25E3%2583%2588_2023-02-01_20.01.55.png?table=block&id=eb24674d-5e6f-442d-8ab9-6ee24f2edcc3&spaceId=9eac8f3d-2b0a-48f1-890e-bf2567cf11ae&width=2000&userId=&cache=v2)

Plugin で Flutter（Dart）をダウンロードします。

![image-20230201200656211](https://peridot-wood-05b.notion.site/image/https%3A%2F%2Fprod-files-secure.s3.us-west-2.amazonaws.com%2F9eac8f3d-2b0a-48f1-890e-bf2567cf11ae%2Fc2789275-18a8-4a37-8615-a0260ad5ad84%2Fimage-20230201200656211.png?table=block&id=9d174d99-6093-405a-9df0-705e1fbb8631&spaceId=9eac8f3d-2b0a-48f1-890e-bf2567cf11ae&width=2000&userId=&cache=v2)

`All settings`を開きます。

![スクリーンショット 2023-02-01 20.08.28](https://peridot-wood-05b.notion.site/image/https%3A%2F%2Fprod-files-secure.s3.us-west-2.amazonaws.com%2F9eac8f3d-2b0a-48f1-890e-bf2567cf11ae%2F90e76ae3-40be-48b8-a6d9-25835cb9295a%2F%25E3%2582%25B9%25E3%2582%25AF%25E3%2583%25AA%25E3%2583%25BC%25E3%2583%25B3%25E3%2582%25B7%25E3%2583%25A7%25E3%2583%2583%25E3%2583%2588_2023-02-01_20.08.28.png?table=block&id=3a41e656-36fb-4b76-8faa-555e2d5fd3b9&spaceId=9eac8f3d-2b0a-48f1-890e-bf2567cf11ae&width=2000&userId=&cache=v2)

検索で`Android-SDK command line tools(latest)`をダウンロードします。

![image-20230201201735534](https://peridot-wood-05b.notion.site/image/https%3A%2F%2Fprod-files-secure.s3.us-west-2.amazonaws.com%2F9eac8f3d-2b0a-48f1-890e-bf2567cf11ae%2Fb6aec142-7b79-45ae-8065-cb282f5a46c2%2Fimage-20230201201735534.png?table=block&id=9db345d9-f7b4-4184-8efe-6ac2cd41c326&spaceId=9eac8f3d-2b0a-48f1-890e-bf2567cf11ae&width=2000&userId=&cache=v2)

もしエラー`✗ Unable to find bundled Java version.`が表示されたら、下記の手順を行います。

> メモ：原因不明（公式の方の問題 issue 未解決）で`Android studio`の名前が`jre`のフォルダが`jbr`になっています。これを修正します。	

1.アイコンを右クリックして、`パッケージの内容を表示`を選択します。

![image-20230201203628765](https://peridot-wood-05b.notion.site/image/https%3A%2F%2Fprod-files-secure.s3.us-west-2.amazonaws.com%2F9eac8f3d-2b0a-48f1-890e-bf2567cf11ae%2Fb634ea3b-0afc-4fb0-b547-e62cb5040948%2Fimage-20230201203628765.png?table=block&id=a0836fe0-0cfb-4c2b-af0f-6be716cc2bc7&spaceId=9eac8f3d-2b0a-48f1-890e-bf2567cf11ae&width=2000&userId=&cache=v2)

2.新規フォルダで名前を`jre`にします。

![image-20230201204013516](https://peridot-wood-05b.notion.site/image/https%3A%2F%2Fprod-files-secure.s3.us-west-2.amazonaws.com%2F9eac8f3d-2b0a-48f1-890e-bf2567cf11ae%2Fa34a573d-f923-40f2-9a01-41962b560601%2Fimage-20230201203852004.png?table=block&id=2f17a5da-2172-40eb-b76c-1ffc2633dadc&spaceId=9eac8f3d-2b0a-48f1-890e-bf2567cf11ae&width=2000&userId=&cache=v2)

3.`jbr`の中身を`jre`フォルダの中にコピペします。

![image-20230201204236264](https://peridot-wood-05b.notion.site/image/https%3A%2F%2Fprod-files-secure.s3.us-west-2.amazonaws.com%2F9eac8f3d-2b0a-48f1-890e-bf2567cf11ae%2F6ca28c17-b79b-457c-8d5a-25a1f6804314%2Fimage-20230201204236264.png?table=block&id=61a3e152-9b1f-44e3-acc8-dbe633389a17&spaceId=9eac8f3d-2b0a-48f1-890e-bf2567cf11ae&width=2000&userId=&cache=v2)

4.これでこの`✗ Unable to find bundled Java version.`のエラー修正が完了です。

続いて、ターミナルを開き、下記のコマンドで Android ライセンス規約をYes（同意）しながら導入します。

```shell
$ flutter doctor --android-licenses
```

## 完了　： Hello Worle !

環境配置が出来たら、早速 Flutter DEMO を一つ立ち上げましょう。

`New Flutter Project`を選択します。

![image-20230201204614005](https://peridot-wood-05b.notion.site/image/https%3A%2F%2Fprod-files-secure.s3.us-west-2.amazonaws.com%2F9eac8f3d-2b0a-48f1-890e-bf2567cf11ae%2F0c934adb-f2d3-4b52-bd05-eeb3b502d08f%2Fimage-20230201204614005.png?table=block&id=911d1768-a7d2-4ade-b968-82e682cc726a&spaceId=9eac8f3d-2b0a-48f1-890e-bf2567cf11ae&width=2000&userId=&cache=v2)

下記のパスに Homebrew でダウンロードした Flutter を見つけて選択します。

```
/opt/homebrew/Caskroom/flutter/3.3.10/flutter
```

![image-20230201210229402](https://peridot-wood-05b.notion.site/image/https%3A%2F%2Fprod-files-secure.s3.us-west-2.amazonaws.com%2F9eac8f3d-2b0a-48f1-890e-bf2567cf11ae%2Facd640a1-5dc8-4aa1-9273-f3e7da66d6fa%2Fimage-20230201210229402.png?table=block&id=35fb4dde-fa84-4ef9-9249-4deaffac2e27&spaceId=9eac8f3d-2b0a-48f1-890e-bf2567cf11ae&width=2000&userId=&cache=v2)

プロジェクトの名前を入力して、`Create`を選択します。

![image-20230201205832811](https://peridot-wood-05b.notion.site/image/https%3A%2F%2Fprod-files-secure.s3.us-west-2.amazonaws.com%2F9eac8f3d-2b0a-48f1-890e-bf2567cf11ae%2F99bf6897-0d6a-455d-b8cc-9f4b4aeb5785%2Fimage-20230201205832811.png?table=block&id=18272212-b1ff-4041-85ac-fd84f6030c0c&spaceId=9eac8f3d-2b0a-48f1-890e-bf2567cf11ae&width=2000&userId=&cache=v2)

これで Flutter のプロジェクトが作成できました。
これは公式のデフォルトな DEMO プロジェクトとなります。基本的は構造やソースコードを含んでいます。

![image-20230201205916568](https://peridot-wood-05b.notion.site/image/https%3A%2F%2Fprod-files-secure.s3.us-west-2.amazonaws.com%2F9eac8f3d-2b0a-48f1-890e-bf2567cf11ae%2F219e4f17-6102-40dd-88e6-2360f63a4193%2Fimage-20230201205916568.png?table=block&id=171dc484-af24-4eb5-a2b6-0fce0ab4ce37&spaceId=9eac8f3d-2b0a-48f1-890e-bf2567cf11ae&width=2000&userId=&cache=v2)

Chrome でプロジェクトを実行します。

![image-20230201210814903](https://peridot-wood-05b.notion.site/image/https%3A%2F%2Fprod-files-secure.s3.us-west-2.amazonaws.com%2F9eac8f3d-2b0a-48f1-890e-bf2567cf11ae%2Fa45f0531-b838-4bab-8e61-0ec3660a0528%2Fimage-20230201210814903.png?table=block&id=b87bf722-fe96-4bf8-8e38-d82f6210ada6&spaceId=9eac8f3d-2b0a-48f1-890e-bf2567cf11ae&width=2000&userId=&cache=v2)

## 終わりに

ほぼゼロから M1 Macbook の Flutter 導入方法を説明しました。ご参考になればうれしいと思います。