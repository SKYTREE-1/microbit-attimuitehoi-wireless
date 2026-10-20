
> このページを開く [https://skytree-1.github.io/microbit-attimuitehoi-wireless/](https://skytree-1.github.io/microbit-attimuitehoi-wireless/)

[チュートリアル全体を表示](https://skytree-1.github.io/microbit-attimuitehoi-wireless/tutorial)

# あっちむいてほい（無線版）

microを使って、無線通信で「あっちむいてほい」をやってみよう！

2台のmicroを使い、じゃんけんで勝った人が選んだ方向を無線で相手に送り、負けた人は相手から見た方向を考えてmicroを動かします。

## このチュートリアルで学ぶこと

- micro:bit の傾きから4方向を選ぶ
- 方向を数字（0～3）に置き換える
- 無線通信で数字を送る
- 受信した数字から方向を判断する
- 加速度センサーを使ってmicro:bitの動きを判定する
  「左右は逆、上下は同じ」という「あっちむいてほい」のルールをプログラムにする

## ゲームの流れ

1. じゃんけんをする
2. 勝った人が方向を選ぶ
3. 選んだ方向を無線で送る
4. 負けた人は、受け取った方向を考えてmicroを動かす
5.「😊」「×」で結果を確認する

![ゲームの流れ]（images/a001.png）

## 使用するもの

- micro:bot × 2
- パソコン
- MakeCode for micro:bit

## チュートリアル

このプロジェクトでは、以下の順番でプログラムを作成します。

1. 指す方向を数字に置き換える
2. 選んだ方向を無線で送る
3. 受信した方向を表示する
4. 受信した方向に合わせてmicroを動かし、判定する
5. 4方向に対応させて、あっちむいてほいを完成させる

詳しい手順は `tutorial.md` を参照してください。


## 実行

* [チュートリアルを実行](https://makecode.microbit.org/#tutorial:github:SKYTREE-1/microbit-attimuitehoi-wireless/tutorial) 

#### メタデータ (検索、レンダリングに使用)

* for PXT/microbit
<script src="https://makecode.com/gh-pages-embed.js"></script><script>makeCodeRender("{{ site.makecode.home_url }}", "{{ site.github.owner_name }}/{{ site.github.repository_name }}");</script>
