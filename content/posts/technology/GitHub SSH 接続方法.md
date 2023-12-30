---
title: "GitHub SSH 接続方法"

date: 2023-03-10T08:02:30+09:00

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
tags: ["RSA", "GitHub", "SSH"]

description: "「追いかけ続ける勇気さえあれば、夢は必ず叶います」"

weight:

cover:
    image: "posts/technology/GitHub SSH 接続方法/cover.001.png"
    alt: ""
    caption: ""
    relative: false # when using page bundles set this to true
    hidden: false # only hide on current single page
# ＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝🔼編集必要🔼＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝
---
# SSH を使用した GitHub への接続

### 2023年12月、追記

本記事で紹介したRSAキー（RSA暗号化鍵）方式で GitHub への接続方法は現在 GitHub より推奨しないようになっております。

その代わりに、DSAキー（DSA署名鍵）をお勧めします。

DSAキーは、デジタルメッセージの真正性と整合性を保証するために使用されるデジタル署名アルゴリズムです。
RSAキーと比較して、同等のセキュリティレベルを持つDSAキーは一般的に小さいです。そのため、署名や検証のプロセスがRSAよりも速くなることがあります。

また、DSAキーが使用不可の場合もあります。
RSAキーとDSAキーの選択はニーズに合わせて選びましょう！

## SSH有無の確認

まずはターミナルを開いて、下記のコマンドで既存のSSHがあるかどうかを確認します。

```shell
cd ~/.ssh
```

図の様に表示される場合は既存のSSHが 存在しない事です。

![image-20230310222201333](https://peridot-wood-05b.notion.site/image/https%3A%2F%2Fprod-files-secure.s3.us-west-2.amazonaws.com%2F9eac8f3d-2b0a-48f1-890e-bf2567cf11ae%2F899ed0fc-965a-4ad7-bf71-6029ca61af71%2Fimage-20230310222201333.png?table=block&id=984447ee-0479-45b1-a45d-a90864b14150&spaceId=9eac8f3d-2b0a-48f1-890e-bf2567cf11ae&width=2000&userId=&cache=v2)

## SSH作成

下記コマンドを入力して、`" "`の中は自分のメールアドレスを入力します。

```shell
ssh-keygen -t ed25519 -C "XXXXXXXX@gmail.com"
```

作成するSSHは`/Users/admin/.ssh`にあります。

![image-20230310222924172](https://peridot-wood-05b.notion.site/image/https%3A%2F%2Fprod-files-secure.s3.us-west-2.amazonaws.com%2F9eac8f3d-2b0a-48f1-890e-bf2567cf11ae%2Fb8ec6bb3-3c62-4b11-80bf-3707a3cae4ad%2Fimage-20230310222924172.png?table=block&id=82531608-8346-44e5-9bd6-261dc6b91969&spaceId=9eac8f3d-2b0a-48f1-890e-bf2567cf11ae&width=2000&userId=&cache=v2)

## 公開鍵・秘密鍵を利用してGitHubと繋がる

### 公開鍵と秘密鍵とは

分かりやすく例えにすれば、公開鍵はロック（錠）です。そして秘密鍵はそのロック（錠）を開ける鍵です。

## 公開鍵の設置

GitHub上の`Settings`ページを開き、左のサイドメニューから `SSH and GPG keys`をクリックします。

緑のボタン`New SSH key`をクリックします。

![image-20230311013310340](https://peridot-wood-05b.notion.site/image/https%3A%2F%2Fprod-files-secure.s3.us-west-2.amazonaws.com%2F9eac8f3d-2b0a-48f1-890e-bf2567cf11ae%2F2dad5198-5d6d-469f-8887-219fda8377a6%2Fimage-20230311013310340.png?table=block&id=e9796541-90fb-4905-a1ae-a662f4580946&spaceId=9eac8f3d-2b0a-48f1-890e-bf2567cf11ae&width=2000&userId=&cache=v2)

開いた画面に、公開鍵の`Title`と`Key`を設定します。

![image-20230311015039346](https://peridot-wood-05b.notion.site/image/https%3A%2F%2Fprod-files-secure.s3.us-west-2.amazonaws.com%2F9eac8f3d-2b0a-48f1-890e-bf2567cf11ae%2F0d192a92-50f6-462f-88dd-4995724b3f5e%2Fimage-20230311015039346.png?table=block&id=b8a8ea06-63a9-429e-8b7f-ae4d8b6364e0&spaceId=9eac8f3d-2b0a-48f1-890e-bf2567cf11ae&width=2000&userId=&cache=v2)

## id_rsa.pubのコピペ方法

まずはファイル`.ssh`に入ります。

```shell
cd ~/.ssh
```

`ls`コマンドで一度公開鍵・秘密鍵の存在を確認します。

```shell
ls
```

下記のように公開鍵・秘密鍵のファイルをの存在を確認できます。

![image-20230311020337694](https://peridot-wood-05b.notion.site/image/https%3A%2F%2Fprod-files-secure.s3.us-west-2.amazonaws.com%2F9eac8f3d-2b0a-48f1-890e-bf2567cf11ae%2F204abfb4-ef75-4378-b2e1-780d0c8e251b%2Fimage-20230311020337694.png?table=block&id=3793439f-f3cd-42c0-8d02-9dd037061c48&spaceId=9eac8f3d-2b0a-48f1-890e-bf2567cf11ae&width=2000&userId=&cache=v2)

コマンド`cat id_rsa.pub`また`vim id_rsa.pubで公開鍵の中身を確認できます。`

```shell
cat id_rsa.pub
```

![image-20230311020656278](https://peridot-wood-05b.notion.site/image/https%3A%2F%2Fprod-files-secure.s3.us-west-2.amazonaws.com%2F9eac8f3d-2b0a-48f1-890e-bf2567cf11ae%2F91b0379e-196c-4687-a8ac-21fa66d99cb3%2Fimage-20230311020656278.png?table=block&id=bf3baa74-530a-4586-8dd7-5d0179968e2a&spaceId=9eac8f3d-2b0a-48f1-890e-bf2567cf11ae&width=2000&userId=&cache=v2)

## 追加完了

コピペができたら、`Add SSH key`ボタンをクリックして、公開鍵、いわばSSH Keyの設定が終わります。

追加済みのSSH Keyは下記のように表示されます。

![](https://peridot-wood-05b.notion.site/image/https%3A%2F%2Fprod-files-secure.s3.us-west-2.amazonaws.com%2F9eac8f3d-2b0a-48f1-890e-bf2567cf11ae%2F18075993-79e7-45c4-8bf1-f51474d2ed9f%2Fimage-20230311021051667.png?table=block&id=f8bbb1a3-cc4f-4945-965f-0c83aadebb8a&spaceId=9eac8f3d-2b0a-48f1-890e-bf2567cf11ae&width=2000&userId=&cache=v2)

## 接続検証

下記コマンドを利用して接続の検証を行います。

```
ssh -T git@github.com
```

入力した後に、まずはエラーが表示されます。

心配せず`yes`を入力して続きます。

```
Are you sure you want to continue connecting (yes/no/[fingerprint])? yes
```

一度設定したパスワードを入力して、下記のような接続成功なメッセージを確認できます。

```
Enter passphrase for key '/Users/admin/.ssh/id_rsa': 
Hi zhangpeng-system! You've successfully authenticated, but GitHub does not provide shell access.
```

↑自分のユーザ名が含まれていることを確認できます。

この以降は`git clone SSH`を使ってGitHubへアクセスできるようになりました。