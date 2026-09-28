# キック機構を駆動させよう

ロボットのキック機構にはサーボモーターを使用しています。このモーターは目標角度を指定して動作させることが可能です。キックバーを跳ね上げるように回転させることで，ボールをキックすることができます。

## 1. サーボモーターの角度を指定して動かす

-   プログラム 4　キック用のモーターを動かす

```cpp
void setup() {
    speaker.beep(1);
    delay(1000);
    speaker.stop();
    delay(1000);
    servo0.set_angle(-90); // サーボモーターを-90°の位置へ動かす
    delay(2000);
    servo0.set_angle(-45); // サーボモーターを-45°の位置へ動かす
    delay(2000);
    servo0.set_angle(0); // サーボモーターを0°の位置へ動かす
    delay(2000);
    servo0.set_angle(-90);
    delay(2000);
}
```

## 2. ピン番号の設定

キック用のモーター以外のモーターが回った場合は，プログラムの上部にあるピン番号の設定部分を修正します。D10,
D1, D2, D3を入れ替えて試してみてください。

-   プログラム 5　ピン番号の設定

```cpp
// ピン番号の設定
constexpr int SERVO_PIN = D10;
constexpr int ROT_PIN_1 = D1;
constexpr int ROT_PIN_2 = D2;
constexpr int ROT_PIN_3 = D3;
```

