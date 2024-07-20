---
title: Deep Q Network
tags: [coursera, ML]

---

## 馬可夫決策過程
現在的狀態是過去的狀態累積的。

## 貝爾曼方程
![image](https://hackmd.io/_uploads/B1CBieYw0.png)

#### 隨機環境
如果環境是隨機的，那每次相同行為的回報也會不同。
因此決策過程不再是單純以最大值計算，而是要計算期望值。

![image](https://hackmd.io/_uploads/S13opeKw0.png)

## Deep Q Network

![image](https://hackmd.io/_uploads/BklAX8ZYwA.png)

![image](https://hackmd.io/_uploads/B1clcZtvC.png)

![image](https://hackmd.io/_uploads/ryTW2WKv0.png)

#### epsilon-greedy

![image](https://hackmd.io/_uploads/ryUiCWtwA.png)

## Mini-batch
[Mini-batch](https://hackmd.io/@anohis/SJN5aYmu0)

![image](https://hackmd.io/_uploads/ByxwbGYDA.png)


## Soft update
由於mini-batch使用的樣本數較少，使得梯度下降不穩，甚至產生更糟的神經網路(甚至不一定是因為mini-batch導致的)。
因此不會直接將新的網路覆蓋，而是採用軟更新的方式，新舊權重將會以一個比例融合。

![image](https://hackmd.io/_uploads/r1dSXzFD0.png)

## 強化學習的限制
* 在模擬環境比現實容易太多
* 強化學習的應用跟監督和無監督相比太少

## 目標網路
當只有一個神經網路訓練Q的時候會變得極度不穩定。
原因是因為誤差計算中，w每次迭代都會被更新。
$$
\overbrace{\underbrace{R + \gamma \max_{a'}Q(s',a'; w)}_{\rm {y~target}} - Q(s,a;w)}^{\rm {Error}}
$$

所以新增一個目標網路$w^-$來避免頻繁更動。
目標網路和Q網路會是相同結構。
$$
\overbrace{\underbrace{R + \gamma \max_{a'}\hat{Q}(s',a'; w^-)}_{\rm {y~target}} - Q(s,a;w)}^{\rm {Error}}
$$

每隔一段時間後，目標網路將會執行軟更新。
$$
w^-\leftarrow \tau w + (1 - \tau) w^-
$$

## 經驗回放
由於在代理與環境交互的過程產生的狀態、行為、獎勵都是連續的。
如果使用這些連續經驗中學習可能會造成一些問題。
因此將蒐集到的經驗儲存到緩衝中，再從緩衝抽樣經驗進行訓練。