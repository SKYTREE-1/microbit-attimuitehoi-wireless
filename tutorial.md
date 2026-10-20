# あっちむいてほい（無線版）

## 1. ゲームの概要  @unplugged

micro:bitを使って「あっちむいてほい」をやってみよう。

![ゲームの概要](https://skytree-1.github.io/microbit-attimuitehoi-wireless/images/a001.png)

## 1. ゲームの概要（つづき）  @unplugged

### ゲームの流れ

1. じゃんけんをする
2. 勝った人が、4方向のうち1つを指す
3. 負けた人は、micro:bitを動かして顔を向ける方向を選ぶ
4. 指した方向と向いた方向が一致したら、指した人の勝ち

### 方向の考え方

「あっちむいてほい」では、**相手から見た方向** を考える。

| 指す人 | 相手（向かい合う）|
|---|---|
| ↑ | ↑ |
| → | ← |
| ↓ | ↓ |
| ← | → |

**ポイント：左右は逆、上下は同じ。**

このルールを使って、micro:bitのプログラムを作っていこう。



## 2. 指す人のプログラム @unplugged

指す人は、指す方向を数字に置き換えて、無線で送ります。

## 2-1. 方向を数字にする  @unplugged

| 方向 | 送る数字 |
|---|---:|
| ↑ | 0 |
| → | 1 |
| ↓ | 2 |
| ← | 3 |

まずは、**4つの方向だけ** を選んで送るプログラムを作ってみよう。



## プログラム 2-1-① 変数の作成

``||variables:変数を追加 ...||`` から、向きを表す変数 ``||variables: direction||`` をクリックして新しい変数を作成します。
また、``||basic:最初だけ||`` に ``||variables:変数 direction を 0にする||`` をいれて初期値を0に設定します。

```blocks
let direction = 0

```
## プログラム 2-1-② 方向を決める

``||input:ゆさぶられたとき||`` を追加して、、``||input:ゆさぶられた||``を``||input:ロゴが上になった||``にかえ、
そこに ``||variables:変数 direction を 0にする||`` と``||basic:矢印を表示（上向き↑）||`` をセットします。


```blocks
input.onGesture(Gesture.LogoUp, function () {
    direction = 0
    basic.showArrow(ArrowNames.North)
})

```

## プログラム 2-1-③ 方向を決める（つづき）

同じようにして ``||input:ゆさぶられたとき||`` を３つ追加して、、``||input:ゆさぶられた||``を``||input:右に傾けた||``,``||input:ロゴが下になった||``,``||input:左に傾けた||``にそれぞれにかえ、
それぞれに ``||variables:変数 direction を 0にする||`` と``||basic:矢印を表示（上向き↑）||`` をセットして、``||variables:変数の値||``を、右のとき **1**、 下のとき **2**、左のとき **3** にして、矢印をそれぞれの向きにかえます。


```blocks
input.onGesture(Gesture.TiltRight, function () {
    direction = 1
    basic.showArrow(ArrowNames.East)
})
input.onGesture(Gesture.LogoDown, function () {
    direction = 2
    basic.showArrow(ArrowNames.South)
})
input.onGesture(Gesture.TiltLeft, function () {
    direction = 3
    basic.showArrow(ArrowNames.West)
})


```

## ダウンロード

ここまでプログラムをしたら、ダウンロードして思った通りにうごくことを確認しましょう。

```blocks
let direction = 0
input.onGesture(Gesture.LogoUp, function () {
    direction = 0
    basic.showArrow(ArrowNames.North)
})
input.onGesture(Gesture.TiltRight, function () {
    direction = 1
    basic.showArrow(ArrowNames.East)
})
input.onGesture(Gesture.LogoDown, function () {
    direction = 2
    basic.showArrow(ArrowNames.South)
})
input.onGesture(Gesture.TiltLeft, function () {
    direction = 3
    basic.showArrow(ArrowNames.West)
})


```


## 2-2. 選んだ方向を無線で送る @unplugged

次に、選んだ方向の数字を、無線で送信するプログラムを作ります。
無線を使うので、はじめに無線グループを設定して、Aボタンを押したときに ``||variables:変数 direction ||`` に入っている数を送ることにします。

### ポイント：
グループの設定は、他の人と重ならないように決めてください。

## プログラム2-2-① 無線グループの設定
``||radio:無線||``グループから、``||radio:無線のグループを設定( )||`` を ``||basic:最初だけ||``にいれてグループの番号を設定します。

```blocks
direction = 0
radio.setGroup(100)

```

## プログラム2-2-② 数を送る
``||input:入力||``から``||input:Aボタンが押されたとき||`` を配置して、
``||radio:無線||``の``||radio:無線で数値を送信( )||`` をセットして、
数値の部分に ``||variables:変数||``にある ``||variables:direction||``をあてはめます。


```blocks
input.onButtonPressed(Button.A, function () {
    radio.sendNumber(direction)
})

```
## 2-3 指す人のプログラムのまとめ @unplugged

ここまでで、指す人が方向（数）を選んで、方向を表す数を相手に送るところまでプログラムができました。

受け取る方のプログラムを作っていないので、いまはテストできないので、このまま次へすすみましょう。

```blocks
input.onGesture(Gesture.TiltRight, function () {
    direction = 1
    basic.showArrow(ArrowNames.East)
})
input.onButtonPressed(Button.A, function () {
    radio.sendNumber(direction)
})
input.onGesture(Gesture.TiltLeft, function () {
    direction = 3
    basic.showArrow(ArrowNames.West)
})
input.onGesture(Gesture.LogoUp, function () {
    direction = 0
    basic.showArrow(ArrowNames.North)
})
input.onGesture(Gesture.LogoDown, function () {
    direction = 2
    basic.showArrow(ArrowNames.South)
})
let direction = 0
direction = 0
radio.setGroup(1)

```

## 3. 相手のプログラム @unplugged

次に相手のプログラムを考えていきます。
相手（向かい合う）は、「あっちむいてほい」のゲームでは、指す人が指を出すタイミングで、顔をうごかします（指す人の指した方向を見るとまけ）。

ここでは、micro:bitを動かすことで、顔を動かす動作を表しましょう。

そして、送られてきたむきと比較して判定をだしましょう。

まずは、**↑ について** だけ、一通りのながれをプログラムすることにします。

### 3-1. 方向を受信する

はじめに、無線で送られてきた数字を受け取って、表示するプログラムを作ります。

まず、指す人と相手の矢印の向きと、指す人が送った数字と矢印の関係を確認しましょう。

* **指す人と相手の矢印の向き**
| 指す人 | 相手（向かい合う）|
|---|---|
| ↑ | ↑ |
| → | ← |
| ↓ | ↓ |
| ← | → |

* **指す人が送った数字と矢印**
| 方向 | 送られてくる数字 |
|---|---:|
| ↑ | 0 |
| → | 1 |
| ↓ | 2 |
| ← | 3 |

ここから、受信した数と矢印の向きの関係は以下のようになります。

* **受信した数字と矢印**
| 方向 | 送られてくる数字 |
|---|---:|
| ↑ | 0 |
| ← | 1 |
| ↓ | 2 |
| → | 3 |


## プログラム 3-1①
``||radio:無線||`` にある ``||radio:無線で受信したとき（receivedNumber)||`` をだして配置します。

```blocks
radio.onReceivedNumber(function (receivedNumber) {
	
})
```

## プログラム 3-1②
この中に ``||logic:論理||`` にある ``||logic:もし〜ならでなければ||`` をセットして、左下の **+** を押して、分岐を４つにします。
```blocks
radio.onReceivedNumber(function (receivedNumber) {
    if (true) {
    	
    } else if (false) {
    	
    } else if (false) {
    	
    } else {
    	
    }
})
```

## プログラム 3-1③
この中に ``||logic:論理||`` にある ``||logic:（ ）＝（ ）||`` をセットして、左辺に ``||variables:receivedNumber||`` をあてはめ、右辺を **0** にします。
``||variables:receivedNumber||`` は、``||radio:無線で受信したとき||``ブロックにあるものをもってきて（ドラッグ&ドロップして）ください。
```blocks
radio.onReceivedNumber(function (receivedNumber) {
    if (receivedNumber == 0) {
    	
    } else if (false) {
    	
    } else if (false) {
    	
    } else {
    	
    }
})
```

## プログラム 3-1④
``||logic:（receivedNumber）＝（0）||`` の下に、``||basic:矢印を表示（上向き↑）||`` をセットします。

```blocks
radio.onReceivedNumber(function (receivedNumber) {
    if (receivedNumber == 0) {
    	basic.showArrow(ArrowNames.North)
    } else if (false) {
    	
    } else if (false) {
    	
    } else {
    	
    }
})
```
## プログラム 3-1⑤
同じようにして、**1**, **2**, **3（それ以外）** を受け取った場合にそれぞれ **←**, **↓**, **→** を表示するようにプログラムを追加してください。

```blocks
radio.onReceivedNumber(function (receivedNumber) {
    if (receivedNumber == 0) {
        basic.showArrow(ArrowNames.North)
    } else if (receivedNumber == 1) {
        basic.showArrow(ArrowNames.West)
    } else if (receivedNumber == 2) {
        basic.showArrow(ArrowNames.South)
    } else {
        basic.showArrow(ArrowNames.East)
    }
})
```

## ダウンロード
ここまでのプログラムを２台の micro:bit にダウンロードして、矢印を送り合ってみましょう。
ペア（またはグループで）同じ無線グループにして、お互いにおくりあうといいです。

```blocks
radio.onReceivedNumber(function (receivedNumber) {
    if (receivedNumber == 0) {
        basic.showArrow(ArrowNames.North)
    } else if (receivedNumber == 1) {
        basic.showArrow(ArrowNames.West)
    } else if (receivedNumber == 2) {
        basic.showArrow(ArrowNames.South)
    } else {
        basic.showArrow(ArrowNames.East)
    }
})
```

## 3-2. 相手のアクションと判定のプログラムをつくる @unplugged

相手のアクションとその結果の判定のプログラムをつくります。
まず「↑」を受信した場合を想定して作っていきましょう。

1. micro:bitを↑に傾ける
2. 正しく傾けられたか確認する
3. 正しければ「😊」、違っていれば「×」を表示する


## プログラム 3-2①

``||logic:もし〜ならでなければ||``ブロックを``||logic:receivedNumber = 0||`` ならの中に入れて、条件に ``||input:ゆさぶられた動き||``をあてはめ、``||input:ゆさぶられた||`` の部分を ``||input:ロゴが上になった||``にかえる。 

```blocks

radio.onReceivedNumber(function (receivedNumber) {
    if (receivedNumber == 0) {
        basic.showArrow(ArrowNames.North)
        if (input.isGesture(Gesture.LogoUp)) {
            
        } else {
           
        }
    } else if (receivedNumber == 1) {
        basic.showArrow(ArrowNames.West)
    } else if (receivedNumber == 2) {
        basic.showArrow(ArrowNames.South)
    } else {
        basic.showArrow(ArrowNames.East)
    }
})

```

## プログラム 3-2②

 ``||input:ロゴが上になった動き||``を検知した時に ``||basic:アイコン表示||``の``||basic:Happy||``、でなければ ``||basic:No||`` を表示します。 
```blocks

radio.onReceivedNumber(function (receivedNumber) {
    if (receivedNumber == 0) {
        basic.showArrow(ArrowNames.North)
        if (input.isGesture(Gesture.LogoUp)) {
            basic.showIcon(IconNames.Happy)
        } else {
            basic.showIcon(IconNames.No)
        }
    } else if (receivedNumber == 1) {
        basic.showArrow(ArrowNames.West)
    } else if (receivedNumber == 2) {
        basic.showArrow(ArrowNames.South)
    } else {
        basic.showArrow(ArrowNames.East)
    }
})

```

## ダウンロード 3-2

ここまでプログラムをしたら、ダウンロードして思った通りにうごくことを確認しましょう。

### 3-3. 残りの3方向を追加する @unplugged

**↑** の時のプログラムの動作確認ができたら、同じ考え方で、次の場合についてもプログラムしましょう。

- →
- ↓
- ←


ただし、「あっちむいてほい」では**左右が逆になる**ことに注意してください。

| 受信した方向 | micro:bitを動かす方向 |
|---|---|
| ↑ | ↑ |
| → | ← |
| ↓ | ↓ |
| ← | → |

## プログラム3-3
**↑** の時と同じように、**1**, **2**, **3** を受け取った場合についてもプログラムしましょう。
できたら、ダウンロードして思った通りにうごくことを確認しましょう。

```blocks
radio.onReceivedNumber(function (receivedNumber) {
    if (receivedNumber == 0) {
        basic.showArrow(ArrowNames.North)
        if (input.isGesture(Gesture.LogoUp)) {
            basic.showIcon(IconNames.Happy)
        } else {
            basic.showIcon(IconNames.No)
        }
    } else if (receivedNumber == 1) {
        basic.showArrow(ArrowNames.West)
        if (input.isGesture(Gesture.TiltLeft)) {
            basic.showIcon(IconNames.Happy)
        } else {
            basic.showIcon(IconNames.No)
        }
    } else if (receivedNumber == 2) {
        basic.showArrow(ArrowNames.South)
        if (input.isGesture(Gesture.LogoDown)) {
            basic.showIcon(IconNames.Happy)
        } else {
            basic.showIcon(IconNames.No)
        }
    } else {
        basic.showArrow(ArrowNames.East)
        if (input.isGesture(Gesture.TiltRight)) {
            basic.showIcon(IconNames.Happy)
        } else {
            basic.showIcon(IconNames.No)
        }
    }
})

```



## 4. あっちむいてほいをやってみよう @unplugged

2人でmicro:bitを使ってゲームをする。

1. じゃんけんをする
2. 勝った人が方向を選ぶ
3. 選んだ方向を無線で送る
4. 負けた人は、受け取った方向を考えてmicro:bitを動かす
5. 「😊」「×」で結果を確認する


## 5. まとめ @unplugged

micro:bitを使って、以下のようなプログラムを作成しました。

- 方向を数字に置き換える
- 無線で数字を送る
- 受け取った数字から方向を判断する
- 加速度センサーを使ってmicro:bitの傾きを判定する



次は、**micro:bitの動きをAIに覚えさせて、方向を判定してみよう。**
