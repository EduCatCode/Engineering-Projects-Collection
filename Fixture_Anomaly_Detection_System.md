# Fixture Anomaly Detection System

## 目錄

1. [專案簡介](#專案簡介)
2. [專案目標](#專案目標)
3. [安裝與工件加工示意](#安裝與工件加工示意)
4. [特徵觀察](#特徵觀察)
   - [時域特徵](#時域特徵)
   - [頻域特徵](#頻域特徵)
5. [恩展夾具異常偵測分析](#恩展夾具異常偵測分析)
   - [加工訊號切割](#加工訊號切割)
   - [正常加工訊號特徵觀察(FFT)](#正常加工訊號特徵觀察fft)
   - [0.15mm加工訊號頻域轉換](#015mm加工訊號頻域轉換)
   - [0.25mm加工訊號頻域轉換](#025mm加工訊號頻域轉換)
6. [未來發展](#未來發展)

## 專案簡介

本專案旨在開發一套夾具異常預警系統，利用電流感測模組和振動感測模組來監測加工過程中的異常狀態。

## 專案目標

- 開發一套能夠準確偵測夾具異常狀態的預警系統。
- 使用電流感測模組和振動感測模組進行即時監控。
- 提高加工過程中的安全性和穩定性，減少不必要的損耗和停機時間。

## 安裝與工件加工示意

### 多角度工件拍攝示例

<div style="display: flex;">
  <img src="https://hackmd.io/_uploads/SkxH0nm8C.jpg" alt="多角度工件拍攝示例1" width="45%">
  <img src="https://hackmd.io/_uploads/HJUHA2Q80.jpg" alt="多角度工件拍攝示例2" width="45%">
</div>

### 電流感測模組安裝位置

![電流感測模組安裝位置](https://hackmd.io/_uploads/H1FrRnm8C.jpg)

### 振動感測模組安裝位置

![振動感測模組安裝位置](https://hackmd.io/_uploads/SJoHChQIR.jpg)


## 特徵觀察

### 時域特徵

<div style="display: flex;">
  <img src="https://hackmd.io/_uploads/HkaOC27UR.png" alt="正常狀態下空轉50秒的電流訊號" width="30%">
  <img src="https://hackmd.io/_uploads/SJytRnQLR.png" alt="夾持不當空轉50秒的電流訊號" width="30%">
  <img src="https://hackmd.io/_uploads/Sy-FA37I0.png" alt="兩圖合在一起觀察" width="30%">
</div>


### 頻域特徵

透過對訊號進行快速傅立葉變換（FFT），我們觀察到當頻率約為83赫茲時，能量顯著較高。細部放大觀察揭示了正常與異常狀態間的差異。在83赫茲頻率處，正常狀態的能量約為480單位，而異常狀態下則降至約420單位。

<div style="display: flex;">
  <img src="https://hackmd.io/_uploads/rkhqR2mLA.png" alt="正常訊號的FFT分析" width="45%">
  <img src="https://hackmd.io/_uploads/HJYoA2mUA.png" alt="異常訊號的FFT分析" width="45%">
</div>

<div style="display: flex;">
  <img src="https://hackmd.io/_uploads/Hkis02Q8A.png" alt="在83赫茲頻率處觀察到的正常訊號峰值" width="45%">
  <img src="https://hackmd.io/_uploads/Hkyh0nXIC.png" alt="在83赫茲頻率處觀察到的異常訊號峰值" width="45%">
</div>

此外，在82赫茲以下頻率範圍內，兩者的能量波幅亦存在顯著差異。然而，這些觀察僅基於單一樣本的比較，且在空轉約50秒的非標準加工條件下進行，因此只能作為初步參考。在實際應用中，應結合更多指標，如振動的增加，以提高診斷的準確性。

<div style="display: flex;">
  <img src="https://hackmd.io/_uploads/B173RnQLR.png" alt="低於83赫茲頻率的正常訊號峰值觀察" width="45%">
  <img src="https://hackmd.io/_uploads/SJrh0hmUA.png" alt="低於83赫茲頻率的異常訊號峰值觀察" width="45%">
</div>


## 恩展夾具異常偵測分析

### 加工訊號切割

觀察多筆交工後，我們設定振幅0.3時為加工開始的閥值，並結合了加工時長與取樣率的計算，以切割每一次的加工周期，左至右分別為正常加工、0.15mm、0.25mm加工。

<div style="display: flex;">
  <img src="https://hackmd.io/_uploads/Hk1x1p7LC.png" alt="正常加工" width="30%">
  <img src="https://hackmd.io/_uploads/rk4l16QUC.png" alt="0.15mm加工" width="30%">
  <img src="https://hackmd.io/_uploads/ByLxkp7LA.png" alt="0.25mm加工" width="30%">
</div>

### 正常加工訊號特徵觀察(FFT)

利用三種不同的加工，2次各做FFT比較圖(一次6秒)，振幅無太大差異。

<div style="display: flex;">
  <img src="https://hackmd.io/_uploads/Bk2g167L0.png" alt="正常加工1" width="30%">
  <img src="https://hackmd.io/_uploads/ryRgy67IA.png" alt="正常加工2" width="30%">
  <img src="https://hackmd.io/_uploads/SygZJ67UC.png" alt="正常加工3" width="30%">
</div>

### 正常加工訊號頻域轉換

使用三筆加工訊號做頻域特徵轉換，每秒轉換一次。
1. **Mean**: 觀察到前二秒的平均振幅較高。
2. **Third moment**: 檢查訊號的非對稱性，並沒有明顯特徵。
3. **Forth moment**: 檢查異常突出訊號成份，第前3秒時異常值較多。

<div style="display: flex;">
  <img src="https://hackmd.io/_uploads/rJw-JaXUA.png" alt="正常加工頻域1" width="30%">
  <img src="https://hackmd.io/_uploads/ryt-ypQIR.png" alt="正常加工頻域2" width="30%">
  <img src="https://hackmd.io/_uploads/S12Wkp7I0.png" alt="正常加工頻域3" width="30%">
</div>

### 0.15mm加工訊號頻域轉換

使用三筆加工訊號做頻域特徵轉換，每秒轉換一次。
1. **Mean**: 觀察到並沒有向正常訊號一樣前二秒的平均振幅較高，也有可能樣本太少。
2. **Third moment**: 檢查訊號的非對稱性，也沒有明顯特徵。
3. **Forth moment**: 檢查異常突出訊號成份，也沒有像正常訊號前3秒時異常值較多，分配不均。

<div style="display: flex;">
  <img src="https://hackmd.io/_uploads/ByfMJpXL0.png" alt="0.15mm加工頻域1" width="30%">
  <img src="https://hackmd.io/_uploads/SJVGkamL0.png" alt="0.15mm加工頻域2" width="30%">
  <img src="https://hackmd.io/_uploads/Sy8fy67LR.png" alt="0.15mm加工頻域3" width="30%">
</div>

### 0.25mm加工訊號頻域轉換

使用二筆加工訊號做頻域特徵轉換，每秒轉換一次。
1. **Mean**: 觀察到與正常訊號一樣前二秒的平均振幅較高，在這假設不論正常或異常加工，應該都有這特性。
2. **Third moment**: 檢查訊號的非對稱性，也沒有明顯特徵。
3. **Forth moment**: 檢查異常突出訊號成份，也沒有像正常訊號前3秒時異常值較多，分配不均。

<div style="display: flex;">
  <img src="https://hackmd.io/_uploads/rJAf1p7LC.png" alt="0.25mm加工頻域1" width="45%">
  <img src="https://hackmd.io/_uploads/BJk7J678C.png" alt="0.25mm加工頻域2" width="45%">
</div>


## 未來發展

未來我們將繼續優化夾具異常預警系統，並考慮以下發展方向：

- **數據集擴展**：我們計劃增加更多不同條件下的數據集，例如來自不同工件、不同加工環境和操作條件的數據，以提高模型的泛化能力，讓系統能在更廣泛的情境中精確運作。這不僅可以提升系統的準確性，還能讓模型適應更多變的真實世界加工行為。
- **模型改進**：未來我們計劃融合更先進的深度學習算法，同時保留目前演算法的優點。具體而言，我們將探索結合圖神經網絡（Graph Neural Networks）和強化學習（Reinforcement Learning）的方法，來進一步提升夾具異常偵測的精確性和可靠性。這樣的改進將使得模型在處理複雜的加工行為時更加靈活和高效。
- **即時監控**：我們將開發即時監控模組，實現在線預測和即時反饋。這將包括一個即時數據流處理系統，能夠在加工過程中即時檢測並預測異常狀態，提供即時的安全提醒和反饋，進一步保障加工安全和效率。
