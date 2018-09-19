# git分布式版本控制系统：   
下载git：https://git-scm.com/downloads   

找到git bash打开,配置git：  
```
$ git config --global user.name "zhyufe711"
$ git config --global user.email "550583865@qq.com"  
```   
去项目目录learngit初始化git：  
```
$ cd d:
$ mkdir learngit
$ cd learngit
$ git init
```   
*`pwd` 可以显示当前目录   
`$ ls -al` 列出当前路径下所有文件的详细信息（包括隐藏文件）   
输入git init后文件夹会多一个隐藏文件夹.git*  

learngit文件夹下建个readme.html 用编辑器写点内容，添加文件到Git仓库：  
```
$ git add readme.html
$ git commit -m "这里是提交的说明"  
```   
*`$ git add readme.html` 把要提交的所有修改放到暂存区   
`$ git commit -m "这里是提交的说明" ` 一次性把暂存区的所有修改提交到分支*  

`git add`可以反复多次使用，添加多个文件，`git commit`可以一次提交很多文件，-m后面输入的是本次提交的说明，可以输入任意内容。  
`$git add file1.html file2.html file3.html`   

新建js文件夹就换成文件夹名字，文件夹里边的文件在修改提交前，别忘切换到文件夹目录  
```
$ git add js
$ cd js
```     
直接add文件夹里所有内容并提交：   
```
$ git add .   
$ git commit -m 'first commit'  
```   

查看文件全部内容   
`$ cat readme.html`   

查看工作区状态：    
`$ git status`

查看工作区(work dict)和暂存区(stage)的区别   
`$ git diff `

查看暂存区(stage)和分支(master)的区别   
`$ git diff --cached`

看工作区和版本库里面最新版本的区别   
`$ git diff HEAD -- readme.html`

查看提交日志,查看日志过程按q退出，回退前可以看看回退到哪儿   
`$ git log`

查看最后一次提交信息：   
`$ git log -1`

简化查看日志输出信息   
`$ git log --pretty=oneline`

查看命令历史   
`$ git reflog`

版本回退   
`$ git reset --hard HEAD^`  
*以上命令是返回上一个版本，在Git中，用HEAD表示当前版本，上一个版本就是HEAD^，上上一个版本是HEAD^^，往上100个版本写成HEAD~100。*  

reflog记录每一次命令，可以查看操作的commit id 方便回退和返回未来  
```
$ git reflog 
$ git reset --hard 8795fc6
```  

### 工作区、暂存区和版本库:  
工作区：在电脑里能看到的目录。  
版本库：在工作区有一个隐藏目录.git，是Git的版本库。   
Git的版本库中存了很多东西，其中最重要的就是称为stage（或者称为index）的暂存区，还有Git自动创建的master，以及指针HEAD。   

`$ git add`实际上是把文件添加到暂存区  
`$ git commit`实际上是把暂存区的所有内容提交到当前分支

撤销修改:   
当你改乱了工作区某个文件的内容，想直接丢弃工作区的修改时，用命令   
`$ git checkout -- readme.html`  

当你不但改乱了工作区某个文件的内容，还添加到了暂存区时，想丢弃修改，分两步:   
第一步，把暂存区的修改撤销掉   
`$ git reset HEAD readme.html`   
第二步，撤销工作区的修改   
`$ git checkout -- readme.html`   

*已经提交了不合适的修改到版本库时，想要撤销本次提交，进行版本回退，前提是没有推送到远程库。*   

删除文件:两种方法。第二种方法回溯比较万能，但会丢失最近一次提交后你修改的内容：   

1.直接找到文件删除，或者执行`$ rm main.js`删除的。   
可以执行：`$ git checkout -- main.js`还原。   
*注意，如果main.js在js文件夹。 正好js文件夹又只有一个main.js文件。那会把js文件夹也删除，就不能这么还原了。就要用2还原*   

 2.`$ git rm main.js`或者之后又提交了 `$ git commit -m 'del main.js'` 都只能通过版本回溯了。要知道版本号后 `$ git reset --hard 7303e84`   

### 远程仓库和本地建立关联：   
先看本地主目录（c盘用户，55058文件夹）下有没有.ssh目录，没有就要创建SSH Key：   
`$ ssh-keygen -t rsa -C "550583865@qq.com"`   

*创建一路回车，会看到创建在哪儿里，其实就是在主目录里。找到其中id_rsa_pub是公钥，可以告诉别人的。复制里边内容。*   

到github网站，找到setting里边的SSH，创建个SSH，其中title随便起，黏贴复制的内容进去，确认创建。   
如果别的地方的电脑，就要重复上边的步骤再添加给SSH，或者直接把之前创建的拿来用   

### 从本地关联远程库：   
先在github上new repository 其中repository name填本地的仓库文件名，比如learngit。确定   
在本地的learngit仓库下运行命令： 第一次会有SSH警告，yes就好。   
`$ git remote add origin git@github.com:zyf711/learngit.git` 

*添加后远程库的名字就是origin,也可以改成别的*   

下一步，就可以把本地库的所有内容推送到远程库上，第一次推送写-u 之后可以省略   
`$ git push -u origin master`   

之后每次提交到远程就   
`$ git push origin master`   

### 从远程库克隆到本地：
github上新建一个仓库，叫gitskills。创建时选上创建readme.md文件   

本地可以通过SSH或者https等途径克隆：   
`$ git clone git@github.com:zyf711/gitskills.git`    
`$ git clone https://github.com/zyf711/gitskills.git`   

克隆之后可以到里边看看有什么 ls是查看文件夹里内容:   
```
$ cd gitskills
$ ls
```  
*多人协作开发：每个人从远程库克隆一份就可以了。https慢。有时还要输入口令。但是有的公司只开放http。就不能用SSH了*   

### 分支：  
一条时间线，主分支master指向提交。HEAD指向当前分支，创建dev分支，HEAD指向dev分支，合并是直接把master指向dev当前提交。合并完可以删dev   

创建分支：   
`$ git branch dev`   

切换分支：   
`$ git checkout dev`

创建+切换分支：   
`$ git checkout -b dev`

查看分支:   
`$ git branch`

查看所有分支（包含远程的）:    
`$ git branch -a`

合并分支到当前分支：   
`$ git merge dev`   
*默认Fast-forward模式，假设当前为master分支。就是直接把master指向dev的当前提交，所以合并速度非常快。但删除分支后，会丢掉分支信息*  

删除分支：   
`$ git branch -d dev`   

在dev上干活，合并到master，删除dev：   
`$ git checkout dev`

干完活儿之后   
```
$ git add readme.html
$ git commit -m 'over'
$ git checkout master
```  
注意在master下合并dev   
```
$ git merge dev
$ git branck -d dev
```   
### 合并分支发生冲突：   
创建新分支feature，修改内容。提交   
切换到master分支，修改内容。提交   
合并分支feature，提示冲突。   
打开编辑器，里边内容会有冲突标识，手动修改好再提交，最后正常了再合并删除feature   
使用`$ git log --graph`可以看分支合并图   

普通模式合并分支--no-ff：  
会在合并时生成一个新的commit，这样从分支历史`$ git log`就可以看出分支信息：   
`$ git merge --no-ff -m "description" dev`   

*默认合并分支的话会用fast forward模式，这种模式删除分支后会丢掉分支信息`$ git merge dev*`   

### 分支策略：   
master分支应是非常稳定的，仅用来发布新版本，不能在上边干活   
所有人干活儿都在dev分支，每个人都有自己的分支，时不时往dev分支合并就可以了。   
到某个时刻再把dev合并到master上，在master上发布1.0版本   

### bug分支：
正在dev分支干活儿，接到一个代号101bug任务要马上修复。但还没发提交正在干的活儿，我们需要先把工作现场存储起来，完成紧急任务继续干活   
保存工作现场：   
`$ git stash` 

现在查看工作区是干净的    
`$ git status`   

然后确认在哪里修复bug，比如在master分支，就切换到master分支，创建临时分支：   
```
$ git checkout master
$ git checkout -b issue-101
```   
修复bug然后提交。到master分支完成合并。   
之后回dev分支干活，可以先查看工作现场还在：   
`$ git stash list` 

一种是:   
`$ git stash apply` 恢复，stash内容并不删除，需要 `$ git stash drop` 来删除。

一种是：   
`$ git stash pop` 恢复同时删除stash内容。

可以保存多个工作现场，用`$ git stash list`就能看到。选择想要恢复的工作现场：   
`$ git stash apply stash@{0}`   

### feature分支：   
在dev分支下建一个新任务分支feature分支，干完提交后准备合并，被告知不要这个内容了。要删除分支。    
`$ git branch -D feature`   
*如果要丢弃一个没有被合并过的分支，可以通过git branch -D feature强行删除。*

### 多人协作：
当从远程仓库克隆时，实际git自动把本地master分支和远程master分支对应起来了。远程仓库默认名称origin    
查看远程库信息（详细信息）：
```
$ git remote
$ git remote -v
```   
推送dev分支，所有成员都在上边工作，要与远程同步：   
`$ git push origin dev`   

*bug分支，没必要推送，除非老板看。feature分支是否推送，取决是否和别人在上边协作开发*   

大家都会往master和dev分支推送修改，比如别人从远程clone时，默认他只能看到本地的master分支。   
现在要在dev分支上开发，就必须创建远程origin的dev分支到本地，之后建立关联就可以在dev上修改了，然后时不时的把dev分支push到远程。   
小伙伴已经向origin的dev分支推送内容，而你也修改了试图推送就会失败。要先从远程抓取分支：   

`$ git pull`   

如果pull也失败，提示:no tracking information,说明是本地dev分支没和远程dev分支建立链接，设置：   

`$ git branch --set-upstream-to=origin/dev dev`   

或者   

`$ git branch --set-upstream dev origin/dev`   

之后在pull成功，但如果合并有冲突，要解决冲突再提交再push   
*在git bash里边每行右侧显示当前路径的位置，原本比如是dev分支，现在可能变成dev|MERGING*   

删除远程分支:    
`$ git push origin --delete dev`

`$ git rebase`执行后，再`$ git log` 原本分叉的提交变成了直线，看上去直观了，缺点是本地的分叉提交被修改过了。   

### 标签：
切换到要打标签的分支上，创建标签：   
`$ git tag v0.1`  

可以用命令查看所有标签：  
`$ git tag`

默认标签打在最新上，想打之前版本上要找到历史提交的commit_id 比如想打在f52c663上  
```
$ git log --pretty 看到了f52c663
$ git tag v0.1 f52c663
```
打带说明的标签：   
`$ git tag -a v0.1 -m '第一个标签'`

查看标签信息：   
`$ git show v0.1`

删除标签：  
`$ git tag -d v0.1`

标签总与commit挂钩，如果这个commit即出现在master又出现在dev，那在两个分支都可以看到标签。   
创建标签都只存在本地，不会自动推送。如要推送：   
`$ git push origin v0.1`

一次推送全部标签：   
`$ git push origin --tags`

如果想删除远程标签，先删除本地的。之后再删远程的：   
```
$ git tag -d v0.1
$ git push origin :refs/tags/v0.1
```  
在github上fork   
fork就在自己账号下克隆了一个仓库 ，然后从自己账号下clone:   
`$ git clone git@github.com:zyf711/bootstrap.git`   

*一定要从自己账号下clone仓库，这样才能推送修改。之后本地干活儿，往自己仓库推送，如果希望bootstrap接受你的修改，发起pull request*   

开源中国的码云，国内的git托管服务gitee.com   
网站上也要弄SSH公钥，如果和github一起同步等操作，远程仓库名origin都是默认的，需要修改下。   

在电脑git的工作区要想忽略一些特殊文件，避免一起传到远程。原则：   
忽略操作系统自动生成的文件   
忽略编译生成的中间文件   
忽略自己带有敏感信息的配置文件   

在工作区建一个.gitignore文件，把要忽略的文件名填进去。这个文件不会被上传到远程   
注意：在编辑器里新建保存，不然windows下直接建会提示必须输入文件名   
想添加文件到git，发现添加不了，有可能是被.gitignore忽略了，-f可强制添加：  
`$ git add -f app.class`   

配置别名,比如：      
`$ git config --global alias.st status`   

*现在输入$ git st 就等同于 $ git status了。每个仓库的git配置文件都在.git/config中，别名就在[alias]里，删别名直接在里边删对应的行即可。*   

当前用户的git配置放在用户主目录（c盘用户，55058文件夹）下的一个隐藏文件夹.gitconfig中，同样方法删设置。   
比如设置叫git适当现实不同颜色，`$ git config --global color.ui true` 就能在.gitconfig中找到   
```
[user]
	name = zhyufe711
	email = 550583865@qq.com
[color]
	ui = true
```   
### 搭建git服务器：   
负责人创建裸服务器，比如git文件夹叫git-server   
甲同学从服务器clone到本地工作，   
`$ git clone 服务器地址 `  
windows下就是使用绝对路径，比如   
`$ git clone E:\git-server`   
clone到本地随意的地方，比如d盘之类的地方，开始干活儿即可。  

github上：   
watch:会关注项目所有动态。项目任何变动，别人pull request issue等，都会通知你   
star:相当于点赞，之后可以在自己的账号上看到。   
fork:相当于原项目的拷贝。如原项目改变，这里不变的。fork就是到自己这里修改，pull request用。   

*小功能：github任何页面按shift+? 都可以看快捷键帮助*

**搜索栏：stars:>1 右边选 sort:most stars 可以看当下star最多的项目排行**

















