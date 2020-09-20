# Gradient Descent的作法
-	上面的例子比較簡單，用線性代數的知識就可以解；但是對於更普遍的問題來說，gradient descent的厲害之處在於，只要`L(f)`是可微分的，gradient descent都可以拿來處理這個`f`，找到表現比較好的parameters
---
### 單個參數的問題
![](Pasted%20image%2016.png)
![](Pasted%20image%2018.png)
![](Pasted%20image%2019.png)
![](Pasted%20image%2020.png)
---

### 兩個參數的問題
![](Pasted%20image%2021.png)
![](Pasted%20image%2022.png)
![](Pasted%20image%2023.png)

	注：這裡兩個方向的η(learning rate)必須保持一致，這樣每次更新座標的step size是等比例縮放的，保證座標前進的方向始終和梯度下降的方向一致；否則座標前進的方向將會發生偏移		
---
# Gradient Descent的缺點
- gradient descent有一個令人擔心的地方，也就是我之前一直提到的，它每次反覆運算完畢，尋找到的梯度為0的點必然是極小值點，local minima；卻不一定是最小值點，global minima

- 這會造成一個問題是說，如果loss function長得比較坑坑窪窪(極小值點比較多)，而每次初始化![](Pasted%20image%2024.png)的取值又是隨機的，這會造成每次gradient descent停下來的位置都可能是不同的極小值點；而且當遇到梯度比較平緩(gradient≈0)的時候，gradient descent也可能會效率低下甚至可能會stuck卡住；也就是說通過這個方法得到的結果，是看人品的
![](Pasted%20image%2025.png)
 -	但是！在linear regression裡，loss function實際上是convex的，是一個凸函數，是沒有local optimal局部最優解的，他只有一個global minima，visualize出來的圖像就是從裡到外一圈一圈包圍起來的橢圓形的等高線(就像前面的等高線圖)，因此隨便選一個起始點，根據gradient descent最終找出來的，都會是同一組參數。
	
## 回到 [002 Machine Learning - Regression Case Study](002%20Machine%20Learning%20-%20Regression%20Case%20Study.md)