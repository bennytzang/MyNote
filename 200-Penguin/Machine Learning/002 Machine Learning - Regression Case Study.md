[2_Regression Case Study](https://sakura-gh.github.io/ML-notes/ML-notes-html/2_Regression-Case-Study.html)
# 案例研究
### 問題的導入：預測寶可夢的CP值
  - Estimating the Combat Power(CP) of a pokemon after evolution
  
   - ### 確定Senario、Task和Model
	   - #### Senario
    首先根據已有的data來確定Senario，我們擁有寶可夢進化前後cp值的這樣一筆資料，input是進化前的寶可夢(包括它的各種屬性)，output是進化後的寶可夢的cp值；因此我們的data是labeled，使用的Senario是Supervised Learning
    	- ##### Task
    然後根據我們想要function的輸出類型來確定Task，我們預期得到的是寶可夢進化後的cp值，是一個scalar，因此使用的Task是
    ==Regression==
   		- #####  Model
    關於Model，選擇很多，這裡採用的是==Non-linear Model==
	![](photo/Machine%20Learning/regularization/Pasted%20image%203.png)
	![](Model.png)
	
 ### Regression的具體過程
- 回顧一下machine Learning的三個步驟：
	1. 定義一個model即function set
	2. 定義一個goodness of function損失函數去評估該function的好壞
	3. 找一個最好的function
	
## Step1：Model (function set)
-	如何選擇一個function的模型呢？畢竟只有確定了模型才能調參。==這裡沒有明確的思路，只能憑經驗去一種種地試==
-	#### Linear Model 線性模型:
![](photo/Machine%20Learning/regularization/Pasted%20image%201.png)
y代表進化後的cp值，X_cp代表進化前的cp值，w和b代表未知參數，可以是任何數值根據不同的W和b，可以確定不同的無窮無盡的function，而![](photo/Machine%20Learning/regularization/Pasted%20image%201.png)這個抽象出來的式子就叫做model，是以上這些具體化的function的集合，即functionset。
實際上這是一種 ``Linear Model``但只考慮了寶可夢進化前的cp值，因而我們可以將其擴展為：
![](photo/Machine%20Learning/regularization/Pasted%20image%202.png)
![](photo/Machine%20Learning/regularization/Pasted%20image%204.png)
 ![](Step1_Model.png)
## Step2：Goodness of Function
![](Pasted%20image%2010.png)
![](Pasted%20image%2011.png)
 ## Lose function 損失函數:  [output = how bad it is]
- 為了衡量function set中的某個function的好壞，我們需要一個評估函數，即
Loss function，損失函數:其==代表為此函數與正確值的誤差大小==。
![](%E6%93%B7%E5%8F%96.png)
之前提到的model是由我們自主選擇的，這裡的loss function也是，最常用的方法就是採用類似於==方差和==的形式來衡量參數的好壞，即預測值與真值差的平方和；這裡真正的數值減估測數值的平方，叫做估測誤差，Estimation error，將10個估測誤差合起來就是loss function
![](photo/Machine%20Learning/regularization/Pasted%20image%205.png)
![](Pasted%20image%206.png)

[2_Regression Case Study](https://sakura-gh.github.io/ML-notes/ML-notes-html/2_Regression-Case-Study.html)
- ## Loss function視覺化-
	- 下圖中是loss function的視覺化，該圖中的每一個點都代表一組`(w,b)`
 ，也就是對應著一個`function`，而該點的顏色對應著的loss function的結果`L(w,b)`，==它表示該點對應function的表現有多糟糕==，顏色越==偏紅色==代表==Loss的數值越大==，這個function的==表現越不好==，越==偏藍色==代表==Loss的數值越小==，這個function的==表現越好==
	 - 比如圖中用紅色箭頭標注的點就代表了b=-180 , w=-2對應的function，即
	![](Pasted%20image%208.png)
    該點所在的顏色偏向於紅色區域，因此這個function的loss比較大，表現並不好
	![](Pasted%20image%209.png)
## Step3：Pick the Best Function
- 我們已經確定了loss function，他可以衡量我們的model裡面每一個function的好壞，接下來我們要做的事情就是，從這個function set裡面，挑選一個最好的function。

- 挑選最好的function這一件事情，寫成formulation/equation的樣子如下：
 ![](Pasted%20image%2012.png)
 ![](Pasted%20image%2013.png)
 - 利用線性代數的知識，可以解得這個closed-form solution，但這裡採用的是一種更為普遍的方法——==gradient descent(梯度下降法)==
# Gradient Descent 梯度下降
[Gradient Descent 梯度下降](Gradient%20Descent%20%E6%A2%AF%E5%BA%A6%E4%B8%8B%E9%99%8D)

# 回到pokemon的問題上來
- 偏微分的計算
- 現在我們來求具體的L對w和b的偏微分
 ![](Pasted%20image%2026.png)
## How's the results?
- 根據gradient descent，我們得到的
![](Pasted%20image%2027.png)
中最好的參數是b=-188.4, w=2.7
- 我們需要有一套評估系統來評價我們得到的最後這個function和實際值的誤差error的大小；這裡我們將training data裡每一隻寶可夢`i`進化後的實際cp值與預測值之差的絕對值叫做`e^i`，而這些誤差之和Average Error on Training Data為
 ![](Pasted%20image%2028.png)
 ``What we really care about is the error on new data (testing data)``
 - 當然我們真正關心的是generalization的case，也就是用這個model去估測新抓到的pokemon，誤差會有多少，這也就是所謂的testing data的誤差；於是又抓了10只新的pokemon，算出來的Average Error on Testing Data為
 ![](Pasted%20image%2029.png)
 可見training data裡得到的誤差一般是要比testing data要小，這也符合常識
 ![](Pasted%20image%2030.png)
 ## How can we do better?
 我們有沒有辦法做得更好呢？這時就需要我們重新去設計model；如果仔細觀察一下上圖的data，就會發現在原先的cp值比較大和比較小的地方，預測值是相當不准的

實際上，從結果來看，最終的function可能不是一條直線，可能是稍微更複雜一點的曲線

![](Pasted%20image%2031.png)
X^2
---
![](Pasted%20image%2032.png)
X^3
---
![](Pasted%20image%2033.png)
X^4
---
![](Pasted%20image%2034.png)
X^5
---
5個model的對比
這5個model的training data的表現：隨著`X`的高次項的增加，對應的average error會不斷地減小；實際上這件事情非常容易解釋，實際上低次的式子是高次的式子的特殊情況(令``高次項對應的為0``，高次式就轉化成低次式)

也就是說，在gradient descent可以找到best function的前提下(多次式為Non-linear model，存在local optimal局部最優解，gradient descent不一定能找到global minima)，function所包含的項的次數越高，越複雜，error在training data上的表現就會越來越小；但是，我們關心的不是model在training data上的error表現，而是model在testing data上的error表現
![](Pasted%20image%2035.png)
在training data上，model越複雜，error就會越低；但是在testing data上，model複雜到一定程度之後，error非但不會減小，反而會暴增，在該例中，從含有``X^4``項的model開始往後的model，==testing data上的error出現了大幅增長的現象==，通常被稱為==overfitting過擬合==
![](Pasted%20image%2036.png)
因此model不是越複雜越好，而是選擇一個最適合的model，在本例中，包含``X^3``的式子是最適合的model

## 進一步討論其他參數
- 之前我們的model只考慮了寶可夢進化前的cp值，這顯然是不對的，除了cp值外，還受到物種的影響
![](Pasted%20image%2037.png)
因此我們重新設計model：
![](Pasted%20image%2038.png)
也就是根據不同的物種，設計不同的linear model(這裡``Xs = species of X``)，那如何將上面的四個if語句合併成一個linear model呢？
![](Pasted%20image%2039.png)
![](Pasted%20image%2040.png)
- 有了上面這個model以後，我們分別得到了在training data和testing data上測試的結果：
![](Pasted%20image%2041.png)
- 考慮所有可能有影響的參數，設計出這個最複雜的model：
![](Pasted%20image%2042.png)
算出的training error=1.9，==但是，testing error=102.3==！==這麼複雜的model很大概率會發生overfitting==(按照我的理解，overfitting實際上是我們==多使用了一些input的變數或是變數的高次項使曲線跟training data擬合的更好==，但不幸的是==這些項並不是實際情況下被使用的==，於是這個==model在testing data上會表現得很糟糕==)，overfitting就相當於是那個範圍更大的韋恩圖，它==包含了更多的函數更大的範圍，代價就是在準確度上表現得更糟糕==
## regularization解決overfitting
### (L2正則化解決過擬合問題)
- regularization可以使曲線變得更加smooth，training data上的error變大，但是 testing data上的error變小。有關regularization的具體原理說明詳見下一部分
- ## [regularization](regularization)

## conclusion:
- 關於pokemon的cp值預測的流程總結：
	- 根據已有的data特點(labeled data，包含寶可夢及進化後的cp值)，確定使用supervised learning監督學習

	- 根據output的特點(輸出的是scalar數值)，確定使用regression回歸(linear or non-linear)

	- 考慮包括進化前cp值、species、hp等各方面變數屬性以及高次項的影響，我們的model可以採用這些input的一次項和二次型之和的形式，如：
	![](Pasted%20image%2052.png)
	而為了保證function的平滑性，loss function應使用regularization，即
	![](Pasted%20image%2053.png)
	注意bias——參數b對function平滑性無影響，因此不額外再次計入loss function(y的運算式裡已包含w、b)

- 利用[Gradient Descent 梯度下降](Gradient%20Descent%20%E6%A2%AF%E5%BA%A6%E4%B8%8B%E9%99%8D)對[regularization](regularization)版本的loss function進行梯度下降反覆運算處理，每次反覆運算都減去L對該參數的微分與learning rate之積，假設所有參數合成一個vector：![](Pasted%20image%2054.png)那麼每次梯度下降的運算式如下：
![](Pasted%20image%2055.png)
![](Pasted%20image%2056.png)
![](Pasted%20image%2057.png)
