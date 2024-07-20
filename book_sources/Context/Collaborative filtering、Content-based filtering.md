---
title: Collaborative filtering、Content-based filtering
tags: [coursera, ML]

---

## 電影推薦
每個使用者都會對電影打分數(不見得每部都會)。
每部電影都有特徵。
替每個使用者建立一個線性回歸模型，預測不同的電影特徵的評價。

![image](https://hackmd.io/_uploads/Sk1lZhXDR.png)
![image](https://hackmd.io/_uploads/HJ8Me3XPR.png)
![image](https://hackmd.io/_uploads/HkTuln7P0.png)

## Collaborative filtering algorithm
現實是，不見得有電影特徵。
假設，我們已經得知所有使用者的模型，那就可以推導出電影特徵。

![image](https://hackmd.io/_uploads/SkClX27PC.png)
![image](https://hackmd.io/_uploads/S183m3XwR.png)

但現實是，不管是使用者模型或是電影特徵我們都不知道。
因此會將兩個目標同時訓練。

![image](https://hackmd.io/_uploads/HyPvrhQDR.png)

![image](https://hackmd.io/_uploads/BkCfLh7D0.png)

最後，可以從多個使用者的資料推論特徵，反過來又可以預測其他用戶的評分。

#### 二進制標籤
Collaborative filtering同樣的也適用於二進制標籤，不限於打分數。
二進制標籤以0/1表示，0是否定、1是肯定，此外還有可能是未知。
例如: 使用者是否點擊過商品，0: 沒有，1: 有，?: 還沒看到商品。

![image](https://hackmd.io/_uploads/SytOOh7P0.png)

由於問題變成0/1所以原先線性回歸的部分會以邏輯回歸取代。

![image](https://hackmd.io/_uploads/ByKAdnmvR.png)

同時，成本函數也變成BinaryCrossEntropy。

![image](https://hackmd.io/_uploads/HJuFt3QvC.png)

## 均值歸一化
對於全新用戶而言，由於沒有任何評分，演算法會傾向把w、b降到0(因為有regularization)。
這會導致估計新用戶的評分通通都是0。

因此使用Mean Normalization來避免上述問題。
最後新用戶的預估評分將會是平均值而不是0。

![image](https://hackmd.io/_uploads/SkVzp37DC.png)


## 實現
tensorflow有自動計算梯度的功能GradientTape。

![image](https://hackmd.io/_uploads/ryXxbpQv0.png)

#### 尋找相關物品
有時候訓練完成後得到的特徵很難解釋。
因此如果要找相似的物品，可以直接用彼此特徵的距離來評估。

#### 侷限
* 不擅長冷啟動問題
    * 新項目、新使用者等等
* 沒辦法很好利用已知訊息
    * 電影導演、演員等
    * 使用者性別、年齡等

## Content-based filtering
Content-based filtering可以解決Collaborative filtering無法利用已知訊息的限制。
Content-based主要是解決使用者和項目的特徵匹配。

![image](https://hackmd.io/_uploads/BJpwG1BvR.png)

在Collaborative filtering中，預設評分是用兩個向量乘積計算。
這兩個向量是直接透過分數學習得到的，因此，要求商品特徵數量和使用者權重數量一致(才可以乘積)。
例如
電影特徵有10個標籤，使用者就只能有對應的10個權重計算(計算上完全不會使用使用者特徵)

而在Content-based，預設評分一樣是用兩個向量乘積計算。
但兩個向量分別是透過以知的特徵學習，僅要求求得的向量長度一致，特徵數量可以不同。
例如
電影有10個標籤、年分、演員等20個特徵，使用者有7個特徵。
分別從電影20個特徵中學習10個特徵向量，以及從使用者7個特徵中學習10個特徵向量。

![image](https://hackmd.io/_uploads/rkImLJHPR.png)

![image](https://hackmd.io/_uploads/BkBO2kSv0.png)

#### 大型推薦系統
如果每次推薦都要計算所有的商品，當商品數量很巨大的時候會變得不可行。
因此，一般會透過兩個步驟來解決
* 檢索
    * 這個國家的排行榜
    * 與過去看過的項目類似的商品，等
* 排名
    * 照模型預測的喜歡程度排名

需要平衡檢索數量與推薦的成效。
一般來說，檢索數量越少，推薦清單更容易塞滿不感興趣的項目。
但檢索數量越多，執行速度就越慢。

## 實作

![image](https://hackmd.io/_uploads/HkGq5pOvR.png)
