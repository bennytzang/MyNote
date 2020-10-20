---
# reshape():
[Python Numpy.reshape(矩阵,(-1,1))_currycode-CSDN博客](https://blog.csdn.net/zongza/article/details/83050001) [[Obsidian-Highlights]]

**z.reshape(-1)**
![](Pasted%20image%2020201013162738.png)
**z.reshape(-1, 1)：**

也就是说，先前我们不知道z的shape属性是多少，但是想让z变成只有一列，行数不知道多少，通过**z.reshape(-1,1)**，Numpy自动计算出有12行，新的数组shape属性为(16, 1)，与原来的(4, 4)配套。
![](Pasted%20image%2020201013162826.png)

**z.reshape(-1, 2)：**

newshape等于-1，列数等于2，行数未知，reshape后的shape等于(8, 2)
![](Pasted%20image%2020201013162900.png)

-- -
# drop()
[Python中pandas dataframe删除一行或一列：drop函数_海晨威-CSDN博客](https://blog.csdn.net/songyunli1111/article/details/79306639) [[Obsidian-Highlights]]


	用法：
	DataFrame.drop(labels=None,axis=0, index=None, columns=None, inplace=False)

参数说明：

* labels 就是要删除的行列的名字，用列表给定==axis 默认为0==，指==删除行==，因此**删除columns==时要指定axis=1**；
* index 直接指定要删除的行
* columns 直接指定要删除的列
* inplace=False，默认该删除操作不改变原数据，而是返回一个执行删除操作后的新dataframe；
* inplace=True，则会直接在原数据上进行删除操作，删除后无法返回。

因此，删除行列有两种方式：
1. labels=None,axis=0 的组合
2. index或columns直接指定要删除的行或列

例子：
![](Pasted%20image%2020201013164356.png)

-- - 
### enumerate()
* 多用於在for循環中得到計數，利用它可以同時獲得索引和值，即==需要index和value值的時候可以使用enumerate==

-- -
# plt參數 
### 直方圖hist(histagram)
 - bins :幾條盒狀圖
 - normed:盒狀圖所佔比例比，默認為1
 
![](Pasted%20image%2020201020164408.png)

### 散佈圖(Scatter plot)

![](Pasted%20image%2020201020164542.png)