#  如何使用Git和GitHub


![](./img/aHR0cHM6Ly9tbWJpei5xcGljLmNuL21tYml6X3BuZy91RFJrTVdMaWEyOGdmYkNUaFFvemtIM0lCemRTTTVJckFadjVDakM3QTJjU0wwS3JRQVFJZkQ3a2liQ2pwUHRjandFSFdpY0hGbXc1TTlHcjZWTGpEV2xpY0EvNjQw.png)

# 什么是Git？

​	Git 是一个免费的开源 分布式版本控制系统，旨在快速高效地处理从小到大的所有项目。

​	首现我们需要知道

​		工作区：改动（增删文件和内容）

​		暂存区：输入命令：`git add 改动的文件名`，此次改动就放到了 ‘暂存区’

​		本地仓库(简称：本地)：输入命令：`git commit 此次修改的描述`，此次改动就放到了 ’本地仓库’，每个 commit，我叫它为一个 ‘版		本’。

​		远程仓库(简称：远程)：输入命令：`git push 远程仓库`，此次改动就放到了 ‘远程仓库’（GitHub 等)

​		commit-id：输出命令：`git log`，最上面那行 `commit xxxxxx`，后面的字符串就是 commit-id



![](img/git_1.png)

### 安装git

```
brew install git
git -version
```

### git常用命令

```
git init		
git add .
git add 文件名
git commit -m 文件名
git status
git reset --hard 版本号
git reset HEAD 文件名
git checkout -- 文件名
git -help	查看帮助
```



### blogs项目使用git案例

###### 1.首先写一个简单功能的html

```html
<!DOCTYPE html>
<html>
<head>
	<meta charset="utf-8">
	<title>index</title>
</head>
<body>	
		<h1>登录</h1>
</body>
</html>
```

在blogs文件下初始化项目添加到暂存区和提交

###### 2.第一次提交登录功能

```
git init
git status
git add index.html
git commit -m '登录功能'
```



###### 3.第二次提交注册功能

```html
<!DOCTYPE html>
<html>
<head>
	<meta charset="utf-8">
	<title>index</title>
</head>
<body>	
		<h1>登录</h1>
  <h1>注册</h1>
</body>
</html>
```

```
git init
git status
git add index.html
git commit -m '注册功能'
```

###### 4.第三次提交直播功能

```html
<!DOCTYPE html>
<html>
<head>
	<meta charset="utf-8">
	<title>index</title>
</head>
<body>	
			<h1>登录</h1>
 		 <h1>注册</h1>
 		 <h1>直播</h1>
</body>
</html>
```

```
git init
git status
git add index.html
git commit -m '直播功能'
git log 查看版本
```

![](img/git_log.png)



###### 5.现在我们想要删除直播功能，回到注册功能代码

```
git reflog
git reset --hard 1d83b43409bc59c2175efa2a442477d1edc75b14
```

![](img/reset_hard.png)

此时html代码更新

```html
<!DOCTYPE html>
<html>
<head>
	<meta charset="utf-8">
	<title>index</title>
</head>
<body>	
		<h1>登录</h1>
  <h1>注册</h1>
</body>
</html>
```

###### 6.现在想了想，觉得直播功能还是很好。我们需要直播功能

```
endless@EndlessdeMacBook-Pro blogs % git reset --hard 7315226
HEAD is now at 7315226 直播
```

![](img/git_log.png)

此时html代码：

```html
<!DOCTYPE html>
<html>
<head>
	<meta charset="utf-8">
	<title>index</title>
</head>
<body>	
			<h1>登录</h1>
 		 <h1>注册</h1>
 		 <h1>直播</h1>
</body>
</html>
```



当文件代码添加到暂存区，怎么返回

```
endless@EndlessdeMacBook-Pro blogs % git reset HEAD index.html 
Unstaged changes after reset:
M	index.html
```

当代码更新，可以使用checkout来恢复到最初

```
endless@EndlessdeMacBook-Pro blogs % git checkout -- index.html 
```

###### 总结：现在理解了Git是如何跟踪代码修改的，每次修改，如果不用`git add`到暂存区，那就不会加入到`commit`中。





### 	![](img/4.png)



### 分支（master）:

##### 			案列：现在我们的项目有登录、注册、直播功能，现在需要新增功能为商城，商城功能写了一半（比如花了半个月），现在直播功能出现bug😩😩,需要调试我们应该怎么办呢？难道要放弃快完成的商城功能，回到直播功能调试bug吗？这里我们可以用到分支了。

###### 	1、在写新功能模块时，创建dev分支用于开发新的模块，再创建一个bug分支用于调试bug

```
endless@EndlessdeMacBook-Pro blogs % git branch dev 	创建dev分支
endless@EndlessdeMacBook-Pro blogs % git branch		查看分支
  dev
* master		  -->当前所在的主分支

```

###### 	2、切换分支

```
endless@EndlessdeMacBook-Pro blogs % git checkout dev		切换到dev分支
M	.DS_Store
M	README.md
Switched to branch 'dev'
```

###### 	3、在dev分支下开发商城功能	

```
git checkout dev
```

![](img/gitsc.png)	

此时商城功能开发到一半，直播功能出现bug，我们需要提交商城功能代码，切换到master主分支，创建一个bug分支用于调试bug，并且不影响商城功能的开发

###### 	4、回到master，创建bug分支

```
endless@EndlessdeMacBook-Pro blog % git log		#此时在master分支上并没有商城功能完成50%
commit 7feddb1b99a42918f39ccf898275f18d96893d02 (HEAD -> master, bug)
Author: epover <endliss@sina.cn>
Date:   Sun Jul 18 22:52:49 2021 +0800

    第一次项目完成
endless@EndlessdeMacBook-Pro blog % git branch bug
endless@EndlessdeMacBook-Pro blog % git checkout bug
Switched to branch 'bug'
```

​	现在bug修复完成👍![](img/gitbug.png)		

###### 	5、此时我们需要切回master上，将bug合并到master分支上。

![](img/gitbug_master.png)

###### 	6、现在切换到dev分支继续开发商城功能

```
git checkout dev
git add . 
git commit -m '商城功能开发完成'
git checkout master

[endless@EndlessdeMacBook-Pro blog % git merge dev		#此时提醒有冲突，需要解决冲突才能合并
Auto-merging index.html
CONFLICT (content): Merge conflict in index.html
Automatic merge failed; fix conflicts and then commit the result.
```

###### 	 7、手动解决冲突，就能完成合并 ✌️😉

![](img/gitdev_master.png)

###### 	8、删除调试完成bug的分支(git branch bug -d) 

```
endless@EndlessdeMacBook-Pro blog % git branch bug -d
Deleted branch bug (was adba566).
endless@EndlessdeMacBook-Pro blog % git branch   
  dev
* master
```



### 使用GitHub实现代码托管

​	**案列**：今天在公司开发了a功能，但是回家需要继续开发a功能，这时就可以将本地代码提交到github上面，回到家将github代码clone到本自己的mac上继续开发a功能。然后在家开发完了a功能，第二天去公司需要继续开发b功能就需要把昨天在家开发的a功能给pull(拉)到公司的电脑上。

###### 	1、将今天在公司写的代码提交到github上面	

```
git add .
git commit -m '在公司写了A功能70%'
git push origin master
git push origin dev
```

###### 	2、回到家将公司的代码给clone到本地

```
git clone github地址
git checkout dev
继续开发A功能剩下的30%
git add . 
git commit -m '在家开发A功能30%'
git push origin master
git push origin dev
```

###### 	3、第二天回到公司

```
git checkout dev
git pull origin dev
继续研发。。。
```

###### **总结** ：GitHub使用起来非常方便，当你写完代码只需要push到GitHub上就行了，需要再次开发的时候只需pull到本地。




> ### 推荐阅读：
>
> ##### [和我一起学习Django👍](https://github.com/epover/LearnDjango)
> ##### [🌳🚀 CS 可视化：有用的 Git 命令](https://github.com/epover/Learn_GitHub/blob/main/%F0%9F%8C%B3%F0%9F%9A%80%20CS%20%E5%8F%AF%E8%A7%86%E5%8C%96%EF%BC%9A%E6%9C%89%E7%94%A8%E7%9A%84%20Git%20%E5%91%BD%E4%BB%A4.md)
> ##### [和我一起学习WebService👍](https://github.com/epover/WebService) 
>
> **[Angular团队提交规范👍](https://github.com/angular/angular.js/blob/master/DEVELOPERS.md#-git-commit-guidelines)**







