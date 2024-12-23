# MsTimer2

## 概要
`MsTimer2`ライブラリは、Arduinoでミリ秒単位のタイマーを簡単に設定するためのライブラリです。このライブラリを使用することで、特定の時間間隔で関数を実行することができます。

## インクルード
まず、`MsTimer2`ライブラリを使用するために必要なヘッダファイルをインクルードします。

```cpp
#include <MsTimer2.h>
```

## タイマーの設定
次に、タイマーを設定します。`MsTimer2::set`関数を使用して、タイマーの間隔（ミリ秒単位）と実行する関数を指定します。

```cpp
void myFunction() {
  // 実行するコード
}

void setup() {
  MsTimer2::set(1000, myFunction); // 1秒ごとにmyFunctionを実行
}
```

## タイマーの開始と停止
設定が完了したら、タイマーを開始します。タイマーを開始するには`MsTimer2::start`関数を使用し、停止するには`MsTimer2::stop`関数を使用します。

```cpp
void setup() {
  MsTimer2::set(1000, myFunction); // 1秒ごとにmyFunctionを実行
  MsTimer2::start(); // タイマーを開始
}

void loop() {
  // メインのコード
}
```

## タイマーのリスタート
タイマーをリスタートするには、`MsTimer2::start`関数を再度呼び出します。

## 使用例
以下は、`MsTimer2`ライブラリを使用してLEDを1秒ごとに点滅させる例です。

```cpp
#include <MsTimer2.h>

const int ledPin = 13;

void toggleLED() {
  static bool ledState = LOW;
  ledState = !ledState;
  digitalWrite(ledPin, ledState);
}

void setup() {
  pinMode(ledPin, OUTPUT);
  MsTimer2::set(1000, toggleLED); // 1秒ごとにtoggleLEDを実行
  MsTimer2::start(); // タイマーを開始
}

void loop() {
  // メインのコード
}
```

## 課題

### 課題1: LEDの高速点滅
`MsTimer2`ライブラリを使用して、LEDを0.5秒ごとに点滅させるプログラムを書いてください。

### 課題2: ボタンを押さないと光るLED
`MsTimer2`ライブラリを使用して、ボタンが押されていない状態が5秒以上続いた場合に、LEDを点灯させるプログラムを書いてください。