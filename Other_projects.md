# 專案目錄

1. [Arduino藍芽與IR循機車](#Arduino藍芽與IR循機車)
2. [實驗室巡邏與自動導航系統](#實驗室巡邏與自動導航系統)
3. [貓咪檢測與追蹤系統](#貓咪檢測與追蹤系統)
4. [乳牛行為預測系統](#乳牛行為預測系統)
5. [機器人自動避障系統](#機器人自動避障系統)
6. [黑暗中人物識別系統](#黑暗中人物識別系統)
7. [簡易記帳系統](#簡易記帳系統)

# Arduino藍芽與IR循機車

## 目錄

1. [專案簡介](#專案簡介)
2. [使用材料](#使用材料)
3. [作業目的](#作業目的)
4. [硬體組裝](#硬體組裝)
5. [程式設計](#程式設計)
6. [真值表](#真值表)
7. [實際成品](#實際成品)

## 專案簡介

本專案旨在利用Arduino和Raspberry Pi製作一個具有影像辨識功能的智能小車。小車可以利用紅外線感測器循跡，並且通過樹莓派進行影像處理以實現更多智能功能。

## 使用材料

| 品項           | 品名           | 數量 | 備註                      |
| -------------- | -------------- | ---- | ------------------------- |
| Arduino        | 2              |      |                           |
| 紅外線感測器   | 3              |      |                           |
| 馬達           | 2              |      |                           |
| 電池           | 1              | 組   |                           |
| 輪子           | 2              |      |                           |
| 輔助輪         | 1              |      |                           |
| 車板           | 1              |      |                           |
| 馬達控制器 L298N| 1             |      |                           |
| 杜邦線         | 1              | 捆   |                           |

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




# 貓咪檢測與追蹤系統

## 目錄

1. [專案簡介](#專案簡介)
2. [主要技術與平台](#主要技術與平台)
3. [通信機制](#通信機制)
4. [應用場景](#應用場景)
5. [結論](#結論)
6. [真值表](#真值表)
7. [實際成品](#實際成品)


## 專案簡介
本專案旨在開發一套貓咪自動檢測與追蹤系統，透過Raspberry Pi整合OpenCV與YOLO演算法來實現實時的貓咪影像檢測。系統檢測到貓咪後，會透過串列通信將位置資料傳送至Arduino控制器。

## 主要技術與平台
- **Raspberry Pi**: 作為主要的處理單元，負責執行OpenCV與YOLO演算法來識別貓咪的位置與動態。
- **OpenCV**: 提供影像處理功能，協助改善檢測效率與準確性。
- **YOLO (You Only Look Once)**: 實時物體檢測系統，用於快速且準確的物體辨識。
- **Arduino**: 接收Raspberry Pi發送的數據，並控制電機調整方向，使機器人能朝貓咪移動。
- **ROS (Robot Operating System)**: 用於Arduino的機器人控制系統，實現高度模塊化的機器人控制。

## 通信機制
使用UART串列通信介面，Raspberry Pi與Arduino之間進行高效率的數據傳輸，以確保系統響應速度。

## 應用場景
此系統可應用於寵物監控、自動餵食或其他與貓咪相關的自動化任務。

## 結論
在本專案中，我們比較了使用YOLO和OpenCV進行物體檢測的效率與準確性。經過測試，YOLO提供了更迅速及更高的辨識正確率。然而，即使使用輕量化的YOLO Lite模型，其準確度大約只有70%，這在實際應用中可能會影響檢測的可靠性。為了優化檢測效果，我們設定每兩秒鐘進行一次檢測，這樣可以在1秒內處理2至3幀的數據。

考慮到即使存在貓咪，每次檢測未能辨識到的機率為30%。因此，連續三次檢測都未檢測到的機率約為0.3 * 0.3 * 0.3 = 0.027，即2.7%。這意味著，整體上，我們的系統有大約97.3%的機率能正確偵測到貓的存在，這對於實時應用來說是一個可接受的正確率。

## 實際成品

![螢幕擷取畫面 2024-06-24 130417](https://hackmd.io/_uploads/HJA_RuUU0.jpg)



# 實驗室巡邏與自動導航系統


## 目錄

1. [專案簡介](#專案簡介)
2. [技術架構與實施](#技術架構與實施)
3. [應用場景](#應用場景)
4. [結論](#結論)
5. [實際成品](#實際成品)

## 專案概述
本專案旨在開發一套綜合使用LiDAR SLAM技術、機器人與自動導航技術的實驗室巡邏與導航系統。通過精確地映射實驗室環境並實施自動巡邏任務，以提高安全性和監控效率。

## 技術架構與實施
- **LiDAR SLAM技術**: 利用雷達掃描與同步定位與地圖構建技術，精確創建實驗室的3D地圖。
- **Turtlebot機器人**: 配備LiDAR感測器的Turtlebot機器人，用於執行實驗室內的自動巡邏任務。


## 應用場景
此系統不僅適用於實驗室環境，還能夠擴展至其他需要精確地圖與自動巡邏的場所，如倉庫、醫院或學校，增強安全與自動化水平。


## 結論
在本專案中，我們整合了先進的導航技術和自動控制系統來提升實驗室環境的管理效率與安全監控能力。巡邏機器人啟動時會首先進行自我校正，通過轉圈對應地圖來增加其路徑規劃的準確度。此外，我們還裝配了超音波感測器，以實時偵測並應對動態障礙物，若前方檢測到障礙物，機器人將強制停止，直到障礙物清除後才繼續前進。這些技術的整合不僅提高了操作的安全性，也增強了系統的可靠性。未來，我們計劃探索更多應用場景，以進一步拓展系統的功能與應用範圍。

## 實際成品

![螢幕擷取畫面 2024-06-24 131236](https://hackmd.io/_uploads/S1yPgtULR.jpg)




# 機器人自動避障系統

## 目錄

1. [專案簡介](#專案簡介)
2. [技術實施](#技術實施)
3. [訓練進度](#訓練進度)
4. [應用場景](#應用場景)
5. [結論](#結論)
6. [實際成品](#實際成品)

## 專案簡介
本專案目標在於開發一套能夠自動識別並避開動態障礙物的機器人控制系統。透過強化學習算法，訓練機器人在複雜環境中有效識別並迴避行人及其他移動障礙物。

## 技術實施
- **強化學習**: 採用Double Deep Q Network (DDQN) 算法，逐步學習最佳行動策略，以達到最大化預期獎勵。
- **感測技術**: 結合LiDAR與視覺系統，實時收集環境數據，確保機器人對周圍環境有精確的認知。
- **動態障礙物識別**: 採用先進的影像處理與物體識別技術，快速識別前方的動態障礙物，特別是在含有多達五名行人的8x8環境中。

## 訓練進度
- **初級訓練**: 從2x2場地開始，逐步適應並優化機器人的行為。
- **中級訓練**: 擴展至4x4場地，增加障礙物與路徑計劃的複雜度。
- **高級訓練**: 嘗試在8x8的場地中進行訓練，儘管成功率低，推測是由於場域較大且行人數較少導致機器人難以有效學習避障策略。

## 應用場景
此系統適用於任何需要高度自動化與安全防護的環境，如工業生產線、公共場所、以及交通繁忙的市區街道等，能夠顯著提升操作效率與安全性。

## 結論
本專案透過結合強化學習與高精度感測技術，展示了一種自動避開動態障礙物的機器人系統，證明了這種方法在理論上是可行的。然而，從實驗階段轉向產品化實施仍面臨許多挑戰，還有一大段路與難題需要克服。未來，我們計劃進一步提升識別算法的準確性與反應速度，並探討如何在大場域中改善避障策略。此外，將著重於增強系統的可靠性與耐用性，以確保技術能夠在各種實際應用環境中有效運作，從而邁向產品化的路途。


## 實際成品

![螢幕擷取畫面 2024-06-24 132604](https://hackmd.io/_uploads/rJIF7KLUR.jpg)



# 乳牛行為預測系統


## 目錄

1. [專案簡介](#專案簡介)
2. [技術實施](#技術實施)
3. [挑戰與解決方案](#挑戰與解決方案)
4. [未來展望](#未來展望)
5. [結論](#結論)
6. [實際成品](#實際成品)


## 專案簡介
本專案的主要目標是在學校的牛舍環境中，利用YOLOv5結合Deep Sort算法進行乳牛的即時識別和行為分析。透過影像識別與序列數據分析，旨在後續精確預測乳牛的行為模式。

## 技術實施
- **YOLOv5**: 使用YOLOv5進行乳牛的即時影像識別，以其強大的物體檢測能力確保識別精度。
- **Deep Sort**: 結合Deep Sort追蹤算法，提升對個別乳牛的追蹤連續性，優化行為分析的準確性。
- **序列數據分析**: 執行基於序列的數據分析，從乳牛的行為模式中抽取有用信息，用於行為預測。

## 挑戰與解決方案
在實際識別過程中，由於牛舍面積相對較小且動物間可能發生重疊，導致Deep Sort的追蹤序列出現斷裂。為解決這一問題，我們計劃引入更精確的位置追蹤技術，以增強系統對乳牛個體的識別與追蹤能力，確保數據連續性並提高整體分析的準確性，目前始使用畫面中座標定位喝水區(在喝水)、飼料區(在吃飯)、其餘則為休息區(依造物件辨識的長方形來判斷牛是趴著還是站立)。

## 未來展望
此項技術的成功實施將顯著提升對乳牛行為的理解與管理效率，有助於改善牛舍的運營與動物福利。未來，我們將探索將此技術應用於更廣泛的農業與畜牧業場景，並持續優化系統的識別與分析能力。


![defaultNAS17AD1E-ONVIF_ONVIF ProfileS Cameras 2021-07-07-06-49-59](https://hackmd.io/_uploads/r1E9IY8IR.jpg)


# 黑暗中人物識別系統

## 目錄

1. [專案簡介](#專案簡介)
2. [系統架構與工作流程](#系統架構與工作流程)
3. [實現成果](#實現成果)



## 專案簡介
本專案旨在開發一套能在低光或黑暗環境中有效識別人物的影像處理系統。透過先進的影像分解與重構技術，提升圖像質量，從而實現在極端光線條件下的人物識別。

## 系統架構與工作流程
系統架構分為四大部分：分解（Decomposition）、調整（Adjustment）、重構（Reconstruct）以及多尺度殘差網絡（Multi-Scale RDN）。

### 1. 分解階段 (Decomposition)
- **DecomNet**: 將輸入的低光圖像分解為兩部分，一部分是照射度較低的區域（S_low），另一部分是照射度較高的區域（S_normal）。
- 此階段的目的是獨立處理不同光照條件下的圖像區域，為後續的增強與恢復提供準備。

### 2. 調整階段 (Adjustment)
- **EnhanceNet**: 針對低照度圖像進行質量提升，以增強圖像的可見性。
- **RestoreNet**: 對照度已調整的圖像進行恢復處理，確保圖像質量的整體一致性。

### 3. 重構階段 (Reconstruct)
- 將經過調整的圖像部分重構回原始圖像格式，保證圖像的完整性與自然感。

### 4. 多尺度殘差網絡 (Multi-Scale RDN)
- 利用殘差網絡在不同尺度上進行特徵提取和學習，進一步提升識別精度。
- 透過向上和向下取樣的方式，實現尺度的動態調整，以適應不同的識別需求。

## 實現成果
本系統採用最新的論文中描述的架構，成功解決了在黑暗環境中辨識人物的問題，顯著提升了夜間監控系統的識別率和可靠性。目前，我們正在進行演算法的微晶片前驗證階段，計劃將此技術實現於硬體中。為了適應晶片的需求，我們計畫簡化架構並將原本使用的PyTorch框架轉移到TensorFlow，以便更好地整合進微晶片技術。此技術的應用可廣泛應用於其他需要在低光條件下進行精確識別的場景。

![圖片1](https://hackmd.io/_uploads/rJge2OFUIA.png)






# 簡易記帳系統


## 目錄

1. [專案簡介](#專案簡介)
2. [實際介面](#實際介面)
3. [功能介紹](#功能介紹)
4. [環境要求](#環境要求)


## 專案簡介
本專案為一個簡易記帳系統，使用Python和Tkinter開發，主要是讓實驗室支出收錄記帳使用，能夠讓財務方便地新增收入和支出，並顯示當前餘額及記帳紀錄。

## 實際介面：
![Screenshot from 2023-05-15 15-52-26](https://github.com/Yen-Wei-Liang/Simple-Accounting-System/assets/127264553/7277b0c7-f13a-4293-9495-79ae088c41b9)

## 功能介紹

### 1. 顯示當前餘額
此功能允許用戶即時查看當前的帳戶餘額，幫助用戶了解自己的財務狀況。

### 2. 新增收入
用戶可以新增收入項目，需提供描述、金額和日期，系統會自動更新餘額。

### 3. 新增支出
用戶可以新增支出項目，需提供描述、金額和日期，系統會自動更新餘額。

### 4. 依據時間區間顯示記帳紀錄
用戶可以選擇特定的時間區間來查看該期間內的所有記帳紀錄，便於財務分析。


## 環境要求

- Python 3.8
- Tkinter
- SQLite3

