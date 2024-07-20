---
title: 密度估計 (Density estimation)
tags: [coursera, ML]

---

## Density estimation
根據分布，來計算資料異常的可能性。

![image](https://hackmd.io/_uploads/BJVKbcXPC.png)

一般會使用高斯分佈。
每特徵會建立專屬的高斯模型，再把每個特徵異常的可能性相乘得到異常可能性。

![image](https://hackmd.io/_uploads/SyABH97w0.png)

![image](https://hackmd.io/_uploads/H1vBPqXvR.png)

#### 驗證
實際上資料有標記正常/異常，但訓練的時候只會拿正常的資料訓練。
測時時，會將實際結果和預測結果做比對。

![image](https://hackmd.io/_uploads/S17HYqXDC.png)

如果異常資料很少，建議是將測試集和驗證集合併使用。
缺點是沒有公正的測試集可以參考。

![image](https://hackmd.io/_uploads/HyMXAc7D0.png)

由於異常資料可能很少，所以建議使用混淆矩陣評估。

#### 與監督學習差異
* 異常檢測
    * 當資料嚴重偏差時，且異常原因可能相距甚遠
* 監督學習
    * 當資料充足，且異常原因基本相似

#### 特徵選擇
* 非高斯分佈特徵
嘗試轉換成高斯分佈。

![image](https://hackmd.io/_uploads/HkfIMoQvC.png)

* 無法區分異常
當現有特徵無法明確判別出異常時，會需要新增特徵來判別。
可能是新的特徵，或是舊的特徵組合。