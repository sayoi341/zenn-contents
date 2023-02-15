---
title: "EAGLEとKitMillで回路基板を作ろう"
emoji: "😺"
type: "tech" # tech: 技術記事 / idea: アイデア
topics: ["電子工作","基板","回路設計"]
published: false
---
## 前書き
茨城高専ロボット部の回路班向けの資料となっています。

## 目次

- ガーバーデータの生成
- ガーバーデータの変換
- CNCフライスで基盤を作る

##  ガーバーデータの生成

EAGLEを使用し、`RS-274X`形式のガーバーデータを生成します。

### 事前準備

#### ダウンロード

ガーバーデータを生成するために、CAMファイル

- `excellon.cam`
- `gerb274z[2L].cam`

をダウンロードします。

リンクは[ここ](https://github.com/sayoi341/camfiles)です。

#### EAGLE用に配置

windowsなら、`C:\Users\$USERNAME\Documents\EAGLE\cam`の中に

macなら、`/Users/$USERNAME/Documents/EAGLE/cam`の中に

（EAGLEのcamの中）に配置してください。


### ガーバーデータの生成

EAGLEを開き、brdファイルを開きます。

CAM Processor(工場のマーク)を開き、Load job file(ファイルのマーク)から、

- `Local CAM jobs` -> `cam` ->`excellon.cam` => `Process Job`
![](https://storage.googleapis.com/zenn-user-upload/b09dcfbdd9dd-20230215.png)

- `Local CAM jobs` -> `cam` ->`gerb274z[2L].cam` => `Process Job`
![](https://storage.googleapis.com/zenn-user-upload/325ed42bb9b3-20230215.png)
で、ガーバーデータが生成されます。

![](https://storage.googleapis.com/zenn-user-upload/0ea2bb2d64a5-20230215.png)
**successfully**って出たら勝ちです。

たくさんできますが、一覧表はこちら[^1]

| 説明               | 拡張子 |
| ------------------ | ------ |
| 部品面パターン     | .cmp   |
| 半田面パターン     | .sol   |
| 部品面レジスト     | .stc   |
| 半田面レジスト     | .sts   |
| 部品面シルク       | .plc   |
| 半田面シルク       | .pls   |
| プリント基盤外形   | .out   |
| ドリルデータ       | .drd   |
| ドリルリスト(inch) | .dri   |

今回は、cmp、out、drdファイルを使います。


## ガーバーデータの変換

orimin pcbを使用し、生成したガーバデータ`RS-274X`からNCプログラムを作成します。

設定いじると外形と穴を掘ってくれます。

## CNCフライスで基盤を作る

NCプログラムができたらもう基盤加工して終わりです。

### 準備するもの

- pc
- コントローラー（銀色の箱）
- CL200（基盤加工機）
- USBメモリ
- 基板加工カッター 土佐昌典VC（エンドミル）

https://www.originalmind.co.jp/goods/07960

### USBCNCで加工

1. 基盤加工機に接続されているコントローラー（銀色の箱）のボタンを押す
2. デスクトップにある`USB CNC V4`を右クリックして、管理者として起動

ここからは[公式サイト](https://www.originalmind.co.jp/special/technical/kitmill/)にも起動方法が載っています。

https://www.originalmind.co.jp/special/technical/kitmill/

3. F1または赤いところを押して、リセット

![](https://storage.googleapis.com/zenn-user-upload/b1e30715d61d-20230215.jpg)

4. F4または赤いところを押して、自動切削操作メニューにかえる
5. F2または赤いところを押して、NCコードを選択し読み込む。

![](https://storage.googleapis.com/zenn-user-upload/caf7166b18d6-20230215.jpg)

6. All filesに変更し、生成した`.ncd`ファイルを選択

![](https://storage.googleapis.com/zenn-user-upload/bf46040df19e-20230215.jpeg)
読み込まれた場合、画面に表示される

![](https://storage.googleapis.com/zenn-user-upload/6479854ee73b-20230215.jpeg)

7. 銅板に両面テープを付け台座に固定

8. エンドミルを固定

9. キーボードの矢印キーを使い、エンドミルの位置を移動させる

コントロールキーを押すと早く移動します。

10. 上のハンドルを回し、エンドミルの先端を調整する

![](https://storage.googleapis.com/zenn-user-upload/46339f141136-20230215.jpeg)
エンドミルの先端が銅板にピッタリになるようにおろす。

![](https://storage.googleapis.com/zenn-user-upload/dde4fe372d1f-20230215.jpeg)

11. 右上のWorkタブから、全方向の軸の原点を合わせる。

![](https://storage.googleapis.com/zenn-user-upload/a23946f466b7-20230215.jpg)
![](https://storage.googleapis.com/zenn-user-upload/c560731daeee-20230215.jpg)

12. F4または緑のボタンを押してスタート

![](https://storage.googleapis.com/zenn-user-upload/1865b5279941-20230215.jpg)
### 加工してる感じ

![](https://storage.googleapis.com/zenn-user-upload/74aa393094f0-20230215.jpeg)
## 参考リンク

https://mobius-el.cocolog-nifty.com/blog/2020/11/post-05dd49.html
