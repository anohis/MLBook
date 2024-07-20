---
title: 神經網路 (Neural Network)
tags: [coursera, ML]

---

## 前向傳播 (Forward Bropagation)

$z^{[1]} = w^{[1]}x+b^{[1]}$
$a^{[1]} = g(z^{[1]})$
$z^{[2]} = w^{[2]}a^{[1]}+b^{[2]}$
$a^{[2]} = g(z^{[2]})$ 
$\hat{y} = a^{[2]}$

## 梯度下降 (Gradient Descent)
根據連鎖法則逐步計算梯度。

假設 $J$ 是邏輯回歸的成本函數，$g$ 是 sigmoid

$J(\hat{y}, y) = -y\log(\hat{y})-(1-y)\log(1-\hat{y})$
$g(z) = \cfrac{1}{1+e^{-z}}$

則

$\cfrac{dJ}{d\hat{y}} = -\cfrac{y}{\hat{y}}+\cfrac{1-y}{1-\hat{y}}$

$\cfrac{d\hat{y}}{da^{[2]}} = 1$

$\cfrac{da^{[2]}}{dz^{[2]}} = a^{[2]}(1-a^{[2]})$

$\cfrac{dz^{[2]}}{dw^{[2]}} = a^{[1]}$

$\cfrac{dz^{[2]}}{db^{[2]}} = 1$

$\cfrac{dz^{[2]}}{da^{[1]}} = w^{[2]}$

$\cfrac{da^{[1]}}{dz^{[1]}} = a^{[1]}(1-a^{[1]})$

$\cfrac{dz^{[1]}}{dw^{[1]}} = x$

$\cfrac{dz^{[1]}}{db^{[1]}} = 1$

總結來看

![image](https://hackmd.io/_uploads/BkevPyZO0.png)

## 權重初始化

權重初始化對神經網路訓練的影響舉足輕重。

[權重初始化](https://hackmd.io/@anohis/S1YKbdfOA)

## 激活函式 (Activation)

讓神經網路成為非線性的關鍵。

不能使用線性的激活函式，這會使神經網路也是線性的。

[激活函式](https://hackmd.io/@anohis/r1yYKCku0)

## 為甚麼要深度

基本上不管是深度還是淺層的神經網路都能解決相同問題。
但是
* 深度神經網路可以分層學習不同層次的特徵
    * 例如人臉辨識，可劃分不同層次為邊緣 > 形狀 > 五官 > 臉
* 有更多的參數，更容易擬合複雜模型

## 正則化 (Regularization)

可以更有效避免overfit。

[正則化](https://hackmd.io/@anohis/H16Y0QB_C)