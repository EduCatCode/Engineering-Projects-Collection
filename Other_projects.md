# Arduino-RaspberryPi-SmartCar

## 目錄

1. [專案簡介](#專案簡介)
2. [使用材料](#使用材料)
3. [作業目的](#作業目的)
4. [硬體組裝](#硬體組裝)
5. [程式設計](#程式設計)
6. [真值表](#真值表)
7. [實際成品](#實際成品)
8. [其他專案描述](#其他專案描述)
9. [未來發展](#未來發展)

## 專案簡介

本專案旨在利用Arduino和Raspberry Pi製作一個具有影像辨識功能的智能小車。小車可以利用紅外線感測器循跡，並且通過樹莓派進行影像處理以實現更多智能功能。

## 使用材料

| 品項           | 品名           | 數量 | 備註                      |
| -------------- | -------------- | ---- | ------------------------- |
| 1              | Arduino        | 2    |                           |
| 2              | 紅外線感測器   | 3    |                           |
| 3              | 馬達           | 2    |                           |
| 4              | 電池           | 1    | 組                        |
| 5              | 輪子           | 2    |                           |
| 6              | 輔助輪         | 1    |                           |
| 7              | 車板           | 1    |                           |
| 8              | 馬達控制器 L298N| 1    |                           |
| 9              | 杜邦線         | 1    | 捆                        |

## 作業目的

1. 利用紅外線感測器，讓智能小車循著黑色膠帶前進。
2. 結合Raspberry Pi進行影像辨識，實現更高階的智能功能。

## 硬體組裝

### 步驟

1. 安裝Arduino板到車板上。
2. 將馬達固定在車板兩側，安裝輪子和輔助輪。
3. 連接紅外線感測器到Arduino，分別放置在小車前端。
4. 安裝電池和馬達控制器L298N，連接馬達控制器到馬達和Arduino。
5. 使用杜邦線將各元件連接到Arduino和Raspberry Pi上。

![Arduino Car](https://hackmd.io/_uploads/Sk4n_3HIC.jpg)

## 程式設計

### Arduino程式碼

```cpp
// Arduino 追跡小車程式碼示例
#define LEFT_SENSOR_PIN A0
#define CENTER_SENSOR_PIN A1
#define RIGHT_SENSOR_PIN A2
#define MOTOR_LEFT_FORWARD 9
#define MOTOR_LEFT_BACKWARD 8
#define MOTOR_RIGHT_FORWARD 7
#define MOTOR_RIGHT_BACKWARD 6

void setup() {
  pinMode(LEFT_SENSOR_PIN, INPUT);
  pinMode(CENTER_SENSOR_PIN, INPUT);
  pinMode(RIGHT_SENSOR_PIN, INPUT);
  pinMode(MOTOR_LEFT_FORWARD, OUTPUT);
  pinMode(MOTOR_LEFT_BACKWARD, OUTPUT);
  pinMode(MOTOR_RIGHT_FORWARD, OUTPUT);
  pinMode(MOTOR_RIGHT_BACKWARD, OUTPUT);
}

void loop() {
  int leftSensor = digitalRead(LEFT_SENSOR_PIN);
  int centerSensor = digitalRead(CENTER_SENSOR_PIN);
  int rightSensor = digitalRead(RIGHT_SENSOR_PIN);
  
  // 真值表對應的動作
  if (leftSensor == 0 && centerSensor == 0 && rightSensor == 0) {
    moveForward();
  } else if (leftSensor == 0 && centerSensor == 0 && rightSensor == 1) {
    turnLeft();
  } else if (leftSensor == 0 && centerSensor == 1 && rightSensor == 0) {
    moveBackward();
  } else if (leftSensor == 0 && centerSensor == 1 && rightSensor == 1) {
    turnLeft();
  } else if (leftSensor == 1 && centerSensor == 0 && rightSensor == 0) {
    turnRight();
  } else if (leftSensor == 1 && centerSensor == 0 && rightSensor == 1) {
    moveForward();
  } else if (leftSensor == 1 && centerSensor == 1 && rightSensor == 0) {
    turnRight();
  } else if (leftSensor == 1 && centerSensor == 1 && rightSensor == 1) {
    moveBackward();
  }
}

void moveForward() {
  digitalWrite(MOTOR_LEFT_FORWARD, HIGH);
  digitalWrite(MOTOR_LEFT_BACKWARD, LOW);
  digitalWrite(MOTOR_RIGHT_FORWARD, HIGH);
  digitalWrite(MOTOR_RIGHT_BACKWARD, LOW);
}

void turnLeft() {
  digitalWrite(MOTOR_LEFT_FORWARD, LOW);
  digitalWrite(MOTOR_LEFT_BACKWARD, HIGH);
  digitalWrite(MOTOR_RIGHT_FORWARD, HIGH);
  digitalWrite(MOTOR_RIGHT_BACKWARD, LOW);
}

void moveBackward() {
  digitalWrite(MOTOR_LEFT_FORWARD, LOW);
  digitalWrite(MOTOR_LEFT_BACKWARD, HIGH);
  digitalWrite(MOTOR_RIGHT_FORWARD, LOW);
  digitalWrite(MOTOR_RIGHT_BACKWARD, HIGH);
}

void turnRight() {
  digitalWrite(MOTOR_LEFT_FORWARD, HIGH);
  digitalWrite(MOTOR_LEFT_BACKWARD, LOW);
  digitalWrite(MOTOR_RIGHT_FORWARD, LOW);
  digitalWrite(MOTOR_RIGHT_BACKWARD, HIGH);
}

```


## 真值表

| 狀態 | 執行動作 | 備註 |
| ---- | -------- | ---- |
| 000  | 前進     | 三個 IR 皆在黑色膠帶上，可能因三個 IR 前後位置不一導致出現 IR 皆感測到膠帶，故設定前進重新偵測。 |
| 001  | 左轉     | 車子微偏右 |
| 010  | 後退     | 因不可能發生，但三個 IR 前後位置不一以免萬一，故設定退後重新偵測。 |
| 011  | 左轉     | 車子偏右 |
| 100  | 右轉     | 車子微偏左 |
| 101  | 前進     | 正常狀況 |
| 110  | 右轉     | 車子偏左 |
| 111  | 後退     | 已偏離軌道，故設定退後重新偵測。 |

## 實際成品

![Tracking](https://hackmd.io/_uploads/Bkc6OhSU0.png)


# 簡易記帳系統

## 界面示意：
![Screenshot from 2023-05-15 15-52-26](https://github.com/Yen-Wei-Liang/Simple-Accounting-System/assets/127264553/7277b0c7-f13a-4293-9495-79ae088c41b9)

## 功能

### 1. 顯示當前餘額
此功能允許用戶即時查看當前的帳戶餘額，幫助用戶了解自己的財務狀況。

### 2. 新增收入
用戶可以新增收入項目，需提供描述、金額和日期，系統會自動更新餘額。

### 3. 新增支出
用戶可以新增支出項目，需提供描述、金額和日期，系統會自動更新餘額。

### 4. 依據時間區間顯示記帳紀錄
用戶可以選擇特定的時間區間來查看該期間內的所有記帳紀錄，便於財務分析。

### 作者
Yen-Wei-Liang

## 環境要求

- Python 3.8
- Tkinter
- SQLite3

## 安裝依賴

```bash
pip install tkinter
pip install pysqlite3

```

