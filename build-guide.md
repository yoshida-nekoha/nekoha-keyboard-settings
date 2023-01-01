# 30% 34 キー 禊(ミソギ) v2

![ロゴ](https://storage.googleapis.com/zenn-user-upload/959476bd5ba7-20221229.jpg)

30%キーボード、禊(みそぎ)のヘルプ用記事です。
ビルドの助けになれば。

## 特徴

仕事(文書作成、プログラミング、チャットツールなど)で毎日使えるキーボードとして設計しました。
BLE Micro Pro(以下 BMP)を使って無線化します(有線でよければ ProMicro で OK)。

- 30%オーソリニアで小型
- PCB サンドイッチ構造で軽量(260g)でもち運びにも便利
- 単４電池一本で無線動作(電池切れでもコンビニで買えます！)
  - 有線でも動作します
- 光りません

![キーボード](https://storage.googleapis.com/zenn-user-upload/800e315c3b8d-20221229.jpg)

## パーツリスト

基盤以外に下記パーツが必要になります。

### 必須パーツ

- `ProMicro互換機` or `BLE Micro Pro`
  - BLE Micro Pro(欠品率高め)
    - [遊舎工房](https://shop.yushakobo.jp/products/ble-micro-pro)
    - [booth](https://booth.pm/ja/items/1177319)
  - Pro Micro
    - [遊舎工房](https://shop.yushakobo.jp/products/pro-micro)
- 下記どちらかの組み合わせ
  - コントローラを抜き差ししたいなら
    - [シングルピンソケット （低メス） １ × １４ （１４Ｐ）](https://akizukidenshi.com/catalog/g/gC-00661/) x2 個
    - [ピンヘッダ　１ × ４０　（４０Ｐ）](https://akizukidenshi.com/catalog/g/gC-00167/) x1 個
      - ピンソケットにフィットにする 13 ピンなら何でも OK
      - 長い場合は折って 13 ピン x2 個にします
      - 細ピンヘッダだとゆるくて導通しない場合があるので注意
    - ~~[ロープロファイルピンヘッダ（低オス）　１ × ４０（４０Ｐ）　７．７ｍｍ](https://akizukidenshi.com/catalog/g/gC-02900/)~~
      - これは多分緩い
  - コントローラ固定で良いなら
    - なんでも良いのでピンヘッダ 13 ピン x2 個 あれば OK
- [スイッチソケット kailh x34 個](https://shop.yushakobo.jp/products/a01ps)
- [ダイオード SMD x34 個](https://shop.yushakobo.jp/products/a0800di-02-100)
  - リードの穴はありますが、スイッチに干渉するので使えません
- MX 互換キースイッチ x34 個 お好みで
- MX 互換キーキャップ お好みで
- [スペーサー M2x10mm x5 個](https://shop.yushakobo.jp/products/a0800c2?variant=37665435320481)
- [スペーサー M2x3mm x5 個](https://shop.yushakobo.jp/products/a0800c2?variant=37665435091105)
- ネジ M2x8mm x5 本
  - ホームセンターで買った
- [ネジ M2x4mm x5 本](https://shop.yushakobo.jp/products/a0800b2?variant=37665433288865)
  - 3mm でも OK

### BLE Micro Pro 用オプション

BLE Micro Pro(BMP)を単 4 電池で使いたい場合は下記が必要です。

- 横型スライドスイッチ
  - [スライドスイッチ　ＩＳＨ－１２６０－ＨＡ－Ｇ](https://akizukidenshi.com/catalog/g/gP-15370/)
- DCDC コンバータ
  - [ＸＣＬ１０３使用３．３Ｖ出力昇圧ＤＣＤＣコンバーターキット](https://akizukidenshi.com/catalog/g/gK-16116/)
  - 付属のピンヘッダを使います
- 単４電池ボックス
  - [電池ボックス 単４ × １本 ピン](https://akizukidenshi.com/catalog/g/gP-02670/)

## BLE Bicro Pro 用設定

[github](https://github.com/yoshida-nekoha/nekoha-keboard-settings/tree/main/misogi-bmp)にコンフィグファイルの設定を置いています。

(ProMicro 用は作ってないです)

## 組み立て

LED はないので、はんだ難易度は低めです。
初心者にもオススメ。

- ソケットとダイオードをはんだ付けする
- BMP を使う場合
  - DCDC コンバータをはんだ付けする
  - 電池ボックスをはんだ付けする
- コントローラの取り付け
  - 基盤の表側に取り付けます(ソケットやダイオードとは反対の面)
  - ピンソケットを使う場合ははんだ付け
    - 取り付けたらコントローラを乗せる前にマスキングテープで端子面を保護します
    - コントローラを載せ、マスキングテープを突き破ってピンヘッダを刺してください
    - コントローラとピンヘッダをはんだ付けしてください
    - コントローラからはみ出たピンは切ってください
  - コントローラを直接はんだ付けする場合
    - BMP ではない、通常の promicro の場合は外側端のピンを使いません
    - ピンヘッダを先に基盤にはんだ付けしてください
- BMP のファームウェアは[BLE-Micro-Pro-WebConfigurator](https://sekigon-gonnoc.github.io/BLE-Micro-Pro-WebConfigurator/)から最新化しておいてください。
  - bootloader は`0_11_0`
  - application version は`ble_micro_pro_default_0_11_3`
- 動くかな？
  - いくつかスイッチを刺すかショートさせてみて、動作確認してください
  - リセットスイッチは取り付けません、ピンセットなどでショートさせてください
  - リセットをよく使う場合はキーマップの中に入れておくと良いです(`KC_RESET`)
- メイン基板にスペーサーを取り付け
  - 左手前、コントローラの右上に 1 つだけボトムから通せないスペーサーがあります
  - ここだけ先に、上向きにスペーサーを取り付けます
- ボトムプレートの取り付け
  - 3mm スペーサーと 8mm ネジでメイン基板の下から締める
- スイッチプレートの取り付け
  - ボトムプレートから伸びているネジに 10mm スペーサーを取り付ける
  - スイッチプレートの右手前コーナーと電池ボックスから通す
  - 電池ボックスに余裕がなくてキツキツです(反省)
- スイッチの取付
  - MX 互換スイッチをはめていきます。
  - 4 つ角から入れていくとはめやすいかと思います
- トッププレートの取り付け
  - 4 つ角とメイン基板からでているロゴ右上のスペーサー 5 箇所を 4mm ネジで締めます
- キーキャップを取り付けて完成！

## 参考: キーマップについて

参考まで、以下の用途でレイヤー定義しています。  
(慣れは必要ですが)プログラミングする仕事でも普段使いで問題なく使えます。  
[github のキーマップ](https://github.com/yoshida-nekoha/nekoha-keboard-settings/blob/main/misogi-bmp/KEYMAP.JSN)

- レイヤー 0: 通常マップ
  - ハイフンがないので `I`と`O`のコンボキー(同時押し)
  - スペースキーは長押しで hhkb レイヤ
  - Enter, Backspace などはレイヤー 3
- レイヤー 1: テンキー用(試験的)
- レイヤー 2: 数字・記号用
- レイヤー 3: 移動・ショートカット・一部記号
  - Enter
  - vim 移動キー
  - win / mac でキー共通化のためコピペ用のショートカット
- レイヤー 4: Mac 用(試験的
  - なるべく win と同じ操作ができるように
- レイヤー 5: Fn キー、BMP 接続
  - Fn1(win でいうヘルプ)は使わないので未定義
  - スクリーンショット用
  - 仮想デスクトップ移動
  - マクロキー
- レイヤー 6: コンボキー定義

## お譲りします

あと１枚基盤が余っているので、送料込み 300 円でお譲りします。
(プロトタイプなのでほぼ送料のみの価格です)
メルカリ / pay pay / paypal のいずれかを選び、[twitter](https://twitter.com/yoshida_nekoha)で DM ください。
