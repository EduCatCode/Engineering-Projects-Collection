# WaferDefectAI: Automated Wafer Anomaly Detection and Classification Using AI

## 目錄

1. [專案簡介](#專案簡介)
2. [專案目標](#專案目標)
3. [晶圓異常類型](#晶圓異常類型)
4. [模型選擇與比較](#模型選擇與比較)
5. [模型結果分析](#模型結果分析)
6. [未來發展與改進](#未來發展與改進)

## 專案簡介

晶圓製造是現代半導體製程中的核心環節，晶圓的品質直接影響最終產品的良率。然而，由於製造過程中的多變性和複雜性，晶圓上常常會出現各種異常，這些異常可能導致嚴重的產品損壞或生產效率下降。為了提高良率，異常的早期識別和分類變得至關重要。

本專案通過分析來自晶圓圖像的異常模式，運用多種機器學習與深度學習技術（如CNN、SVM、隨機森林等），來自動識別並分類晶圓上的異常，從而提升晶圓製造過程的穩定性與品質管理效率。

## 專案目標

本專案旨在構建一個高效的晶圓異常自動辨識系統，具體目標包括：

- **自動化異常檢測**：利用圖像處理技術從晶圓圖像中提取特徵，並使用機器學習算法自動識別異常。
- **異常分類**：針對晶圓上不同的異常類型進行精確的分類，協助製程優化。
- **模型優化**：透過不同的模型進行比較，挑選出最佳的異常識別算法。
- **提升生產良率**：減少人工檢測時間與錯誤，從而提高製造過程的穩定性與生產良率。

## 晶圓異常類型

在半導體製造中，晶圓異常種類繁多，以下是一些常見的晶圓異常類型：

![image](https://hackmd.io/_uploads/SJlAG0HTR.png)

1. **中心點缺陷**：晶圓中心出現明顯的缺陷，通常由於製造設備的問題所導致。
2. **環形缺陷**：晶圓邊緣形成一個環狀缺陷，這種缺陷可能來自於光刻過程中的問題。
3. **不規則塊狀缺陷**：在晶圓表面上不規則分佈的塊狀缺陷，通常與污染有關。
4. **晶圓碎裂**：晶圓在製造過程中破裂，可能是由機械衝擊或設備錯誤引起的。
5. **噪點型缺陷**：在晶圓表面散布小的噪點，可能與清洗不徹底或微粒污染有關。

這些異常的快速、準確分類對於製程優化與設備維護至關重要。

![image](https://hackmd.io/_uploads/HJlBpfRSTR.png)
![image](https://hackmd.io/_uploads/rydTGRSTR.png)

## 模型選擇與比較

在本專案中，選擇了多種機器學習和深度學習模型進行異常識別與分類，具體包括：

1. **卷積神經網絡（CNN）**：
   - CNN 特別適合處理圖像數據，其通過自動提取圖像特徵，能夠精確識別晶圓上的異常模式。
   - 優點：高準確率，擅長複雜模式的識別。
   - 缺點：需要較大的計算資源和訓練數據。

![image](https://hackmd.io/_uploads/SJX9xCSp0.png)

2. **支持向量機（SVM）**：
   - SVM 是一種有效的二元分類器，通過使用核函數可以應用於高維度圖像特徵分類。
   - 優點：對於小樣本有較好的表現。
   - 缺點：在面對多類分類時表現較弱，且對於大數據集的處理速度較慢。

3. **隨機森林（Random Forest）**：
   - 隨機森林使用多棵決策樹進行分類，能有效處理異常檢測的多樣性。
   - 優點：對於小數據集非常穩定，具有良好的泛化能力。
   - 缺點：對於高維數據（如圖像）處理速度較慢。

4. **決策樹（Decision Tree）**：
   - 決策樹通過逐層劃分特徵空間，能夠進行異常的快速分類。
   - 優點：易於解釋，模型訓練時間短。
   - 缺點：容易過擬合，泛化能力較差。

5. **K-Means 分群**：
   - 雖然 K-Means 主要用於無監督學習，但它可以用來對異常進行分群探索，從而幫助發現潛在的異常模式。
   - 優點：快速，易於實現。
   - 缺點：無法進行有監督分類，適用性有限。

6. **最近鄰居演算法（KNN）**：
   - KNN 是一種基於距離的分類算法，在晶圓異常辨識中可以用來檢測異常的鄰近類型。
   - 優點：易於實現，無需模型訓練。
   - 缺點：對於大數據集效率較低，且對噪音敏感。

## 模型結果分析

| Model                | Accuracy | F1 Score | Recall  |
|----------------------|----------|----------|---------|
| CNN                  | 0.885490      | 0.879677     | 0.885490    |
| SVM                  | 0.855914      | 0.832916     | 0.855914    |
| Random Forest        | 0.896335      | 0.886859     | 0.896335    |
| Decision Tree        | 0.852895      | 0.852168     | 0.852895    |
| K-Nearest Neighbors  | 0.811094      | 0.757195     | 0.811094    |

### 模型分析

1. **CNN**：在所有模型中表現最佳，尤其適合處理圖像數據並進行高精度的異常分類，但其訓練時間和計算資源需求較高。
2. **SVM**：在處理多類異常分類時，表現稍微遜色於 CNN，但仍然有不錯的準確度，尤其在小樣本下表現優異。
3. **隨機森林與決策樹**：這兩個樹模型的表現相對穩定，隨機森林能有效降低過擬合，但在大規模圖像數據下性能有限。
4. **KNN**：KNN 的表現適中，適合用於鄰近類型的異常檢測，但對於數據量較大的情況效率較低。

## 未來發展與改進

1. **擴展數據集**：為了進一步提升模型的準確度與泛化能力，未來應該擴展更大、更豐富的異常數據集，涵蓋更多的異常類型與晶圓製程情境。
   
2. **更複雜模型與強化學習**：可嘗試使用更複雜模型或強化學習技術，讓模型在動態製程中學習異常檢測，實現更精確的異常分類與預測。

3. **異常分群與預測**：除了分類，未來的發展可結合無監督學習（如分群）來自動發現新型異常，並進一步使用預測模型進行早期預警。

4. **整合製程參數**：將晶圓製程中的關鍵參數（如溫度、壓力等）與異常辨識結果結合，進行多維度分析，從而幫助工程師進一步優化製程。

5. **部署與自動化**：最終目標是將晶圓異常檢測系統部署於生產線上，實現實時檢測與即時異常響應，進一步提升製造效率與良率。

## 結論

本專案通過使用多種機器學習與深度學習模型進行晶圓異常辨識，展示了不同模型在異常分類中的優劣。未來的發展將聚焦於數據集擴展、模型優化與自動化部署，以進一步提升晶圓製造過程中的異常檢測能力，從而促進半導體產業的技術升級與創新。
