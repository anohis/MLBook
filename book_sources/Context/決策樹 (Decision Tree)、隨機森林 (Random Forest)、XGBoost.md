---
title: 決策樹 (Decision Tree)、隨機森林 (Random Forest)、XGBoost
tags: [coursera, ML]

---

## 決策樹 (Decision Tree)
* 如何選擇特徵
    * 分類出來的兩邊擁有最大純度(purity)
* 何時停止
    * 節點只擁有一個類別
    * 樹已經到最大深度
    * 節點純度已到達閾值
    * 節點數量小於閾值

![image](https://hackmd.io/_uploads/Bkh5uNZDR.png)

![image](https://hackmd.io/_uploads/rkeJiYVWD0.png)

## Entropy
可以使用Entropy來測量不純度(impurity)。
當$p=0.5$時擁有最大的Entropy，表示這個群體有一半的+與一半的-。
反之，當一個全體都是+或-，$p=0$，此時Entropy最小。

![image](https://hackmd.io/_uploads/HJn16NWP0.png)

## 訊息增益(Information gain)
![image](https://hackmd.io/_uploads/B1c1-UbDA.png)

![image](https://hackmd.io/_uploads/BklBk8-D0.png)

要選擇使用哪個特徵時，個別計算訊息增益，選擇訊息增益最大的方案。

之所以要加權是為了辨別節點大小，在數量多的節點上擁有小的Entropy比數量少的來的重要。

當訊息增益過小時，表示分支意義不大，反而有可能導致overfit。

## 離散特徵
離散特徵採用one hot方式編碼。

#### 實現
Pandas提供一個方法get_dummies，可以將資料改用one-hot方式儲存。
```python=0
import pandas as pd

df = pd.get_dummies(data = df,
                         prefix = cat_variables,
                         columns = cat_variables)
```

## 連續特徵
遇到連續特徵時，通常會從訓練資料中挑選值來計算訊息增益。

## 回歸樹
選擇特徵的方式改以計算權重方差。

![image](https://hackmd.io/_uploads/ryDzdNfv0.png)

#### 實現
```python=0
from sklearn.tree import DecisionTreeClassifier

model = DecisionTreeClassifier()
model.fit(xTrain,y_train) 
pred = model.predict(xTest)
```

DecisionTreeClassifier有兩個參數
* min_samples_split: 可以分支的最小樣本數
* max_depth: 樹的最深度

提高min_samples_split、降低max_depth都有助於改善overfit。

## 群集
由於單一決策樹對資料很敏感，訓練資料稍有不同可能導致建構出完全不一樣的樹。
因此應當建立決策樹群集，預測資料將是每個樹投票的結果。

## 替換採樣 (Sampling with replacement)
每次採樣後會將選擇的丟回候選中。

![image](https://hackmd.io/_uploads/rJUDQSMDR.png)

## 隨機森林 (XGBoost)
透過替換採樣創建n個樹，n個樹的投票結果就是預測結果。
通常n不會超過100。

很多時候，n個樹中有部分會是很相似的，為了避免過於相似，會限制可選擇的特徵。
例如，有m個特徵可以使用，但會限制只能從其中k個選擇。
通常，$k=\root \of {m}$。

#### 實現
```python=0
from sklearn.ensemble import RandomForestClassifier

model = RandomForestClassifier()
model.fit(xTrain,y_train) 
pred = model.predict(xTest)
```

RandomForestClassifier有三個參數
* min_samples_split: 可以分支的最小樣本數
* max_depth: 樹的最深度
* n_estimators: 有多少顆樹

## XGBoost (eXtreme Gradient Boosting)
類似隨機森林，但挑選的資料會更集中在表現不佳的資料中。
每次建構一顆樹後，會檢查所有資料中哪些是預測錯誤的。
並且之後有更大的機率把那些資料挑選出來訓練。

#### 實現
```python=0
# 分類
from xgboost import XGBClassifier

model = XGBClassifier()
model.fit(xTrain, yTrain)
pred = model.predict(xTest)
```

```python=0
# 回歸
from xgboost import XGBRegressor

model = XGBRegressor()
model.fit(xTrain, yTrain)
pred = model.predict(xTest)
```

## 總結
* 決策樹
    * 對表格類(結構化)的資料表現很好
    * 不推薦用在非結構化的資料，例如圖片、音樂、文字
    * 訓練很快
* 神經網路
    * 對所有資料類型表現都好
    * 訓練比較慢
    * 遷移學習
    * 更適合多個模型協同系統，可以使用梯度下降統一訓練