#简单Git与Github交互使用的总结

[toc]

# 屁话
我说现在哥们是真的不会用Git,所有的操作都局限于开一个`main`分支然后`commit`,完事再`push`到github上面,最多是开一个新分支然后`merge`到`main`里面...

无所谓还是可以写一写.主要跟Github结合一下.
    
## 连接Github
在关联本地和远程仓库时,需要先建立连接.一般使用SSH密钥连接,[在GitHub的Setting](https://github.com/settings/keys)里可以找到.有点麻烦,不过用一次就可以了,记不得上网搜.

## 基础操作
在Github创建仓库时,会给出一个模版:

    echo "# aaaaa" >> README.md
    git init
    git add README.md
    git commit -m "first commit"
    git branch -M main
    git remote add origin https://github.com/zzzxc332233/aaaaa.git
    git push -u origin main

逐行来解析一下.

    echo "# aaaaa" >> README.md     //创建README.md
 
    git init    //初始化仓库
 
    git add README.md   //跟踪README.md

    git commit -m "first commit"    //进行首次提交

    git branch -M main  //将主分支置为main
    
    git remote add origin https://github.com/zzzxc332233/aaaaa.git  //连接Github仓库
    
    git push -u origin main //进行首次推送

首先我们要明白Git是一个以"提交(commit)"为单位的管理程序,每次执行提交时就会创建一个`commit`,可以创建不同的分支(branch)来创建不同的提交树.分支名实际上是指向提交的一个指针,可以操作指针在提交树上进行移动,更新或者合并等操作.还有一个特殊的指针:`HEAD指针`,它通常是指目前操作的指针,但也可以将其分离实现一些特性.

比较重要的命令有

### `git checkout`
用于在不同分支间切换.其实也承担了很多其它的功能.

### `git branch`
用于操纵分支.`git branch new`创建新分支,参数`-d`用于删除分支,`-D`用于强制删除.`-a`则用于展示所有分支.

创建完分支后记得`checkout`过去.

### `git commit`
用于进行一次提交.需要注意,分支仅创建是不够的,此时他的指针仍停留在`HEAD`的位置上,需要commit一次将这两个指针分离.

### `git merge`
`git merge new`可以把`new`分支合并到`HEAD`处并创建一个新的commit.需要注意,此时作为一个指针,`new`仍然停留在原有的提交的位置上.这时如果checkout到`new`再执行`git merge main`,因为这时`main`已经成为了原有的`main`和`new`的并集,或者说`main`对`new`有继承关系,这两个提交树将会完全合并,`main`和`new`同样停留在`HEAD`位置.

### `git reset`
使用`git reset HEAD~2`用于回滚到当前的前两个提交,其中`HEAD~n`表示向上位第n个提交相对引用.而`HEAD^`=`HEAD~1`,`HEAD^^^`=`HEAD~3`.

当然`reset`的后面也可以接一个普通的指针.

### `git rebase`
在分支`new`时,如果执行`git merge main`,则会将`new`以上与`main`分支分开的地方全部复制粘贴到`main`的下面.这使得并行的开发好像变成了**线性的**,这很适合进开发->测试->更新的流程.但是多人开发的时候也许不太能有完全并行的开发场景.

### `题外话:远程开发`
但我们需要注意到一点:本地仓库的更新不可能与远程仓库永远保持同步(除非愿意付出高昂的网络代价),而且逻辑上远程仓库*似乎是*"只加不减"的,有时无法方便地进行回滚或删除操作,并且如果小伙伴这时有更新,还需要将远程仓库的更新同步到本地.总之有点区别,嗯.

### `远程分支`
造成上述特性的一个原因就是远程分支的存在,远程分支有一个命名规范 —— 它们的格式是:
    
    <remote name>/<branch name>

接下来与Github保持一致,令

        <remote name> = origin
        <branch name> = main

其实`origin/main`反映的是**远程仓库(在你上次和它通信时)的状态**,也就是远程仓库中的`main`指针所在的位置在**本地仓库的投影**,并不是直接操控远程仓库的分支!

事实上,在checkout到`origin/main`并执行一次提交后,`origin/main`并没有发生移动,**`HEAD`分离了出来并向下提交**.

### `git revert`
这个命令可以帮助理解一下上面提到的内容.一般在远程开发需要回滚时,会使用这个命令而不是`reset`,区别是`reset`会直接倒回上一个提交,而较新的提交则变成了没有指针指向的一个值.但`revert`就会在`HEAD`直接创建一个新的提交以继承.这让我们再推送到远程仓库是就不会出现太大的问题.

### `git clone`
在本地时如果要下载远程已有的库并开始工作,可以使用`clone`语句

    git clone http://github.com/xxx/xxx.git

### `git fetch`
    git fetch http://github.com/xxx/xxx.git

这个命令可以理解为简单的下载,并把`origin/main`更新到远程仓库中`main`的位置**但不会移动本地`main`的位置**.

### `git pull`
其实这个命令等价于

    git fetch http://github.com/xxx/xxx.git
    git merge origin/main

也就是把本地`main`的位置移到和`origin/main`合并后的提交上(我在说什么).

### `git push`
最后一步就是把东西推送到Github上面,这就是`push`.只需执行`git push`.

远程仓库将接收多出来的commit,并且远程仓库中的`main`将被指向这个新的提交.并且`origin/main`也将被指向这个新的提交,所有的分支都更新了!

## 进阶工作流
### 分离`HEAD`

### `push`的各种参数和高级用法

### 一些技巧