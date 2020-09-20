## regularization解決overfitting
### (L2正則化解決過擬合問題)
- regularization可以==使曲線變得更加smooth==，==training data上的error變大==，==但是 testing data上的error變小==。有關regularization的具體原理說明詳見下一部分
原來的loss function只考慮了prediction的error，即
![](Pasted%20image%2043.png)
而regularization則是在原來的loss function的基礎上加上了一項
![](Pasted%20image%2044.png)


	注意:	不須加上"b"，bias不會對圓滑度有影響，僅會平移。

-	而regularization則是在原來的loss function的基礎上加上了一項
![](Pasted%20image%2046.png)
就是把這個model裡面所有的的平方和用λ加權(其中i代表遍歷n個training data，j代表遍歷model的每一項)

-	也就是說，我們期待參數`W`越小甚至接近於`0`的`function`，為什麼呢？
-	因為參數值接近0的function，是比較平滑的；所謂的平滑的意思是，當今天的輸入有變化的時候，output對輸入的變化是比較不敏感的

![](Pasted%20image%2048.png)
![](Pasted%20image%2049.png)

	注：這裡的λ需要我們手動去調整以取得最好的值

-	==λ值越大代表考慮smooth的那個regularization那一項的影響力越大==，我們找到的function==就越平滑==

-	觀察下圖可知，當我們的==λ越大的時候==，在==training data上得到的error其實是越大的==，但是這件事情是非常合理的，因為==當λ越大的時候==，我們就==越傾向於考慮w的值而越少考慮error的大小==；但是有趣的是，雖然在training data上得到的error越大，但是==在testing data上得到的error可能會是比較小的==

- 下圖中，當λ從0到100變大的時候，training error不斷變大，testing error反而不斷變小；但是當λ太大的時候(>100)，在testing data上的error就會越來越大

我們==喜歡比較平滑==的function，因為它對noise不那麼sensitive；==但是我們又不喜歡太平滑的function==，

因為它就==失去了對data擬合的能力==

；而function的平滑程度，就需要通過調整λ來決定，就像下圖中，當λ=100時，在testing data上的error最小，因此我們選擇λ=100

注：這裡的error指的是
--- 
### error
![](Pasted%20image%2050.png)
--- 
![](Pasted%20image%2051.png)

---

## Regularization -> redefine the loss function
- 關於overfitting的問題，很大程度上是由於曲線為了更好地擬合training data的資料，而引入了更多的高次項，使得曲線更加“蜿蜒曲折”，反而導致了對testing data的誤差更大

- 回過頭來思考，我們之前衡量model中某個function的好壞所使用的loss function，僅引入了真實值和預測值差值的平方和這一個衡量標準；我們==想要避免overfitting過擬合的問題==，==就要使得高次項對曲線形狀的影響盡可能小==，因此我們要==在loss function裡引入高次項(非線性部分)的衡量標準==，也就是==將高次項的係數也加權放進loss function中==，這樣可以使得訓練出來的model既==滿足預測值和真實值的誤差小==，又滿足高次項的係數盡可能小而使==曲線的形狀比較穩定集中==

- 以下圖為例，如果loss function僅考慮了
![](photo/Machine%20Learning/regularization/Pasted%20image.png)
- 這一誤差衡量標準，那麼擬合出來的曲線就是紅色虛線部分(`overfitting`)，而==overfitting就是所謂的model對training data過度自信==, 非常完美的擬合上了這些資料, 如果具備`overfitting`的能力, 那麼這個方程就可能是一個比較複雜的非線性方程 , 正是因為這裡的`X^3`和`X^2`使得這條虛線能夠被彎來彎去, 所以整個模型就會特別努力地去學習作用在`X^3`和`X^2`上的c、d參數. 但是在這個例子裡，我們期望模型要學到的卻是這條藍色的曲線. 因為它能更有效地概括資料.而且只需要一個`y = a+bx`就能表達出資料的規律。
- 或者是說, 藍色的線最開始時, 和紅色線同樣也有c、d兩個參數, 可是最終學出來時, c 和 d 都學成了0, 雖然藍色方程的誤差要比紅色大, 但是概括起資料來還是藍色好
![](photo/Machine%20Learning/regularization/Pasted%20image%201.png)
- 這也是我們通常採用的方法，我們不可能一開始就否定高次項而直接只採用低次線性運算式的model，因為有時候真實資料的確是符合高次項非線性曲線的分佈的；而==如果一開始直接採用高次非線性運算式的model，就很有可能造成overfitting==，在曲線偏折的地方與真實資料的誤差非常大。我們的目標應該是這樣的：

==在無法確定真實資料分佈的情況下，我們盡可能去改變loss function的評價標準==
- 我們的model的運算式要盡可能的複雜，包含盡可能多的參數和盡可能多的高次非線性項。
- 但是我們的loss function又有能力去控制這條曲線的參數和形狀，使之不會出現overfitting過擬合的現象。
- 在真實資料滿足高次非線性曲線分佈的時候，loss function控制訓練出來的高次項的係數比較大，使得到的曲線比較彎折起伏。
- 在真實資料滿足低次線性分佈的時候，loss function控制訓練出來的高次項的係數比較小甚至等於0，使得到的曲線接近linear分佈

那我們如何保證能學出來這樣的參數呢? 這就是 L1 L2 正規化出現的原因。
之前的loss function僅考慮了
![](photo/Machine%20Learning/regularization/Pasted%20image%202.png)
這一誤差衡量標準，而L1 L2正規化就是在這個loss function的後面多加了一個東西，即model中跟高次項係數有關的運算式；
![](photo/Machine%20Learning/regularization/Pasted%20image%203.png)
相對來說，L2要更穩定一些，L1的結果則不那麼穩定，如果用p表示正規化程度，上面兩式可總結如下：
![](photo/Machine%20Learning/regularization/Pasted%20image%204.png)
![](photo/Machine%20Learning/regularization/Pasted%20image%205.png)

## 回到 [002 Machine Learning - Regression Case Study](002%20Machine%20Learning%20-%20Regression%20Case%20Study.md)