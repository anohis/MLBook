---
title: Softmax regression
tags: [ML]

---

## Softmax regression

Softmax regression可以用在多類別分類。  
模型輸出表示屬於各分類的機率，機率加總應為 $1$。

![image](https://hackmd.io/_uploads/SJdjTeUdC.png)

實現輸出機率的關鍵是softmax層

$$softmax(\mathbf {z} )_{j}={\frac {e^{z_{j}}}{\sum _{c=1}^{C}e^{z_{c}}}}$$

### Loss function

$$Loss(\hat{y}, y) = -\sum y_j\log{\hat{y}_j}$$

$$\cfrac{dJ}{dz}=\hat{y}-y$$

### 實作

在實作上，將最後一層的激活設定成softmax。

```python=0
model = Sequential(
    [
        Input((2, )),
        Dense(2, activation = "relu"),
        Dense(4, activation = "softmax"),
    ])

model.compile(loss = SparseCategoricalCrossentropy(),
             optimizer = Adam(0.01))

model.fit(x, y, epochs = 200)
```

但基於誤差等理由，在訓練的時候，會傾向將最後一層的sofmax改成線性激活函式，反過來在損失函式加上參數 from_logits = True。

```python=0
model = Sequential(
    [
        Input((2, )),
        Dense(2, activation = "relu"),
        Dense(4, activation = "linear"),
    ])

model.compile(loss = SparseCategoricalCrossentropy(from_logits = True),
             optimizer = Adam(0.01))

model.fit(x, y, epochs = 200)
```