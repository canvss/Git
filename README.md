# Git

**Git 是一个免费的开源 分布式版本控制系统，旨在快速高效地处理从小到大的所有项目。**

- 工作区：改动（增删文件和内容）
- 暂存区：输入命令：`git add 改动的文件名`，此次改动就放到了 ‘暂存区’
- 本地仓库(简称：本地)：输入命令：`git commit 此次修改的描述`，此次改动就放到了 ’本地仓库’，每个 commit，我叫它为一个 					‘版本’。
- 远程仓库(简称：远程)：输入命令：`git push 远程仓库`，此次改动就放到了 ‘远程仓库’（GitHub 等)
- commit-id：输出命令：`git log`，最上面那行 `commit xxxxxx`，后面的字符串就是 commit-id

> Git 是由 Linux 之父 Linus Tovalds 为了更好地管理linux内核开发而创立的分布式版本控制／软件配置管理软件。



## 安装Git

- brew install git
- git -versions

## Git常用命令

- git init：初始化Git
- git add .：添加当前目录所有文件到暂存区
- git add 文件名：将指定文件添加到暂存区
- git commit -m 提交名称：提交代码
- git status：查看状态
- git reset --hard 版本号：回到指定版本
- git reset HEAD 文件名：回到暂存区
- git checkout -- 文件名：
- git -help	查看帮助文档
- git remote rm origin 删除远程仓库
- git log  查看版本

### 案例：使用Git提交项目

#### 1.第一次提交登录功能

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

- git init		
- git status
- git add index.html
- git commit -m '登录功能'

#### 2.第二次提交注册功能

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

- git init
- git status
- git add index.html
- git commit -m '注册功能'

#### 3.第三次提交直播功能

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

- git init
- git status
- git add index.html
- git commit -m '直播功能'
- git log    

#### 4.现在我们想要删除直播功能，回到注册功能代码

![](img/reset_hard.png)

- git reflog
- git reset --hard 1d83b43409bc59c2175efa2a442477d1edc75b14

**此时html代码更新为：**

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

#### 5.现在想了想，觉得直播功能还是很好。我们需要直播功能

- git reset --hard 7315226

**此时html代码：**

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

#### 当文件代码添加到暂存区，怎么返回？

- git reset HEAD index.html 

#### 当代码更新，可以使用checkout来恢复到最初。

- git checkout -- index.html 

#### 总结：

**现在理解了Git是如何跟踪代码修改的，每次修改，如果不用`git add`到暂存区，那就不会加入到`commit`中。**

![](img/4.png)

## 分支（master）:

### 			案列：

**现在我们的项目有登录、注册、直播功能，现在需要新增功能为商城，商城功能写了一半（比如花了半个月），现在直播功能出现bug,需要调试我们应该怎么办呢？难道要放弃快完成的商城功能，回到直播功能调试bug吗？这里我们可以用到分支了。**

#### 1、在写新功能模块时，创建dev分支用于开发新的模块，再创建一个bug分支用于调试bug

```
endless@EndlessdeMacBook-Pro blogs % git branch dev 	创建dev分支
endless@EndlessdeMacBook-Pro blogs % git branch		查看分支
  dev
* master		  -->当前所在的主分支

```

#### 2、切换分支

```
endless@EndlessdeMacBook-Pro blogs % git checkout dev		切换到dev分支
M	.DS_Store
M	README.md
Switched to branch 'dev'
```

#### 3、在dev分支下开发商城功能	

- git checkout dev

**此时商城功能开发到一半，直播功能出现bug，我们需要提交商城功能代码，切换到master主分支，创建一个bug分支用于调试bug，并且不影响商城功能的开发**

#### 4、回到master，创建bug分支

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

##### 	现在bug修复完成	

#### 5、此时我们需要切回master上，将bug合并到master分支上.

#### 6、现在切换到dev分支继续开发商城功能

- git checkout dev
- git add . 
- git commit -m '商城功能开发完成'
- git checkout master

#### 7、手动解决冲突，就能完成合并 

- git merge dev

#### 8、删除调试完成bug的分支(git branch bug -d) 

```
endless@EndlessdeMacBook-Pro blog % git branch bug -d
Deleted branch bug (was adba566).
endless@EndlessdeMacBook-Pro blog % git branch   
  dev
* master
```

# GitHub

![](img/howusegithub.png)

**确切的说 GitHub 是一家公司，位于旧金山，由 Chris Wanstrath, PJ Hyett 与Tom Preston-Werner 三位开发者在2008年4月创办。2008年4月10日，GitHub正式成立，地址：How people build software · GitHub ，主要提供基于git的版本托管服务。一经上线，它的发展速度惊为天人，截止目前，GitHub 已经发展成全球最大的开（同）源（性）社区。**

## 如何使用Github？

![](img/20160509095442956.png)

> GitHub其中一位创始人[Chris](defunkt (Chris Wanstrath) · GitHub)也详细描述了[GitHub初创的前因后果](Startup Riot 2009 Keynote 路 GitHub)，他说道：Do whatever you want.



## 使用GitHub实现代码托管

### 案列1：

**今天在公司开发了a功能，但是回家需要继续开发a功能，这时就可以将本地代码提交到github上面，回到家将github代码clone到本自己的mac上继续开发a功能。然后在家开发完了a功能，第二天去公司需要继续开发b功能就需要把昨天在家开发的a功能给pull(拉)到公司的电脑上。**

#### 1、将今天在公司写的代码提交到github上面

- git add .
- git commit -m '在公司写了A功能70%'
- git remote add origin https://github.com/epover/git.git
- git push -u origin master	或者 git push origin master
- git push origin dev

#### 2、回到家将公司的代码给clone到本地

- git clone github地址
- git checkout dev
- 继续开发A功能剩下的30%
- git add . 
- git commit -m '在家开发A功能30%'
- git push origin master
- git push origin dev

#### 3、第二天回到公司

- git checkout dev
- git pull origin dev
  
  

**总结 ：GitHub使用起来非常方便，当你写完代码只需要push到GitHub上就行了，需要再次开发的时候只需pull到本地。**

### 案列2：

**今天在公司开发新功能A（完成50%）提交完代码，下班。回到家中pull才发现在公司忘记push到GitHub上面去了，此时你根据记忆继续开发功能A（完成%30），又新开发了B功能（50%），然后push睡觉。第二天回到公司**

#### 1、今天在公司开发新功能A（完成50%）提交完代码，下班。

```
在开公司写代码
git add .
git commit -m '公司开发A功能（50%）'
```

#### 2、回到家中pull才发现在公司忘记push到GitHub上面去了，此时你根据记忆继续开发功能A（完成%30），又新开发了B功能	（50%），然后push睡觉。

```
git pull origin dev 
发现没有更新
凭借记忆努力写代码
git add .
git commit -m '在家通过记忆对A功能继续开发30%；还开发了B功能'
git push origin dev
```

#### 3、第二天回到公司，继续开发A功能剩下的20%和B功能剩下的50%。  

```
git push origin dev
此时会提醒合并冲突，因为昨天在公司和在家都对A功能进行了开发，在合并时会发生冲突，此时需要我们收到解决它
继续开发A功能剩下的20%和B功能剩下的50%
.....
git add .
git commit -m '项目开发完成'
git push origin dev
git checkout master
git merge dev
git push origin master
```



### 总结：常用命令

- git remote add origin https://github.com/sqlsafe/git.git
- git remote remove origin 	删除origin
- git push origin	推送代码
- git pull origin	获取代码



### 常见问题：

#### 1、remote: Support for password authentication was removed on August 13, 2021

**官方解释：**https://github.blog/2020-12-15-token-authentication-requirements-for-git-operations/

修改token的动机

我们描述了我们的动机，因为我们宣布了对 API 身份验证的类似更改，如下所示：近年来，GitHub 客户受益于 GitHub.com 的许多安全增强功能，例如双因素身份验证、登录警报、经过验证的设备、防止使用泄露密码和 WebAuthn 支持。 这些功能使攻击者更难获取在多个网站上重复使用的密码并使用它来尝试访问您的 GitHub 帐户。 尽管有这些改进，但由于历史原因，未启用双因素身份验证的客户仍能够仅使用其GitHub 用户名和密码继续对 Git 和 API 操作进行身份验证。从 2021 年 8 月 13 日开始，我们将在对 Git 操作进行身份验证时不再接受帐户密码，并将要求使用基于令牌（token）的身份验证，例如个人访问令牌（针对开发人员）或 OAuth 或 GitHub 应用程序安装令牌（针对集成商） GitHub.com 上所有经过身份验证的 Git 操作。 您也可以继续在您喜欢的地方使用 SSH 密钥（如果你要使用ssh密钥可以参考）

**解决办法：**

- 创建token：https://github.com/settings/tokens	

- 将token添加到远程仓库中：git remote set-url origin https://<your_token>@github.com/USERNAME/REPO	

- 例如：git remote set-url origin https://ghp_7WkOwfkDasasdgsgdsaskFshyasvswUzJCLrdsgsaYm@github.com/name/project.git

#### 2、kex_exchange_identification: read: Connection reset by peer

Connection reset by 20.205.243.178 port 22
fatal: Could not read from remote repository.
Please make sure you have the correct access rights
and the repository exists.

**解决办法：**

生成新的公钥：ssh-keygen-t rsa -C"邮箱地址"
