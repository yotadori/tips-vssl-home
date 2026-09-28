# 足回りモーターを駆動させよう

三輪ロボットの各車輪はオムニ（全方位移動）ホイールとなっており，それぞれのモーターに回転数差を与えることで全方向に移動ができます。使用するモーターは連続回転サーボモーターで，回転方向とスピードを制御できます。全方向移動の他，ある位置での定置回転も可能です。

## 1. 一つのモーターを回してみる

まず，一つのモーターだけを回してみよう。rot1と書いてあるところをrot2やrot3に書き換えれば，違うモーターが回転します。

-   プログラム 6　モーターを回す

```cpp
void setup() {
    delay(1000);
    rot1.set_speed(0.5); // モーターを0.5の速さで時計回りに回す
    delay(2000);
    rot1.stop(); // モーターを止める
    delay(2000);
    rot1.set_speed(-0.5); // モーターを0.5の速さで反時計回りに回す
    delay(2000);
    rot1.stop();
}
```

## 2. ピン番号の設定

下記プログラムを実行し，①ロボット右前のモーター，②後ろのモーター，③左前のモーターという順番に回るよう，ピン番号の設定を確認・修正してみよう。

-   プログラム 7　モーターのピン番号確認用プログラム

```cpp
void setup() {
    delay(1000);
    speaker.beep(1);
    rot1.set_speed(0.5);
    delay(2000);
    rot1.stop();

    speaker.beep(2);
    rot2.set_speed(0.5);
    delay(2000);
    rot2.stop();

    speaker.beep(3);
    rot3.set_speed(0.5);
    delay(2000);
    rot3.stop();
    speaker.stop();
}
```

## 3. ロボットを走らせる

三つのホイールを適切な速度で同時に動かすことで，ロボットを任意の方向に移動，回転させることができる。下記プログラムを実行して確認しよう。

-   プログラム 8　ロボットを走らせるプログラム（一部）

```cpp
// 割り込み処理
void timer1Task() {
    robo.execute(cycle);
}

// 割り込み用タイマー
EspEasyTimer timer1(TIMER_GROUP_0, TIMER_0);

void setup() {
    robo.setup();
    timer1.begin(timer1Task, cycle);
}

void loop() {
    robo.set_target_vel(200, 0, 0); // ロボットを前方向に動かす
    delay(2000);
    robo.set_target_vel(0, 200, 0); // ロボットを左方向に動かす
    delay(2000);
    robo.set_target_vel(0, 0, 5); // ロボットを反時計回りに回転
    delay(2000);
    robo.set_target_vel(-150, -150, 0); // ロボットを右後ろに動かす
    delay(2000);
    robo.stop();
    delay(3000);
}
```

