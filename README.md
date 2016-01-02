# learn-git
你可以 pork 本 repo 来实践学习 git 的使用  
  
## 前言
git 不仅仅只是 github, 还有 osc@git, bitbucket 等，都提供了使用 git 作为版本维护的  
服务。当然，github 是最早也是最知名的 git 服务商。

每次你在 github 上创建一个新的 repo 的时候，都会有下面这样的提示内容  
  
    …or create a new repository on the command line
    
    
    echo # learn-git >> README.md
    git init
    git add README.md
    git commit -m "first commit"
    git remote add origin https://github.com/dotku/learn-git.git
    git push -u origin master
    …or push an existing repository from the command line
    
    
    git remote add origin https://github.com/dotku/learn-git.git
    git push -u origin master
    …or import code from another repository
    
    You can initialize this repository with code from a Subversion, Mercurial, or TFS  
    project.
    
    Import code

我觉得做技术的，都需要有点耐心，刚刚开始可能云里雾里的，不过多看几遍，多多实践，  
就会明白这些东西了。  
  
这里我帮你翻译讲解一下  

    # 译文
    ...或者通过命令行创建一个代码仓库
    
    echo # learn-git >> README.md
    git init
    git add README.md
    git commit -m "first commit"
    git remote add origin https://github.com/dotku/learn-git.git
    git push -u origin master
    
    ...或者推送已经存在的代码仓库
    
    git remote add origin https://github.com/dotku/learn-git.git
    git push -u origin master
    
    ...或者通过其他的代码仓库里面导入代码
    
    你可以通过 Subversion, Mercurial 或者 TFS 项目来初始化本代码仓库
    
    [导入代码]

其实对于 git 初学者来说，即使看得英文的字面意思，还是不明白是什么，所以还是有必要  
一个个来讲解一下。

## 入门

既然来了这里，想必都知道 git 是用来管理版本的，看过故事，也知道 git 是 subversion 的  
晚辈这匹黑马能杀出重围，想必有什么过人之处。  

### 历史

了解一个技术，我总是很喜欢先读历史，了解一个来龙去脉，这样比较好把握这个技术的未来  
发展，所以来看看 git 的历史吧，来感受一下。  
  
简单的来说， git 是 Linux 的核心开发组的人于 2005 年的时候开发的，说是包罗万象的傻瓜式  
版本追踪器。

    GIT - the stupid content tracker

github 在 2008 年的时候就退出了其在线服务，市面上也有开源的 git 服务软件， osc, bitbucket  
等也加入了这摊生意。

### 基本原理  
  
git 复杂起来也很复杂，版本控制上有很多相关的图片说明，其实我是越看越晕。简而言之，其实  
是这样...  
  
每次 git init 的时候，就会在当前目录初始化，产生一个 .git 的隐藏文件夹，这个文件夹就包含了  
git 的一些列的信息，包括版本代号，更新编号 (用 40 位 sha 加密的信息) 等。只要这个文件夹到  
哪里，你的代码仓库，以及 git 控制范围就到哪里。  
  
好的，现在来讲解一下代码大概是什么意思。
  
#### 通过命令行创建一个代码仓库
  
        echo # learn-git >> README.md

这个是为了创建一个自读文件，其实没有太大意义，作为一个用来试验的文件例子而已，自读文件  
是不错的选择。

        git init

这个命令就初始化了 git，建立了 .git 目录，存储 git 信息。

        git add README.md

把 README.md 文件加入到版本控制中去，git 就识别到这个文件了，可以对这个文件进行跟踪。  
这里的 add 不仅仅只是新增文件到 git 中，还有删改等操作，也是通过 add 来执行添加动作的。  
其实在实际环境中，我们还经常通过 git status 来查看更新的动作。不过这里，我们保持简单，  
直接添加文件。

        git commit -m "first commit"

确认，或备注这条操作。

        git remote add origin https://github.com/dotku/learn-git.git

添加远程仓库的地址。  
  
其实简单通过 git clone 就可以完成， git init 和 git remote add 的操作了，不过这里是为了让步骤  
更加完整，估计这样安排的。  

        git push -u origin master 

恭喜你，把更新发布到远程上去了 :)

#### 推送已经存在的代码仓库
  
        git remote add origin https://github.com/dotku/learn-git.git
        git push -u origin master

如果能理解前面的内容，这两句就很简单了，就是已经执行过 git init, git add, git commit 之后，想要
push 代码到 github 上面来，就必须要 git remote add，然后 push 操作，就行了。
  
#### 通过其他的代码仓库里面导入代码

这个是说把别的项目代码通过 URL 方式导入， git 会自动转换其他的版本控制器，比如 subversion 等。
把他们的记录信息转换为 git 所使用的记录信息格式。

### 实践  
  
在实际操作中，我们经常是这样进行开发的。

        1. git fetch， 这个会更新 .git 目录下的内容
        2. git pull, 这个会更新代码文件夹中的内容; 一般我会用 git checkout master, master 是分支号码
        3. 更改代码，测试
        4. git status  检查
        5. git add .  添加代码入库， . 表示所有的, --all 表示包括删除的, <filename> 表示固定的某个文件
        6. git commit -m '更新备注'
        7. git push origin master, origin 表示你的 git 所在的位置, 可以通过 git remote -v，来查看 origin 所代表的 git url 信息，master 是分支代号

除此之外，还有 git checkout -b 来建立开发分支，还有 git commit --amed -m '修改 commit 信息'，  
以及 git diff，git merge 等操作用来合并不同的分支，还有 git rsa 密匙管理等，这个可以自行谷歌百度  
再深入了。
