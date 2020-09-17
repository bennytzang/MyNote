# git push
 - git status
 - git add .
 - git commit -m "text" 
 - git push

# git pull
 - git stash (本地與遠端資料不一致時)ㄔ
 - git pull

### 參考資料
[【Git学习笔记】Git冲突：commit your changes or stash them before you can merge._刘春明的博客-CSDN博客](https://blog.csdn.net/liuchunming033/article/details/45368237?utm_medium=distribute.pc_relevant.none-task-blog-title-1&spm=1001.2101.3001.4242)

    有的时候使用git pull命令，可能遇到这样的问题：

	Please, commit your changes or stash them before you can merge.  
	Aborting

    这是由于远程库中的更改与本地的更改有冲突。
    git的提示已经非常明确了，告诉我们要么把我们的更新进行commit要么就先stash本地更新。
    第一种方法，stash：
    那怎么stash本地的更新呢？直接执行：
    git stash：备份当前的工作区，从最近一次提交中读取相关内容，让工作区保持和上一次提交的内容一致。同时，将工作区的内容保存到git栈中。
    git stash pop：从git栈中读取最近一次保存的内容，恢复工作区的相关内容。由于可能存在多个stash的内容，所以用栈来管理，pop会从最近一个stash中读取内容并恢复到工作区。
    git stash list：显示git栈内的所有备份，可以利用这个列表来决定从那个地方恢复。
    git stash clear：情况git栈。