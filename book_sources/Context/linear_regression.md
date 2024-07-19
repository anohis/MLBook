## 線性回歸 (Linear regression)

主要用在回歸問題。

## 數學模型
$$ f_{w,b}(x^{(i)}) = wx^{(i)} + b$$

## 成本函數
  $$J(w,b) = \frac{1}{2m} \sum\limits_{i = 0}^{m-1} (f_{w,b}(x^{(i)}) - y^{(i)})^2$$ 
 
其中 
  $$f_{w,b}(x^{(i)}) = wx^{(i)} + b$$
  
- $f_{w,b}(x^{(i)})$ 是使用 $w,b$ 預測第 $i$ 比資料的結果  
- $(f_{w,b}(x^{(i)}) -y^{(i)})^2$ 是和真實結果的方差   
- 基於計算方便使用 `2m` 計算 $J(w,b)$.

## 梯度下降
$$\begin{align*} \text{repeat}&\text{ until convergence:} \; \lbrace \newline
\;  w &= w -  \alpha \frac{\partial J(w,b)}{\partial w}  \; \newline 
 b &= b -  \alpha \frac{\partial J(w,b)}{\partial b}  \newline \rbrace
\end{align*}$$

其中， $w$, $b$ 是同步更新的。

梯度計算方式是

$$
\begin{align}
\frac{\partial J(w,b)}{\partial w}  &= \frac{1}{m} \sum\limits_{i = 0}^{m-1} (f_{w,b}(x^{(i)}) - y^{(i)})x^{(i)} \\
  \frac{\partial J(w,b)}{\partial b}  &= \frac{1}{m} \sum\limits_{i = 0}^{m-1} (f_{w,b}(x^{(i)}) - y^{(i)}) \\
\end{align}
$$