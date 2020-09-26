---
title: "コマンドプロンプトの背景画像を設定したい！"
emoji: "😳"
type: "tech"
topics: ["WindowsTerminal"]
published: true
---

# はじめに
この記事は、Windows 10でコマンドプロンプトの背景画像を設定して、楽しくコマンドを打ってみたいと思っている方向けです。



# Windows Terminalをインストール・起動

背景画像を設定するとしても、cmdのままですと変更が出来ません。そこで！Windows Terminalをインストールします。

## インストール
 [こちら](https://www.microsoft.com/ja-jp/p/windows-terminal/9n0dx20hk701?activetab=pivot:overviewtab)より、Windows Terminalをインストールします。
 Microsoft Storeが開くので、インストールしてください。

## 起動
![windowster](https://storage.googleapis.com/zenn-user-upload/x825zzif7oemuepatprhl5b1f8iv)
Windows Terminalでは、PCにインストールされている様々なコマンドプロンプトを一つにまとめて使うことができます。

# 背景画像の設定

## 設定を開く

Windows Terminalでは、jsonファイルを書き換えることで設定を変更できます。
`Ctrl`+`;`+`,`を押す、又は、上部の下向きの折れ線を押した後、出てくる設定を押すと、設定が書かれたjsonファイルが開きます。
![settings](https://storage.googleapis.com/zenn-user-upload/gv8xp42vt3catgihgwly4b59tun1)



## jsonファイルの変更
### 画像の保存場所
jsonファイルを変更する前に、背景に設定する画像を保存します。
画像の保存場所は`C:\Users\ユーザー名\AppData\Local\Packages\Microsoft.WindowsTerminal_〇〇\LocalState`です。
:::message
もし、ファイルが表示されない場合は、エクスプローラーの表示から隠しファイルのチェックボックスにチェックを入れてください。
:::
そして、保存した画像のパスをしっかりコピーしてください。


### setting.jsonの書き方
今回は、cmdの背景を変更してみます。
![settings.json](https://storage.googleapis.com/zenn-user-upload/y8wcjey7c2oyceablut3wech029a)
setting.jsonを開くと、下の方に`list`とあります。
`list`の中身は
|名前|効果|
|---|---|
|guid|中身の文字が、上の`defaultProfile`と同じなら、最初に開く|
|name|名前|
|hidden|`true`の場合表示されなくなり、`false`の場合表示される|
|source または commandline|ソースです（）|
となっています。

そこに
```json
"backgroundImage":"C:\\Users\\ユーザー名\\AppData\\Local\\Packages\\MicrosoftWindowsTerminal_〇〇\\LocalState\\画像名",
"backgroundImageOpacity": 0.2,
"backgroundImageStretchMode": "uniformToFill"
```
と追加してください。

追加したものは
|名前|効果|
|---|---|
|backgroundImage|ダブルクォーテーションの中に先ほど保存した画像のパスを入れると背景画像設定出来る|
|backgroundImageOpacity|0~1で、0になるほど黒なり、1になるほど明るくなる|

`backgroundImageStretchMode`はサイズに関する項目で、設定する通りが4つあり
|名前|効果|
|---|---|
|none|背景画像のサイズはそのまま|
|fill|背景画像のサイズはウインドウサイズに合わされる。縦横比は維持されない。|
|uniform|背景画像のサイズはウインドウサイズの小さい辺に合わされる。縦横比は維持される。余白は黒になる。|
|uniformToFill|背景画像のサイズはウィンドウサイズの大きい辺に合わされる。縦横比は維持される。|
画像をきれいに表示させたい。そして、余白をなくしたい場合は、`uniformToFill`が適切です。

追加したら、保存してください。

以上！！

# あとがき
もともと筆者がmacのターミナルで背景画像を設定していましたが、windows10に移り背景画像が変更できず奮闘したのを今回まとめてみました。お役に立てれば幸いです。
不備がありましたら、[こちら](https://twitter.com/_Emiya_Saber)までよろしくお願いします。

# リンク
[Windows ターミナル プロファイルの設定](https://docs.microsoft.com/ja-jp/windows/terminal/customize-settings/profile-settings#unique-identifier)