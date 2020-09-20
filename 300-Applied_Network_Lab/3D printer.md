- [你要學懂的3D打印基本設定 - 3D Printing Lab](https://www.3dprintinglab.com.hk/blog/basic-settings-of-3d-printing-slicing-software) #[[Roam-Highlights]]
- 
### 層厚 （Layer Height）
層厚的3D打印設定越大模型的質素就越低，但打印所需的時間就越短，相反層厚的3D打印設定越小，打印就越細緻，但打印時間越長。一般來說，0.1-0.15mm （100 -150microns）的層厚設定是已經屬於高質素，而0.2mm （200 microns）就算屬於中級質素。

### 殼厚 （Shell Thickness）
Shell thickness 就是模型的外殼的厚度，而Shell thickness的3D打印設定要是噴嘴（nozzle）直徑的倍數，而==一般Shell thickness是噴嘴直徑的兩倍==。
精緻或裝飾性設計通常不需要強度

### 填充密度（Fill Density/ Infill）
FillDensity就是3D打印物件裡面的填充密度，假如填充密度是100%，那麼模型就會被打印成實心，而0%的話模型就會是空心，而填充密度太低有可能導致模型出現穿崩（pillowing）。
一般來說，為了令模型堅硬一些，==填充密度的3D打印設定在BCN3DCura中一般為20%==。

### 打印速度 （Print Speed）
3D打印速度（以mm/s 為單位）是指當噴嘴擠出打印物料時，打印噴頭所移動的速度。
細節較少的簡單物體可以更快地打印。另一方面，具有更多細節的更複雜物體較適合較慢的打印速度。打印速度還會影響到打印表面的附著力，導致擠出不足或過度以及其他問題。
==一般40mm/s 是一個很好的嘗試開始點==。

### 支撐（Support）
當打印的物件有懸空部分時，用家就可能需要加 支撐用來承托懸空的部分。一般來講，==當3D模型某部分的傾斜度超過45度，就需要在BCN3D Cura中設定支撐。==

### 底座類型（Platform Adhesion Type）
這個3D打印設定決定了你怎樣把模型粘貼在打印床上。 當你發現打印模型時出現翹邊的情況時，又或者模型與打印床的接觸點太小，你就可以在BCN3D Cura或3D打印軟件中啟動這個3D打印設定。啟動這個設定後面，用家一般有兩個選擇 - Raft 和 Brim。
Brim： 選擇這個的話，==便會在在模型底部產生延伸的邊緣，這個延伸的邊緣會增加物件粘在打印床的強度，減低翹起的情況。==
Raft ： ==會在模型底部多打印一個底座，在打印一些與打印床的接觸點小的模型時加上Raft會有很大幫助。== BCN3D Cura 中有一個叫Platform Adhesion Type的欄目讓用家選擇Raft 及Brim。

### 噴嘴加熱溫度（Printing Temperature ）
PLA的加熱3D打印溫度設定一般約==210度到225度==。而ABS則是==230-245度左右。==

### 打印平台溫度（Platform Temperature）
使打印物料粘附到打印表面是成功進行打印的關鍵。PLA在某種程度上很容易粘附到各種表面上，所以使PLA成為易於3D打印的材料之一。
雖然不帶加熱床打印PLA也可以，但打印平台如果能加熱的話，對於打印大面積的PLA模型更能粘附得更好，一般建議3D打印平台溫度設定在==50至65度之間。==
### 縮回 (Retraction)
當打印噴頭從打印物件上的一個打印點移動到另一個打印點時，縮回
這個打印設定會將打印膠絲稍微拉回到打印噴頭中。這樣可以減少膠絲從打印噴嘴中漏出，在原本為中空的地方留下一串膠料。