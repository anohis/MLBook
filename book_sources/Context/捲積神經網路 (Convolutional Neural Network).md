---
title: 捲積神經網路 (Convolutional Neural Network)
tags: [ML]

---

## 捲積

圖片與捲積核 (kernel)，或稱濾波器 (filter)，進行互相關 (cross-correlation) 運算。

![image](https://hackmd.io/_uploads/r140eovuR.png)

## 邊緣

使用特定捲積核可以檢測出邊緣。

#### 正邊緣、負邊緣

![image](https://hackmd.io/_uploads/rkNr-ivOA.png)

#### 水平、垂直

![image](https://hackmd.io/_uploads/BkjfGoDOA.png)

#### 帶權重

如果讓捲積核有不同權重，會有不同效果。

![image](https://hackmd.io/_uploads/HktqfoD_0.png)

不同問題適合不同的權重
但比起手工選擇捲積核權重，讓模型自動學習比較好。

## Padding

對於邊緣的像素來說，捲積的計算次數明顯比中央的像素少，表示邊緣的資訊容易被忽略。

此外，每次捲積後的輸出都會比原始圖片小，限制了卷積次數。

基於上面兩點，可以考慮每次捲積前填充圖片邊緣。

![image](https://hackmd.io/_uploads/HkZBIsD_A.png)

### 有效捲積 (Valid convolution)

不填充圖片，因此輸出大小為

$$(n, n)*(f, f) \rightarrow (n-f+1, n-f+1)$$

### 相同捲積 (Same convolution)

捲積前先填充，讓輸出大小保持原始。

$$(n, n) \rightarrow (n+p, n+p)*(f, f) \rightarrow (n, n)$$

其中

$$p=\cfrac{f-1}{2}$$

## 跨步捲積 (Strided convolution)

捲積的跨步 (stride) 是可以設定的。

![image](https://hackmd.io/_uploads/BkCd1xO_0.png)

假設原始圖片 $(n,n)$ 經過pad $p$，且捲積核大小為 $(f,f)$，跨步 $stride=2$  
那最後會得到

$$(\cfrac{n+2p-f}{stride}, \cfrac{n+2p-f}{stride})$$