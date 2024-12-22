# **Arduinoにおける基本的な入出力関数：`pinMode`、`digitalWrite`、`digitalRead`**

Arduinoを使ったプログラミングでは、デジタルピンを操作するために次の3つの関数が基本となります：

1. **`pinMode`**: ピンのモードを設定します（入力または出力）。
2. **`digitalWrite`**: ピンの状態を設定します（HIGHまたはLOW）。
3. **`digitalRead`**: ピンの状態を読み取ります（HIGHまたはLOW）。

---

## **1. `pinMode` 関数**
### **説明**
`pinMode` は、指定したピンを **入力** もしくは **出力** として設定するために使用します。

### **構文**
```cpp
pinMode(pin番号, モード);
```

### **引数**
- **`pin番号`**: 操作対象のデジタルピン番号 (例: 2, 13)。
- **`モード`**:
  - `INPUT`: 入力モード（例: ボタンやセンサーのデータを受け取る）。
  - `OUTPUT`: 出力モード（例: LEDやモーターを制御する）。
  - `INPUT_PULLUP`: 内蔵プルアップ抵抗を使用した入力モード。

### **例**
```cpp
void setup() {
  pinMode(13, OUTPUT); // ピン13を出力モードに設定
  pinMode(2, INPUT);   // ピン2を入力モードに設定
}
```

---

## **2. `digitalWrite` 関数**
### **説明**
`digitalWrite` は、指定したピンに **HIGH**（電圧を供給）または **LOW**（電圧を0にする）の状態を設定します。

### **構文**
```cpp
digitalWrite(pin番号, 状態);
```

### **引数**
- **`pin番号`**: 操作対象のデジタルピン番号。
- **`状態`**:
  - `HIGH`: ピンに5Vを出力。
  - `LOW`: ピンに0Vを出力。

### **例**
```cpp
void setup() {
  pinMode(13, OUTPUT);  // ピン13を出力モードに設定
}

void loop() {
  digitalWrite(13, HIGH); // ピン13をON
  delay(1000);            // 1秒待つ
  digitalWrite(13, LOW);  // ピン13をOFF
  delay(1000);            // 1秒待つ
}
```

---

## **3. `digitalRead` 関数**
### **説明**
`digitalRead` は、指定したデジタルピンの現在の状態（HIGHまたはLOW）を読み取ります。

### **構文**
```cpp
int 状態 = digitalRead(pin番号);
```

### **戻り値**
- **`HIGH`**: ピンがHIGH状態の場合。
- **`LOW`**: ピンがLOW状態の場合。

### **例**
```cpp
void setup() {
  pinMode(2, INPUT); // ピン2を入力モードに設定
}

void loop() {
  int buttonState = digitalRead(2); // ピン2の状態を読み取る

  if (buttonState == HIGH) {
    Serial.println("ボタンが押されました"); // printf()と同じ
  } else {
    Serial.println("ボタンが離されました");
  }
}
```

---

## **実践的な応用例**

### **例1: ボタンを押すとLEDが点灯する**
```cpp
void setup() {
  pinMode(2, INPUT_PULLUP); // ピン2を入力モード（プルアップ）に設定
  pinMode(13, OUTPUT);      // ピン13を出力モードに設定
}

void loop() {
  if (digitalRead(2) == LOW) { // ボタンが押された場合（INPUT_PULLUPなので、LOWは押された状態）
    digitalWrite(13, HIGH);   // LEDを点灯
  } else {
    digitalWrite(13, LOW);    // LEDを消灯
  }
}
```

---

### **例2: ボタンでモーターの回転を制御する**
この例では、モータードライバを使用し、1つのDCモーターを制御します。

#### **回路構成**
- **モータードライバ**:
  - `IN1` → Arduino ピン8  
  - `IN2` → Arduino ピン9  
- **ボタン**:
  - 片方をArduinoのピン2に接続（プルアップモードを使用）。  
- **モーター**:
  - モータードライバのモーター出力端子に接続。

---

### **コード例**
```cpp
// ピン定義
const int motorPin1 = 8;  // モータードライバIN1
const int motorPin2 = 9;  // モータードライバIN2
const int buttonPin = 2;  // ボタン入力ピン

void setup() {
  // モータードライバのピンを出力モードに設定
  pinMode(motorPin1, OUTPUT);
  pinMode(motorPin2, OUTPUT);
  
  // ボタンのピンを入力モード（プルアップ）に設定
  pinMode(buttonPin, INPUT_PULLUP);
}

void loop() {
  // ボタンの状態を読み取る
  int buttonState = digitalRead(buttonPin);
  
  if (buttonState == LOW) { // ボタンが押されたら
    // モーターを正転（逆転であれば、HIGHとLOWを入れ替える）
    digitalWrite(motorPin1, HIGH); 
    digitalWrite(motorPin2, LOW);
  } else {
    // モーターを停止（LOWとLOWで停止する）
    digitalWrite(motorPin1, LOW);
    digitalWrite(motorPin2, LOW);
  }
}
```

---

## **課題**

### **1日目. LED点滅**
- ピン番号13に接続されたLEDを、1秒ごとに点滅させるプログラムを書いてください。

---

### **2日目. ボタンを使う**
- ボタン（ピン番号2）を押すと、ボタンが押されたことを表示するプログラムを書いてください。
- printf()ではなく、Serial.print()を使用してください。

---

### **3日目. ボタン操作でLEDの状態を変更**
- ボタン（ピン番号2）を押すとLED（ピン番号13）が点灯するプログラムを書いてください。
- ボタンが離されたらLEDが消灯するようにしてください。

---

### **4日目. 複数LEDの制御**
- ピン番号8、9、10に接続された3つのLEDを、順番に点灯させてください（例: LED1 → LED2 → LED3 → LED1…）。

---

### **5日目. ボタンで状態をトグル**
- ボタンを押すたびにLED（ピン番号13）の状態を切り替える（トグルする）プログラムを書いてください。

---

### **6日目. モーターの制御**
- 一定時間（5秒）モーターを動作させた後、自動で停止するプログラムを書いてください。

---

### **7日目. 2つのボタンでモーターを制御**
- ボタン１（ピン番号2）を押すとモーターを正転させ、ボタン２（ピン番号3）を押すとモーターを逆転させるプログラムを書いてください。
- どちらのボタンも押されていない場合は、モーターを停止させます。

---