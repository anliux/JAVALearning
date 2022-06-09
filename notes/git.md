## 目录
<!--GFM-TOC -->
- [Git简介](#git简介): 起源, 版本控制系统, 集中式, 分布式, 安装, 使用, Unix的哲学是“没有消息就是好消息”
- [Git本地仓库](#git本地仓库): 初始化, 忽略特殊文件, 提交到仓库
- [版本管理](#版本管理): 版本与回退, Git分区, 管理修改, 删除文件
- [Git远程库](#git远程库): 参考, 连接本地主机与Github, 连接本地仓库到Github新仓库, 克隆GitHub仓库到本地文件夹
- [Git分支管理](#git分支管理): 概述分支, 分支操作(增删改查), 合并分支, 合并冲突解决, 分支管理, bug分支, 多人协作, 变基
- [标签](#标签): 概述, 打标签, 查看标签, 删除标签, 上传标签
- [GitHub使用](#github使用): GitHub创建仓库, 参与开源项目
- [设置Git命令行简写](#设置git命令行简写): 简写命令, config文件设置别名
- [Git的图形化工具：SourceTree](#git的图形化工具sourcetree)
- [Git流管理](#git流管理)
- [常用命令](#常用命令)
- [参考教程推荐](#参考教程推荐)
<!--GFM-TOC -->



## Git简介
### 起源：
- 由Linux创始人Linus用 c语言 写成的 分布式版本控制系统
- 2008年，GitHub上线

### 版本控制系统：
- 能自动记录每次文件的改动，还可以让多人协作编辑
- 集中式和分布式的区别是：本地是否有完整的版本库历史

### 集中式版本控制系统：
- 版本库是集中存放在中央服务器的，用自己电脑干活时先从中央服务器取得最新版本，干完活再把自己的成果推送到中央服务器。
- 缺点：必须联网才能工作；中央服务器出问题就翻车。
- 代表：CVS及SVN

### 分布式版本控制系统：
- 不存在中央，每个人的电脑都有完整的版本库，修改完后相互推送即可。更安全。
- 分布式的核心设计：同步，而不是主从
- 代表：Git, BitKeeper,..

### 安装
- 测试：命令行输入git，如果没有显示没有安装，则是安装成功了
- 安装：[安装Git](https://www.liaoxuefeng.com/wiki/896043488029600/896067074338496)

### 使用
- Mac：在终端使用
- Windows：git bash窗口中输入命令使用，或窗口版点击使用

### Unix的哲学是“没有消息就是好消息”
- 如果Git命令后没有任何显示，说明成功
- Git跟踪并管理的是修改，而非文件。

<!--GFM-TOC -->
### [返回目录](#目录)
<!--GFM-TOC -->



## Git本地仓库
### 初始化：
- `git init`：
   - 初始化仓库，把当前文件夹初始化为Git可以管理的仓库，并生成'.git'目录，
   - '.git': 是Git来跟踪管理版本库的，不要随意修改

### 忽略特殊文件
- `.gitignore`: 放在仓库根目录下，用于忽略特殊文件，不跟踪这类文件的改动，不track
   - '.gitignore'文件本身要放到版本库里，并且可以对.其做版本管理
   - 格式：
      - `#`表示注释，可以简单说明是什么类型，如`#JAVA`下添加一下java语言需要忽略的`* class`文件等
      - `!filename`:  <!+文件名>, 把指定文件排除在ignore规则之外 (指可以添加)
   - 检测标准：git status命令是不是说working directory clean。
- `git add -f <filename>`: 强制添加已忽略文件
- `git check-ignore -v Xxxxfilename.xxx`: 检查已有`.gitignore`与指定文件的冲突在哪里
   - 会显示行号和冲突的那条命令
- mac的`.DS_Store`：
  - DS_Store是Mac OS保存文件夹的自定义属性的隐藏文件,如文件的图标位置或背景色,相当于Windows的desktop.ini。
  - 可以放在.gitignore中

### 提交到仓库
- `git status`:
   - 查询当前仓库的状态，会显示绿色已添加未提交、红色已修改未添加的文件
   - 可以设置快捷，如git st
- `git add filename`  / `git add .` / `git add *`: 
   - 把新文件/修改文件添加到仓库，添加成功无显示，可用status确认
- `git commit -m "xxxxxx"`:
   - 把文件提交到仓库，会显示 "1 file changed, 2 insertions(+)"等信息
   - `-m`后面输入的是本次提交的说明，方便从历史记录里查找改动记录
   - 注：第一次commit可能会要求输入自己的邮箱和名字以确认身份，按提示输入即可
      - `git config --global user.email "you@example.com"`
      - `git config --global user.name "Your Name"`
- add和commit的区别：
   - add是添加，commit是提交
   - 可以多次add后，一次性commit

<!--GFM-TOC -->
### [返回目录](#目录)
<!--GFM-TOC -->



## 版本管理 
### 版本与回退
- 版本锚点：
   - 每一次commit提交；每个版本类似于游戏中的每次存档
- `commit id`（版本号):
   - SHA1计算出来的很大的数字，用十六进制表示
   - 跳转不同版本时，版本号没必要写全，前几位就可以了，Git会自动去找
- `git diff filename`:
   - 对比不同，适用于status显示已修改、未添加的情况(status红色)，add后不再有diff结果
   - 结果(Unix通用的diff格式): 加减号显示增加或删除的行，命令行带颜色
   - 应用场景：status显示已修改未提交，但是自己忘记修改了什么不确定是否要提交等的情况
- `git log`:
   - 查看版本详细信息，显示从最近到远的有限次commit信息
   - 输入q可以退出
- `git log --pretty=oneline`:
   - 简化版log，每行显示一条版本信息
   - 会展示很多条版本信息，远比上一个log命令展示的多
- `git log --graph --pretty=oneline --abbrev-commit`: 
   - 显示简化commit ID后的分支图(分支合并情况)
- `HEAD`: 大小写不影响，`^`可表述为倒V
   - HEAD指针：指向当前版本 (当前分支，如master)
   - `HEAD^`:  指向上一个版本; `HEAD^^`: 指向上上个版本; 以此类推
   - `HEAD~100`: 前100个版本写尖容易写不过来，可以用此格式
- `git reset --hard 版本号或HEAD指向`
   - `git reset --hard 1094a`: 只提供版本号前几位(5位左右)，跳转到该版本
   - `git reset --hard HEAD^`: HEAD指向上一个版本，跳转到上一个版本
   - `hard`: ?
- `git reflog`:
   - 查看命令历史，同时会显示版本号

### Git分区：工作区、暂存区、分支
- Git管理的文件分为：工作区，版本库；版本库又分为暂存区stage和暂存区分支master(仓库)
   - 工作区>>>>暂存区>>>>仓库
   - git add把文件从工作区>>>>暂存区，git commit把文件从暂存区>>>>仓库，
- git diff：
   - git diff：查看工作区和暂存区差异 (1-2)
   - git diff --cached：查看暂存区和仓库差异 (2-3)
   - git diff HEAD：查看工作区和仓库的差异 (1-3)
- 图示：
   - ![](https://img2022.cnblogs.com/blog/1265453/202206/1265453-20220606165806467-1321019732.png)

### 管理修改
- Git跟踪并管理的是修改，而非文件。
- `git checkout -- file` / `git restore <file>`:
   - git add的反向命令，撤销工作区修改，即把暂存区最新版本转移到工作区 (2->1)
- `git reset HEAD <file>` / `git restore --staged <file>`:
   - git commit的反向命令，就是把仓库最新版本转移到暂存区 (3->2)
- `git restore`: git 2.23新增命令，用来分担checkout (管理分支等)的各种任务, 会在新版Git中出现在提示部分
   - 建议用此命令

### 删除文件
- `rm filename`: 删除文件，等同于手动在文件夹删除 
- 本地删除文件后，如果确实需要删掉：
   - `git add/rm <file>`删掉该文件，并且`git commit`提交到分支
- 本地删除文件后，如果想要反悔：
   - `git restore <file>`或者`git checkout -- filename`: 撤销这次本地删除
- 本地和暂存库都删除文件后，如果想要反悔：
   - `git restore --staged <file>`退回到上一个状态(即本地删除但未commit)，继续退`git restore <file>`恢复本地已删除文件
- 删除并commit到分支：test.txt
   - `git reset --hard HEAD^`：思路是回退到上一个版本，弊端是可能丢失最新修改的一些数据

<!--GFM-TOC -->
### [返回目录](#目录)
<!--GFM-TOC -->



## Git远程库
### 参考：
  - [廖雪峰Git-远程仓库](https://www.liaoxuefeng.com/wiki/896043488029600/896954117292416)
  - [Mac生成和查看SSH Key](https://blog.csdn.net/u010545480/article/details/122034047)

### 连接本地主机与Github库-Mac版:
- 步骤：
   - 创建SSH Key：`$ ssh-keygen -t rsa -C "自己的email地址xxx@xx.com"`，之后一路回车会生成公钥和秘钥
   - 找到公钥：可以在用户主目录里找到.ssh目录，id_rsa.pub是公钥
   - 登录Github添加SSH公钥: 账号settings -- SSH key -- 添加key
- mac版：
    - 默认状态下找不到ssh文件，由于默认是隐藏状态 ("."开头的文件默认是隐藏文件)  
    - 需要终端进入.ssh文件夹，找到公钥内容并复制，访达里没有
    - 参考：[Mac生成和查看SSH Key](https://blog.csdn.net/u010545480/article/details/122034047): 有Mac相关详细步骤
    - 相关代码：
      ```
      $ cd ~/.ssh
      $ ls
      $ cat id_rsa.pub
      ```

### 连接本地仓库到Github新仓库
- 前提准备：
   - 一个GitHub里的仓库；如果没有，新建：右上角找到“Create a new repo”后创建
   - 找到远程库的SSH地址并复制备用: 仓库主页 -- 绿色code -- 点开小三角有三个地址，其一是SSH地址
- 需要关联的本地仓库目录下：
   - `git remote add origin git@github.com: xxx/xxx.git<此处贴上面找到的远程库SSH地址>`
   - `origin`：远程库的名字，Git默认的叫法；如果关联了多台远程服务器，可以分别命名为其他，否则默认是origin
- 查看远程库信息：
   - `git remote`: 相当于查看远程库列表，只有名字
   - `git remote -v`：查看远程库列表的详细信息，同时列出远程库名和地址、分支等
      - 会显示可以抓取和推送的origin的地址。如果没有推送权限，就看不到push的地址
- 推送本地库到远程库：
   - `git push -u origin master`:
      - `-u`参数: 由于远程库是空的，我们第一次推送master分支时，加上了-u参数，Git会把本地的master分支内容推送的远程新的master分支，同时会把本地的master分支和远程的master分支关联起来，在以后的推送或者拉取时就可以简化命令。
   - `git push / git push origin master`: 加`-u`参数后的推送的简化命令
- 删除远程仓库与本地仓库的关联：
   - 注：“删除”其实是解除了本地和远程的绑定关系；要真正删除远程库，需要到GitHub的后台删除。
   - 先查看远程库信息，后删除
   - `git remote rm origin<此处为远程库的名字>`

### 克隆GitHub仓库到本地文件夹
- #### 备注：
   - 先有远程库的情况下，可以直接clone后使用
- #### clone和download的区别：
    - 采用git clone的项目：
       - 包含.git目录，这里面有历史版本信息
       - 会先在你当前选择的文件夹下建立一个本地仓库，然后再clone服务器上的git工程，这个文件夹下直接进行pull或者push等操作。
    - 采用下载zip文件：
       - 没有版本历史信息的，只是当前分支的最新版本
       - 会切断和git仓库的代码联系，得到的是一个单纯的项目文件，后期无法再对仓库进行pull和push等操作
    - 参考：
       - [从gitlab或者github采用git clone和download zip的区别](https://blog.csdn.net/u011250186/article/details/103595325)
       - [git直接打包下载和使用git clone进行项目拷贝的区别](https://www.csdn.net/tags/Mtjagg3sNDEyMDktYmxvZwO0O0OO0O0O.html)
- #### 克隆步骤：
   - 命令行进入正确路径下
   - `git clone + 目标远程库的地址(推荐SSH地址)`
   - 成功的话：会展示clone进度，最后显示done

<!--GFM-TOC -->
### [返回目录](#目录)
<!--GFM-TOC -->



## Git分支管理 
### 概述分支：
- Git鼓励使用分支完成某个任务，合并后再删掉分支，这和直接在master分支上工作效果是一样的，但过程更安全。
- git的分支最终是要合并到主干的
- HEAD: 指向当前分支，然后分支指向某时间线
  - HEAD -> master -> 时间线，或HEAD -> dev -> 某时间线 
  - 创建新分支dev后(新分支基于之前的分支如master)，将HEAD指向dev，即当前分支由master变为dev
  - 合并dev与master：即当前HEAD指向的master指向dev的当前提交，就完成了合并
- 快速切换的奥义：
   - 仅仅是指针指向的切换，所以快
- 对于所有分支而言， 工作区和暂存区是公共的。
   - 所以会在某分支修改文件后，切换到其他分支，查看状态发现还在的情况；
   - [git 切换分支时会把未add或未commit的内容带过去](https://blog.csdn.net/stpeace/article/details/84351160)
   - 一般先提交后切换分支

### 分支操作：(增删查改)
- `git branch`: (查) 列出所有分支，其中带星号的分支是当前分支
- `git branch <name>`: (增) 创建分支
- `git checkout <name>`或者`git switch <name>`: (改) 切换分支
- `git checkout -b <name>`或者`git switch -c <name>`: (增+改) 创建+切换分支，相当于两步brance和checkout
- `git branch -d <name>`: (删) 删除指定分支 (不能删除当前分支，需要先切换到其他分支)
   
### 合并分支
- `git merge <name>`: (先切换到需要保留的分支)，合并某指定分支到当前分支
   - `Fast-forward`: 如果没有冲突，合并后提示的信息，表示这次合并是“快进模式” (并不是每次合并都能Fast-forward)
- `git merge --no-ff -m "merge with no-ff" dev`: 合并时强制禁用Fast forward模式，会在merge时生成一个新的commit，可从分支历史上就可以看出分支信息
   - ff模式合并后：不显示分支图，只在某处标记曾经出现过一个某某分支，不直观
   - no ff模式合并后：分支图历史有分支，能看出来曾经做过合并
   - `--no-ff`参数，表示禁用Fast forward; `-m "xx"`为添加commit note
- ff模式图示：
  - ![](https://img2022.cnblogs.com/blog/1265453/202206/1265453-20220607172209148-96579727.png)
  - ![](https://img2022.cnblogs.com/blog/1265453/202206/1265453-20220607172710367-2036978058.png)
- no ff模式图示：
  - ![](https://img2022.cnblogs.com/blog/1265453/202206/1265453-20220607172509664-938435040.png)
  - ![](https://img2022.cnblogs.com/blog/1265453/202206/1265453-20220607172842827-2118204606.png)

### 合并冲突解决
- 冲突：
   - 当两个分支都对同一行进行了修改并commit，且修改不同时，合并的时候会产生冲突
   - 示例：dev对readme文件加一行并commit，随后切换到master分支，同样对readme文件加不同的一行，并commit；此时如果合并dev分支到master分支，就会冲突。
   - 图示：![](https://img2022.cnblogs.com/blog/1265453/202206/1265453-20220607105211812-24796839.png)
- 解决冲突：
   - 直接merge：会显示合并失败 (Merge conflict in xxx.txt)；
   - 查看status：会显示冲突文件 (both modified: xxx-filename)
   - 解决冲突：vi编辑冲突文件
     - 会看到冲突位置已经标出，可以手动查看并修改为最终版本，删掉标识，保存退出
     - 注：Git用 `<<<<<<<`，`=======`，`>>>>>>>` 标记出不同分支的内容
   - 此时直接merge还是失败，提示需要`git add/rm <file>`
   - 再次查看状态(both modified..)，之后正常add-commit此文件 
      - 这里add-commit相当于将手动解决冲突后完成了merge这一步
   - `git log --graph --pretty=oneline --abbrev-commit`: 显示简化commit ID后的分支图(分支合并情况)
      - graph：显示图
      - abbrev-commit：简单显示commit ID
   - 后面不需要再merge了，解决冲突后commit，相当于已经将其他分支的内容手动合并到了当前分支 
      - 此时merge: Already up to date 
      - 注：此时其他分支的冲突文件仍是原样(不是解决冲突时修改为的样子)，只是合并这一步的冲突解决了
   - 删除已合并分支：`git branch -d  其他分支名`
     - 注：`git branch -D <name>`: 强行删除一个没有被合并过的分支，用小写d会删除失败
- 合并操作 (merge)：
   - 当Git无法自动合并分支时，就必须首先解决冲突。解决冲突后，再提交，合并完成。
      - 解决冲突就是把Git合并失败的文件手动编辑为我们希望的内容，再提交
   - 只对当前所在分支产生影响：无论是否存在冲突，合并之后，另一个分支都不会发生变化
   - 二进制文件冲突就是二选一，你决定留下哪个就是哪个，没有合并一说
   - 一般合并完成后，以主线版本为主，这时可以删掉其他分支(可能与主线版本不一致)，然后在主线分支基础上新建其他分支

### 分支管理
- git有个最佳实践：
   - master是主分支，用来做正式发布版之后的保留历史，
   - dev用来做正常开发，
   - 多个feature用来做某些特性功能，
   - release用来做发布版历史，每次发布都是用release打包，
   - hotfix用来做发布版之后的一些及时迭代修复bug的工作。
- 团队合作的分支看起来就像这样：
   - ![](https://img2022.cnblogs.com/blog/1265453/202206/1265453-20220607173414674-1094418243.png)

### bug分支
- 场景：
  - 正在dev开发分支营业时，发现master分支有个bug急需处理；
  - 在还没有干完活的情况下，未commit的已修改文件会在status显示到别的分支
  - 可以先把dev分支的活存起来，先去master，修完bug回来继续干存起来的活
  - 注：相当于暂存在某个栈里，用时弹出
- stage命令：
  - `git stash`: 当前工作现场“储藏”起来，等以后恢复现场后继续工作
  - `git stash list`: 列出已存储内容
  - 恢复法1：`git stash apply`恢复但stash内容并不删除，需要用`git stash drop`来删除
    - `git stash apply stash@{0}`: 如果多次stash，可以指定恢复哪条存储内容
  - 恢复法2：`git stash pop`，恢复的同时把stash内容也删了
- `git cherry-pick commit ID`: 在当前分支上修复在其他分支修复的同样的bug
   - 场景：如果在master分支上修复了一个bug101，而同样的bug，想要在dev分支上也修复，
   - 我们只需要把fix bug101这个提交所做的修改“复制”到dev分支。
   - 注意：只复制fix bug101这个提交所做的修改，并不是把整个master分支merge过来。(dev分支可能比master分支新好多)
   - 当然，同样滴，也可以在dev分支上修复bug，然后在master分支上“重放”

### 多人协作
#### 注：多人协作：势必涉及到远程库

#### 流程
- 首先，可以试图用git push origin <branch-name>推送自己的修改；
- 如果推送失败，则因为远程分支比你的本地更新，需要先用git pull试图合并；
- 如果合并有冲突，则解决冲突，并在本地提交；
- 没有冲突或者解决掉冲突后，再用git push origin <branch-name>推送就能成功！
- 如果git pull提示no tracking information，则说明本地分支和远程分支的链接关系没有创建
   - 用命令`git branch --set-upstream-to <branch-name> origin/<branch-name>`

#### 通常涉及的命令
- 查看远程库信息，使用git remote -v；
- 本地新建的分支如果不推送到远程，对其他人就是不可见的；
- 从本地推送分支，使用git push origin branch-name，如果推送失败，先用git pull抓取远程的新提交；
- 在本地创建和远程分支对应的分支，使用`git checkout -b branch-name origin/branch-name`，本地和远程分支的名称最好一致；
- 建立本地分支和远程分支的关联，使用`git branch --set-upstream branch-name origin/branch-name`；
- 从远程抓取分支，使用git pull，如果有冲突，要先处理冲突。

### 变基
- `git rebase`: 把本地未push的分叉提交历史整理成直线 (git log时的分支图)
   - 使得我们在查看历史提交的变化时更容易，因为分叉的提交需要三方对比
- 注：只对尚未推送或分享给别人的本地修改执行变基操作清理历史； 从不对已推送至别处的提交执行变基操作

<!--GFM-TOC -->
### [返回目录](#目录)
<!--GFM-TOC -->



## 标签 
### 概述
- tag就是一个让人容易记住的有意义的名字，它跟某个commit绑在一起。
- 标签是指向commit的死指针，分支是指向commit的活指针
- 标签总是和某个commit挂钩。如果这个commit既出现在master分支，又出现在dev分支，那么在这两个分支上都可以看到这个标签

### 打标签
- `git tag <name>`: 默认标签是打在最新提交的commit上的 (默认为HEAD)
- `git tag 标签名称 commit ID`: 将标签打在指定commit上，包含历史commit
   - 例如：`git tag v0.9 f52c633`
- `git tag -a <tag name> -m "<说明文字>" commit ID`: 创建带有说明的标签，用`-a`指定标签名，`-m`指定说明文字
   - 例如：`git tag -a v0.1 -m "version 0.1 released" 1094adb`

### 查看标签
- `git tag`: 列出所有标签名，注意是按字母排序列出，与时间无关
- `git show <tagname>`: 查看标签信息，如commit信息，作者，时间，说明文字等

### 删除标签
- `git tag -d <tagname>`: 在本地删除指定标签
- `git push origin :refs/tags/<tagname>`: 删除一个远程标签
   - 在'.git'文件的路径refs/tags下存储了所有的tags信息
   - 冒号在这里，前面为空，即将一个“空”的标签推送给对应的标签，即删除

### 上传标签
- `git push`: 不会传送标签到远程仓库服务器上, 在创建完标签后你必须显式地推送标签到共享服务器上。 
   - 这个过程就像共享远程分支一样
- `git push origin <tagname>`: 推送本地的指定分支到远程库
- `git push origin --tags`：一次性推送全部尚未推送到远程的本地标签
   - 或者`git push origin master --tags`：可以把全部的标签打上去

<!--GFM-TOC -->
### [返回目录](#目录)
<!--GFM-TOC -->



## GitHub使用
### GitHub创建仓库
- 登录到GitHub账号
- 加号 -- 新建仓库
- 新建页面：设置仓库名、是否公开，选择自动生成readme/.gitignore/协议等
- 确认创建

### 参与开源项目
- 在GitHub上，可以任意Fork开源仓库，然后从自己账号下clone到本地后进行操作和上传；
- 自己拥有Fork后的仓库的读写权限：
   - 一定要从自己的账号下clone仓库，这样你才能推送修改
- 可以推送pull request给官方仓库来贡献代码：
   - 流程：干活 -- 干完活后，往自己的仓库推送 -- 发起pull request给官方仓库，等对方接受

<!--GFM-TOC -->
### [返回目录](#目录)
<!--GFM-TOC -->



## 设置Git命令行简写
- `git config --global alias.xx abcde`: 全局设置abcde简写为xx
    - `--global`参数是全局参数，也就是这些命令在这台电脑的所有Git仓库下都有用。
    - 加上 `--global`是针对当前用户起作用的，如果不加，那只针对当前的仓库起作用
- 示例：
    - `git config --global alias.st status`: 全局设置status简写为st
    - `git config --global alias.co checkout`: 全局设置checkout简写为co
    - `git config --global alias.ci commit`: 全局设置commit简写为ci
    - `git config --global alias.br branch`: 全局设置branch简写为br
    - `git config --global alias.unstage 'reset HEAD'`: 简写的不是单个单词时，可以加引号区分
- 配置文件位置：
  - `.git/config`: 每个仓库的Git配置文件
  - `隐藏文件.gitconfig`: 当前用户的Git配置文件放在用户主目录下
  - `[alias]  last = log -1 // ....`: 配置文件中会写简写前命令和别名
  - 可以直接在配置文件中修改别名：
    - `cat .gitconfig`: 查看用户git配置文件
    - `cat .git/config`: 查看仓库的.git配置文件

<!--GFM-TOC -->
### [返回目录](#目录)
<!--GFM-TOC -->



## Git的图形化工具：SourceTree
- 可以官网下载使用，更直观

<!--GFM-TOC -->
### [返回目录](#目录)
<!--GFM-TOC -->



## Git流管理
- 参考：[Git工作流-千锋教育(来自b站)](cnblogs.com/anliux/p/9924093.html)

<!--GFM-TOC -->
### [返回目录](#目录)
<!--GFM-TOC -->



## 常用命令
### 文件相关命令：
- `ls`: 查看当前路径下的文件
- `ls -ah`: 列出包括隐藏文件在内的所有文件
- `ls -la`: 列出所有文件的详细信息，包括隐藏文件和文件权限等
- `mkdir filename`: 当前路径下创建名为filename的文件夹
- `cd xx`: 进入某某文件夹
- `pwd`: 显示当前路径
- `cat xx`: 查看某某文件的具体内容
- `rm filename`: 删除文件，等同于手动在文件夹删除 

### vim简单编辑
- `vi/vim filename`: 进入filename的文件编辑状态; 如果是新文件键入并保存，效果相当于新建文件并键入内容
- 键盘按`i`或者`o`：进入编辑模式 (i: insert)
- `ESC`: 编辑完毕之后，esc退出编辑模式
- `shift+;` : 进入末行模式，然后可以输出wq等退出vim
- `wq`: 保存并退出，w写入，q退出
- `e!`: 强制还原到最原始的状态
- `wq!`: 强制保存并退出，感叹号为强制，后可接w或q

### Git相关：
- `git init`：初始化仓库
- `.gitignore`: 放在仓库根目录下，用于忽略特殊文件，不跟踪这类文件的改动，不track
      - `#`表示注释，可以简单说明是什么类型，如`#JAVA`下添加一下java语言需要忽略的`* class`文件等
      - `!filename`:  <!+文件名>, 把指定文件排除在ignore规则之外 (指可以添加)
- `git add -f <filename>`: 强制添加已忽略文件 (添加在.gitignore文件中的文件)
- `git check-ignore -v Xxxxfilename.xxx`: 检查已有`.gitignore`与指定文件的冲突在哪里
   - 会显示行号和冲突的那条命令
- `git status`: 查看状态，常用 (可设置快捷，如git st)
- `git add filename`  / `git add .` / `git add *`: 添加有更新的文件(status查看变红的文件)，星号可以通配各种文件，一键添加
- `git commit -m "xx"`: 提交到仓库 (注：可多次add后一次性commit)

- `git diff filename`: 对比已修改、未添加文件的不同(status红色的文件，绿色diff无结果)
   - git diff：查看工作区和暂存区差异(1-2)
   - git diff --cached：查看暂存区和仓库差异(2-3)
   - git diff HEAD：查看工作区和仓库的差异(1-3)
- `git log`: 查看版本详细信息，显示有限条最新版本，按q退出
- `git log --pretty=oneline`: 简化版log，每行显示一条版本信息
- `git log --graph --pretty=oneline --abbrev-commit`: 显示简化commit ID的分支图(分支合并情况)
- `git reset --hard 版本号或HEAD指向`
   - `HEAD`: 指向当前版本的指针，可用`HEAD^`或`HEAD~100`回退版本
- `git reflog`: 查看命令历史，同时会显示版本号

- `git restore <file>` / `git checkout -- file`:
   - git add的反向命令，撤销工作区修改，即把暂存区最新版本转移到工作区 (2->1)
-  `git restore --staged <file>` / `git reset HEAD <file>`:
   - git commit的反向命令，就是把仓库最新版本转移到暂存区 (3->2)
- `git restore`: git 2.23新增命令，用来分担checkout (管理分支等)的各种任务, 会在新版Git中出现在提示部分
   - 建议用此命令

- `origin`: 远程库的默认名字
- `git remote`: 相当于查看远程库列表，只有名字
- `git remote -v`：查看远程库列表的详细信息，同时列出远程库名和地址、分支等

- `git remote add origin git@github.com: xxx/xxx.git<此处贴上面找到的远程库SSH地址>`：本地仓库路径下，关联到目标远程库
- `git push -u origin master`：首次推送本地库到远程库，加参数`-u`
- `git push / git push origin master`: 加`-u`参数后的推送的简化命令
- `git pull <remote> <branch>`: 拉取远程库代码，push的格式同
- `git remote rm origin<此处为远程库的名字>`：删除远程库与本地仓库的关联，如删除origin
- `git clone + 目标远程库的地址(推荐SSH地址)`：本地正确路径下使用此命令，会克隆包含`.git`的远程库到此路径下

- `git branch`: (查) 列出所有分支，其中带星号的分支是当前分支
- `git branch <name>`: (增) 创建分支
- `git checkout <name>`或者`git switch <name>`: (改) 切换分支
- `git checkout -b <name>`或者`git switch -c <name>`: (增+改) 创建+切换分支，相当于两步brance和checkout
- `git checkout -b branch-name origin/branch-name`: (远程) 在本地创建和远程分支对应的分支，本地和远程分支的名称最好一致；
- `git branch --set-upstream branch-name origin/branch-name`: (远程) 建立本地分支和远程分支的关联；
- `git merge <name>`: 合并某指定分支到当前分支
   - `Fast-forward`: 合并后提示的信息，表示这次合并是“快进模式” (并不是每次合并都能Fast-forward)
- `git merge --no-ff -m "merge with no-ff" dev`: 合并时强制禁用Fast forward模式，会在merge时生成一个新的commit，可从分支历史上就可以看出分支信息
   - `--no-ff`参数，表示禁用Fast forward; `-m "xx"`为添加commit note
- `git branch -d <name>`: (删) 删除指定分支 (不能删除当前分支，需要先切换到其他分支)
- `git branch -D <name>`: (删) 强行删除一个没有被合并过的分支，用小写d会删除失败

- git rebase`: 变基，把本地未push的分叉提交历史整理成直线 (git log时的分支图)
   - 注：只对尚未推送或分享给别人的本地修改执行变基操作清理历史； 从不对已推送至别处的提交执行变基操作

- `git stash`: 当前工作现场“储藏”起来，等以后恢复现场后继续工作
   - 注：stash看起来像一个存储栈，需要弹出等
- `git stash list`: 列出已存储内容
- `git stash apply`：恢复但stash内容并不删除，需要用`git stash drop`来删除
   - `git stash apply stash@{0}`: 如果多次stash，可以指定恢复哪条存储内容
- `git stash drop`: 删除stash存储区的内容，再次stash list查看会发现删掉了
- `git stash pop`：恢复的同时把stash内容也删了
- `git cherry-pick commit ID`: 在当前分支上复现在其他分支修复的同样的bug 
    - 例如在master分支修改bug101后在dev分支复现修复bug101的动作，而不会merge整条master分支

- `git tag <name>`: 默认标签是打在最新提交的commit上的 (默认为HEAD)
- `git tag 标签名称 commit ID`: 将标签打在指定commit上，包含历史commit
- `git tag -a <tag name> -m "<说明文字>" commit ID`: 创建带有说明的标签，用`-a`指定标签名，`-m`指定说明文字
- `git tag`: 列出所有标签名，注意是按字母排序列出，与时间无关
- `git show <tagname>`: 查看标签信息，如commit信息，作者，时间，说明文字等
- `git tag -d <tagname>`: 在本地删除指定标签
- `git push origin :refs/tags/<tagname>`: 删除一个远程标签
- `git push origin <tagname>`: 推送本地的指定分支到远程库
   - `git push`: 命令并不会传送标签到远程仓库服务器上,在创建完标签后你必须显式地推送标签到共享服务器上。 这个过程就像共享远程分支一样
- `git push origin --tags`：一次性推送全部尚未推送到远程的本地标签
   - 或者`git push origin master --tags`：可以把全部的标签打上去

- `git config --global alias.xx abcde`: 全局设置abcde简写为xx
   - 注：可以直接在配置文件中修改alias的内容，与命令作用相同

<!--GFM-TOC -->
### [返回目录](#目录)
<!--GFM-TOC -->



## 参考教程推荐：
- [廖雪峰：Git教程](https://www.liaoxuefeng.com/wiki/896043488029600)
- [远古学习笔记](https://www.cnblogs.com/anliux/p/9825219.html)

<!--GFM-TOC -->
### [返回目录](#目录)
<!--GFM-TOC -->



### END
