---
title: K-means
tags: [coursera, ML]

---

## K-means
為了分類k個群。
首先隨機挑選k個位置作為各別群的中心。
再計算所有資料更接近哪個群中心，屬於哪個群。
分類完後重新計算k個群的中心，重複上述步驟值到中心不再變動。

![image](https://hackmd.io/_uploads/r1UGS2GDC.png)

如果初始中心沒有被分配到任何資料，則可以
* 刪除群，也就是變成k-1個群
* 重新亂數中心

通常，刪除群比較常見。

#### 成本函數
計算所有資料和聚類中心的平均距離。

![image](https://hackmd.io/_uploads/S1g_wDmvR.png)


#### 初始化
隨機挑選k筆資料當初始中心開始訓練。
重複上述步驟，挑選其中有最小成本的模型。

#### k的選擇
elbow method: 挑選明顯曲線趨緩的點。
但很多時候曲線是平滑的。
![image](https://hackmd.io/_uploads/r1QlhvmPC.png)

另一種方式是看業務需求決定k。