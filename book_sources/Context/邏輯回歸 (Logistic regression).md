---
title: 邏輯回歸 (Logistic regression)
tags: [coursera, ML]

---

## 邏輯回歸 (Logistic regression)
主要用在分類問題。

## 數學模型
跟線性回歸類似，差別在多了一個輸出轉換。

$$ f_{\mathbf{w},b}(\mathbf{x}^{(i)}) = g(\mathbf{w} \cdot \mathbf{x}^{(i)} + b )$$ 

其中，$g(z)$ 稱作 Sigmoid 或 Logistic Function

$$g(z) = \frac{1}{1+e^{-z}}$$

## 成本函數
  $$J(w,b) = \frac{1}{m} \sum\limits_{i = 0}^{m-1} loss(f_{\mathbf{w},b}(\mathbf{x}^{(i)}), y^{(i)}) $$ 
 
其中 $loss$ 是單筆資料的損失

\begin{equation}
  loss(f_{\mathbf{w},b}(\mathbf{x}^{(i)}), y^{(i)}) = \begin{cases}
    - \log\left(f_{\mathbf{w},b}\left( \mathbf{x}^{(i)} \right) \right) & \text{if $y^{(i)}=1$}\\
    - \log \left( 1 - f_{\mathbf{w},b}\left( \mathbf{x}^{(i)} \right) \right) & \text{if $y^{(i)}=0$}
  \end{cases}
\end{equation}


可以簡化計算成
    $$loss(f_{\mathbf{w},b}(\mathbf{x}^{(i)}), y^{(i)}) = (-y^{(i)} \log\left(f_{\mathbf{w},b}\left( \mathbf{x}^{(i)} \right) \right) - \left( 1 - y^{(i)}\right) \log \left( 1 - f_{\mathbf{w},b}\left( \mathbf{x}^{(i)} \right) \right)$$
    
## 梯度下降

邏輯回歸的梯度下降一樣是

$$\begin{align*}
&\text{repeat until convergence:} \; \lbrace \\
&  \; \; \;w_j = w_j -  \alpha \frac{\partial J(\mathbf{w},b)}{\partial w_j}   \; & \text{for j := 0..n-1} \\ 
&  \; \; \;  \; \;b = b -  \alpha \frac{\partial J(\mathbf{w},b)}{\partial b} \\
&\rbrace
\end{align*}$$

其中

$$\begin{align*}
\frac{\partial J(\mathbf{w},b)}{\partial w_j}  &= \frac{1}{m} \sum\limits_{i = 0}^{m-1} (f_{\mathbf{w},b}(\mathbf{x}^{(i)}) - y^{(i)})x_{j}^{(i)}  \\
\frac{\partial J(\mathbf{w},b)}{\partial b}  &= \frac{1}{m} \sum\limits_{i = 0}^{m-1} (f_{\mathbf{w},b}(\mathbf{x}^{(i)}) - y^{(i)})
\end{align*}$$

唯一的差別是

* $f_{\mathbf{w},b}(x) = g(z)$
* $g(z) = \frac{1}{1+e^{-z}}$
* $z = \mathbf{w} \cdot \mathbf{x} + b$  

## 數學解釋

邏輯回歸的數學模型是

$$f_{\mathbf{w},b}(\mathbf{x}^{(i)}) = g(\mathbf{w} \cdot \mathbf{x}^{(i)} + b )$$

其輸出表達的是 ${x}^{(i)}$ 是正樣本的機率

$$f_{\mathbf{w},b}(\mathbf{x}^{(i)}) = p({y}^{(i)}=1 \mid {x}^{(i)}) = \hat{{y}^{(i)}}$$

而負樣本的機率自然是

$$p({y}^{(i)}=0 \mid {x}^{(i)}) = 1 - p({y}^{(i)}=1 \mid {x}^{(i)}) = 1 - \hat{{y}^{(i)}}$$

因此如果想要計算 $x$ 是 $y$ 的機率，可以表示

$$p(y \mid x) = \hat{y}^{y}*(1-\hat{y})^{(1-y)}$$

又因為 $log$ 是絕對單調遞增函數，所以當 $log$ 越大，$p(y \mid x)$ 保證越大

$$\log(p(y \mid x)) = y\log(\hat{y}) + (1 - y)\log(1-\hat{y})$$

因此目標是讓 $\log(p(y \mid x))$ 越大，所以

$$loss(y,\hat{y}) = -log(p(y \mid x))$$

當 $loss$ 越小，$p(y \mid x)$ 就會越大