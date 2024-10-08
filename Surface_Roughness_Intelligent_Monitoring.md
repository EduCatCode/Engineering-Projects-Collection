# 表面粗糙度智能監測系統

## 目錄

1. [專案簡介](#專案簡介)
2. [專案目標](#專案目標)
3. [安裝與數據收集](#安裝與數據收集)
4. [實驗 Part1](#實驗-part1)
5. [實驗 Part2](#實驗-part2)
6. [實驗設定詳細說明](#實驗設定詳細說明)
7. [實驗結果紀錄](#實驗結果紀錄)
8. [初步觀察與深入分析](#初步觀察與深入分析)
9. [結論](#結論)

## 專案簡介

本專案旨在開發一套表面粗糙度智能監測系統，利用振動感測器和電流感測器監測 EQUIPTOP 1224CNC 機台在粗研磨過程中的振動與電流特性。

![image](https://hackmd.io/_uploads/SkLd-nraA.png)

## 主要成就

![napkin-selection (5)](https://hackmd.io/_uploads/H1jELD3aR.png)

- 預測準確度：成功實現加工過程中表面粗糙度的即時監控，並實際應用於產線的 120 次加工中，預測準確度達到 90%（120 次中有 109 次預測正確）。
- 穩定性提升：系統有效減少不必要的機台停機時間，穩定加工品質並減少產品不合格率。
- 損耗降低：通過即時數據監控，減少機台的非必要停機時間和材料浪費，最終使生產效率提高約 12%。

## 專案目標

- 開發一套能夠準確監測和分析表面粗糙度的智能系統。
- 使用振動感測器和電流感測器進行實時監控。
- 提高加工過程中的穩定性和品質，減少不必要的損耗和停機時間。

## 安裝與數據收集

### 安裝 EQUIPTOP 1224CNC 機台振動感測器與電流感測器

#### 目的

測量機台在粗研磨下的振動與電流特性。

#### 安裝電流感測器

擷取數據展示與電流感測器位置與機台走線圖：

| 安裝感測儲存模組與感測器 | 電控箱安裝比流器位置 | 安裝完成且放置於電控箱上 |
|:--------------------------:|:--------------------:|:-------------------------:|
| ![圖片1](https://hackmd.io/_uploads/S1zlUnH8C.jpg)|![圖片2](https://hackmd.io/_uploads/H1we83HUC.jpg) |![圖片3](https://hackmd.io/_uploads/By9lU2HUA.jpg)|

## 實驗 Part1

### 六筆加工完成工件RA

右圖為工件6砂輪主軸電流訊號RMS（區分6面）

| 工件 | 第一面 RA | 第二面 RA | 第三面 RA | 第四面 RA | 第五面 RA | 第六面 RA | 進給量 (面板左) | 進給量 (面板右) | 間距 |
|:---:|:--------:|:--------:|:--------:|:--------:|:--------:|:--------:|:--------:|:--------:|:--------:|
| 1 | 0.168 | 0.143 | 0.144 | 0.135 | 0.128 | 0.138 | 9um | 22um | 460mm |
| 2 | 0.170 | 0.172 | 0.162 | 0.160 | 0.162 | 0.212 | 9um | 22um | 460mm |
| 3 | 0.200 | 0.181 | 0.163 | 0.185 | 0.190 | 0.242 | 10um | 25um | 480mm |
| ... | ... | ... | ... | ... | ... | ... | ... | ... | ... |

| 工件1 | 電流訊號切分工序 |
|:-----:|:-----:|
| ![圖片4](https://hackmd.io/_uploads/rJ1bU3BLA.jpg)| ![圖片5](https://hackmd.io/_uploads/SJ8Z82H80.png) |

## 實驗 Part2

### 加工較細的工件

使用振動訊號當作區分6面的工序

| 加工較細的工件 | 使用振動訊號區分6面 |
|:--------------:|:-----------------:|
| ![圖片6](https://hackmd.io/_uploads/rJLZLnSI0.jpg) | ![圖片7](https://hackmd.io/_uploads/r1UWU3BL0.png) |

### 六筆加工完成工件RA（細的工件）

| 工件 | 第一面 RA | 第二面 RA | 第三面 RA | 第四面 RA | 第五面 RA | 第六面 RA | 進給量 (面板左) | 進給量 (面板右) | 間距 |
|:---:|:--------:|:--------:|:--------:|:--------:|:--------:|:--------:|:--------:|:--------:|:--------:|
| 1 | 0.139 | 0.221 | 0.227 | 0.282 | 0.232 | 0.257 | 8um | 18um | 490mm |
| 2 | 0.131 | 0.194 | 0.217 | 0.224 | 0.227 | 0.230 | 9um | 18um | 500mm |
| 3 | 0.121 | 0.218 | 0.226 | 0.190 | 0.234 | 0.230 | 9um | 18um | 520mm |
| ... | ... | ... | ... | ... | ... | ... | ... | ... | ... |

## 實驗設定詳細說明

實驗旨在探討兩個關鍵加工參數對於加工表面粗糙度（RA值）的影響。具體參數設定如下：

- **因素 1 (研磨進給)**：此因素考量了三個不同水平的研磨進給量，分別為 8um、9um 和 10um，旨在探討研磨進給量對加工表面質量的影響。
- **因素 2 (修砂進給量)**：此因素亦設定了三個水平，分別為 490mm/min、550mm/min 和 600mm/min，以評估修砂進給量變化對RA值的影響。
- **主軸轉速**：為控制變量，固定於 1600rpm，確保實驗結果的一致性和可比較性（為實際加工參數不更改）。

### 實驗參數設定

| Round | 研磨進給 (um) | 修砂進給量 (mm/min) |
|:-----:|:------------:|:-------------------:|
| 1 | 8 | 490 |
| 2 | 8 | 490 |
| 3 | 9 | 600 |
| 4 | 10 | 600 |
| 5 | 10 | 490 |
| 6 | 9 | 490 |
| 7 | 8 | 550 |
| 8 | 10 | 550 |
| 9 | 9 | 550 |
| 10 | 10 | 600 |
| 11 | 8 | 490 |

依兩個變因設計9 Round並記錄下6面的RA（每Round進行2次）。10 Round與11 Round為驗證我們假設實驗。

### 實驗結果紀錄

| Round | 大致加工次數 | 研磨進給 (um) | 修砂進給量 (mm/min) | 第一次RA | 第二次RA |
|:-----:|:------------:|:------------:|:-------------------:|:-------:|:-------:|
| 1 | 1、2 | 8 | 600 | 0.180, 0.174, 0.182, 0.152, 0.155, 0.191 | 0.170, 0.198, 0.177,0.169, 0.214, 0.169 |
| 2 | 3、4 | 8 | 490 | 0.190, 0.170, 0.164, 0.166, 0.178, 0.180 | 0.179, 0.160, 0.170, 0.176, 0.194, 0.200 |
| 3 | 5、6 | 9 | 600 | 0.187, 0.172, 0.202, 0.192, 0.194, 0.185 | 0.180, 0.210, 0.172, 0.163, 0.181, 0.185 |
| ... | ... | ... | ... | ... | ... |


### 數據預處理

首先將收集到的加工次數、研磨進給、修砂進給量與各面RA值整理成結構化數據，以便於後續的統計分析與機器學習處理。


### 特徵觀察

從數據中識別出RA值的關鍵特徵，例如哪一面的RA值通常最高，哪一面的RA值最接近平均值等，以獲得更深入的見解。

#### 相關性分析

通過熱力圖對相關係數進行視覺化展示並透過趨勢圖得知了加工次數對RA值的最影響。

- **研磨進給 (um) 與 RA 值**：研磨進給與各面RA值之間的相關性不是非常強，這表明研磨進給的變化對RA值的影響可能有限。
- **修砂進給量 (mm/min) 與 RA 值**：修砂進給量與RA值之間也沒有顯示出強烈的相關性，意味著修砂進給量的改變可能不是影響RA值的主要因素。

![圖片8](https://hackmd.io/_uploads/r1LZLnSIR.png)


### 描述性統計分析

- **研磨進給 (um)**：平均值為9.05um，變化範圍從8um到10um，表示大多數數據集中在這個範圍內。
- **修砂進給量 (mm/min)**：平均值為549.05mm/min，最小值為490mm/min，最大值為600mm/min，顯示修砂進給量在這個範圍內變動。
- **RA值**：
  - RA_1至RA_6的平均值分別為0.215、0.215、0.208、0.205、0.209、0.218，顯示不同面之間的RA值相差不大。
  - RA_6的平均值最高（0.218），可能表示第六面通常有稍高的粗糙度。
  - RA_4的平均值最低（0.205），顯示第四面可能相對較平滑。

我們發現RA6的平均值最高，這可能表明在給定的加工條件下，第六面通常會有較高的粗糙度，因為磨完六面才會修砂一次，故第六面材料移除力比較低。

### 線性回歸模型分析結果

以下是針對每個RA值的線性回歸模型分析結果，包括模型系數（Coefficients）、均方誤差（MSE）以及決定系數（R²）：

| RA值 | Coefficients（系數） | MSE（均方誤差） | R²（決定系數） |
|:----:|:----------------------:|:----------------:|:--------------:|
| RA_1 | [ 0.01302654, -0.00020338 ] | 0.000531403768440758 | 0.25032708947868487 |
| RA_2 | [ 0.01743559, -0.00010089 ] | 0.0007154697700379554 | 0.2311137821956305 |
| RA_3 | [ 1.35824961e-02, -4.68631391e-05 ] | 0.0007717283768698377 | 0.1411188006276614 |
| ... | ... | ... | ... |

### 加工次數影響分析

| RA與加工次數關係圖 | 加上考量修砂給擊量的關係圖 |
|:-------------------:|:-----------------------------:|
| ![圖片9](https://hackmd.io/_uploads/H1IWU2rUC.png)| ![圖片10](https://hackmd.io/_uploads/ryIZI2S8R.png) |

## 初步觀察與深入分析

### 材料去除率（Material Removal Rate, MRR）的深入分析

材料去除率，通常以MRR表示，是衡量研磨加工效率的重要指標。MRR定義為單位時間內從工件表面去除的材料體積，其值不僅受研磨力的影響，還與砂輪與工件間的接觸面積、砂輪的磨損情況緊密相關。當砂輪的尺寸變小，即直徑減少時，其每轉一圈所經過的路徑長度隨之縮短，這可能導致在相同的時間內，去除的材料量減少，從而降低了MRR。

![圖片11](https://hackmd.io/_uploads/S1e8WUhHU0.png)


綜合上述因素，當砂輪尺寸變小，由於接觸面積減少及每轉一圈的切削路徑縮短，由於久博在砂輪主軸轉速不變情形，加工次數越多當砂輪變小時，材料移除率就會下降。因此，在實驗過程中，可發現即使是同參數但RA值在加工次數提升時，RA值也會跟著提高。

(若利用查表區間簡化模型訓練預測，區間為20如左圖、50如右圖)

### 建議

- 若利用查表區間簡化模型訓練預測，現場操作人員轉述約加工200~300工件會換一次砂輪，區間為20如左圖、50如右圖
- 久博實際參數設定模式，當天早上前3個工件測試參數，若符合標準RA則當天就固定此參數。
- 加工工件（中）使用時間約30分鐘、加工工件（小）使用時間約20分鐘，若一天8小時，工件（中）可加工16個，工件（小）可加工24個，與我們上述實驗提出20為一個區間相符。
- 建議是否請久博紀錄每天前3個工件參數及RA，提供我們訓練。

### 資料樣本設計

我們選取了18個加工工件的振動訊號。針對每個工件，其加工的六個不同面，同時對每一面的表面粗糙度（RA）測量記錄，則有18工件×6面 = 108個原始樣本。

為了提升模型的訓練效果，我們進一步依照表面粗糙度是否符合品質標準將資料分為合格與不合格兩部分。並利用了視窗移動（window moving）的方法，透過對每個樣本的10秒訊號進行滑動視窗處理，以此擴增資料樣本量。

透過這種方法，我們最終擴展了資料集到791個樣本作為訓練集，以及302個樣本作為測試集。

這種資料量的擴展有助於提高模型的泛化能力，確保其在實際應用中的準確性和可靠性。

### 時域分析視覺化

圖中展示了兩種不同的加工，左圖對應的表面粗糙度為RA 0.174，而右圖的表面粗糙度為RA 0.247。發現第4秒時的振幅都是最高的，不論從Rawdata、RMS、Mean都可以觀察到，圖示找RA最低與RA最高來視覺化觀察特徵，但合格與不合格的RA振幅的高低不太明顯。

| RA 0.174 | RA 0.247 |
|:--------:|:--------:|
| ![圖片12](https://hackmd.io/_uploads/ryLbInrU0.png)| ![圖片13](https://hackmd.io/_uploads/r1xUb8hBLA.png) |

### 模型訓練分析

在分析砂輪加工相關的資料集時，我們觀察到SVM的效果最好，這也驗證SVM在處理線性可分問題上的高效表現而顯示出較高的準確度。

特別是，砂輪加工次數、研磨進給和修砂進給量這三個參數與目標變數的關係較為直接且顯著，這些特徵的線性關係適合使用SVM進行模型建構。

儘管SVM在目前資料集上表現優異，但我們也需警惕潛在的過度擬合問題。過度擬合可能導致模型在訓練資料上表現出色，但目前資料驗證中並未發現。

| 多模型建立 | 多模型混淆矩陣 |
|:----:|:----:|
| ![圖片14](https://hackmd.io/_uploads/SkeIZL3rU0.png) |![圖片15](https://hackmd.io/_uploads/ByKWUhSLA.png)|

### 結論

儘管SVM在目前資料集上表現優異，但我們也需警惕潛在的過度擬合問題，為了驗證這一點，需要收集更多的樣品。

與其他模型（如神經網路、決策樹等）進行效能對比，不僅限於訓練集、測試集，可以再來預測新的資料集。

其他模型如神經網路、決策樹、隨機森林、神經網路和高斯過程的表現雖然都在70%左右，但這現象我們可能需要進一步調整模型參數或考慮採用更複雜的非線性模型來捕捉資料中的高階關係，或進行特徵工程以提取更有資訊量的特徵，增強模型的預測能力。
