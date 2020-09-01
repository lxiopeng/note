# Git&GitHub学习笔记

[toc]

### 一、版本控制

#### 1.集中式版本控制工具：CVS,**SVN**,VSS...

#### 2.分布式版本控制工具：**Git**,Mercurial,Bazaar,Darcs...

#### 3.版本控制工具应具有的功能：

3.1**协同开发**

3.1.1 多人并行不悖的修改服务器端的同一个文件。
3.2**数据备份**
3.2.1不仅保存目录和文件的当前状态，还能够保存每一个提交过的历史状态。
3.3**版本管理**
3.3.1在保存每一个版本的文件信息的时候要做到不保存重复数据，以节约存储空间，提高运行效率。这方面 SVN 采用的是增量式管理的方式，而 Git 采取了文件系统快照的方式。
3.4**权限控制**
3.4.1 对团队中参与开发的人员进行权限控制。
3.4.2对团队外开发者贡献的代码进行审核——Git 独有。
3.5**历史记录**
3.5.1 查看修改人、修改时间、修改内容、日志信息。
3.5.2将本地文件恢复到某一个历史状态。
3.6**分支管理**
3.6.1允许开发团队在工作过程中多条生产线同时推进任务，进一步提高效率。

### 二、Git

#### 1.官网：<https://git-scm.com>

#### 2.Git的优势

2.1大部分操作在本地完成，不需要联网

2.2完整性保证

2.3尽可能添加数据，而不是修改数据

2.4分支操作非常快捷流畅

2.5与Linux命令全面兼容

#### 3.Git安装：一直下一步就可以

#### 4.Git结构

工作区（写代码）++>git add ++>暂存区（临时存储）++>本地库（历史版本）

![Git结构](https://github.com/lxiopeng/image/raw/master/Git/gitjiegou.png)

#### 5.代码托管中心（维护远程库）

5.1局域网环境下：GitLab

5.2外网环境下：GitHub,码云

#### 6.本地库和远程库

6.1团队内部协作

![脱队内部协作](https://github.com/lxiopeng/image/raw/master/Git/tuanduineixiezuo.png)

6.2跨团队协作

![跨团队协作](https://github.com/lxiopeng/image/raw/master/Git/kuaituanduixiezuo.png)

#### 7.Git命令行操作

7.1本地库初始化：git init

7.2设置签名

7.2.1设置签名的作用：区分不同开发人员的身份（这里设置的签名和登录远程库的账号密码没有任何关系）

7.2.2设置签名语法格式：

- 项目级别/仓库级别：尽在当前本地库范围有效
  - git config user.name tom_pro
  - git config user.email goodMorning_pro@qq.com
  - 签名信息保存的位置：.git/config文件
- 系统用户级别：登录当前操作系统的用户范围
  - git config --global user.name tom_glb
  - git config --global user.email goodMorning_glb@qq.com
  - 签名信息保存的位置：.gitconfig文件
- 优先级：就近原则（项目级别优先于用户级别，二者都有是采用项目级别，只有一个时，有哪个用哪个，二者都没有不允许）
- 实际开发的时候设置系统用户级别的就可以了，如果某个项目有特殊需求，可以设置项目级别的签名

#### 8.Git基本操作

8.1查看工作区，暂存区状态：git status

8.2将工作区的“新建/修改”添加到暂存区：git add 文件名

8.2.1将暂存区文件撤回：git rm --cached 文件名

8.3将暂存区的内容提交到本地库：git commit - m "commit message" [file name]

8.4查看历史记录：git log （多屏显示控制方式：空格向下翻页，b向上翻页，q退出）

8.4.1：git log --pretty=oneline：每条记录显示一行，哈希码显示全部

8.4.2：git log --oneline：每条记录显示一行，哈希码显示一部分

8.4.3：git reflog：每条记录显示一行，哈希码显示一部分，显示HEAD@{移动到当前版本需要的步数}

8.5前进后退:本质，移动HEAD节点

8.5.1基于索引值操作[推荐]

- git reset --hard [局部索引值]
- 表示退到某一步

8.5.2使用^符号：只能后退

- git reset -- hard HEAD^
- 一个^后退一步，n个后退n步

8.5.3使用~符号：只能后退

- git reset --hard HEAD~n
- b表示后退n步

8.5.4reset三个参数对比

- --soft参数：仅仅在本地库移动HEAD指针
- --mixed参数：在本地库移动HEAD指针，重置暂存区
- --hard参数：在本地库移动HEAD指针，重置暂存区，重置工作区

8.6删除（rm 文件名 之后add，commit）文件并找回：

8.6.1前提：删除前，文件存在时的状态提交到了本地库

8.6.2操作：get reset --hard[指针位置]

- 删除操作已经提交到本地库：指针位置指向历史记录

- 删除操作尚未提交到本地库：指针位置使用 HEAD 

8.7比较文件差异

8.7.1将工作区的文件和暂存区进行比较：git diff [文件名]

8.7.2将工作区中的文件和本地库历史记录比较：git diff \[本地库中的历史版本][文件名]

#### 9.分支管理

![分支管理](https://github.com/lxiopeng/image/raw/master/Git/gitfenzhi.png)

9.1什么是分支？在版本控制过程中，使用多条线同时推进多个任务

9.2分支的好处

9.2.1同时推进多个功能开发，提高开发效率

9.2.2各个分支在开发过程中，如果某一个分支开发失败，不会对其他分支有任
何影响。失败的分支删除重新开始即可。

9.3分支操作

9.3.1创建分支：git branch [分支名]

9.3.2查看分支：git branch -v

9.3.3切换分支：git checkout [分支名]

9.3.4合并分支

- 第一步：切换到接受修改的分支（被合并，增加新内容）上
  git checkout [被合并分支名]
- 第二步：执行 merge 命令
  git merge [有新内容分支名]
- 解决冲突
  - 第一步：编辑文件，删除特殊符号
  -  第二步：把文件修改到满意的程度，保存退出
  - 第三步：git add [文件名]
  - 第四步：git commit -m "日志信息"（ 注意：此时 commit 一定不能带具体文件名）

#### 10.Git基本原理

10.1哈希：哈希是一个系列的加密算法，各个不同的哈希算法虽然加密强度不同，但是有以下几个共同点：
10.1.1不管输入数据的数据量有多大，输入同一个哈希算法，得到的加密结果长度固定。
10.1.2哈希算法确定，输入数据确定，输出数据能够保证不变
10.1.3哈希算法确定，输入数据有变化，输出数据一定有变化，而且通常变化很大
10.1.3哈希算法不可逆
10.1.4Git 底层采用的是 SHA-1 算法，哈希算法可以被用来验证文件。原理如下（Git 就是靠这种机制来从根本上保证数据完整性的）：

![Git基本原理](https://github.com/lxiopeng/image/raw/master/Git/githash.png)

10.2Git保存版本的机制

10.2.1集中式版本控制工具的文件管理机制：以文件变更列表的方式存储信息。这类系统将它们保存的信息看作是一组基本文件和每个文件随时间逐步累积的差异。原理如下：

![集中式版本控制机制](https://github.com/lxiopeng/image/raw/master/Git/jizhongshibanbenkongzhi.png)

10.2.2Git的文件管理机制：Git 把数据看作是小型文件系统的一组快照。每次提交更新时 Git 都会对当前的全部文件制作一个快照并保存这个快照的索引。为了高效，如果文件没有修改，Git 不再重新存储该文件，而是只保留一个链接指向之前存储的文件。所以 Git 的工作方式可以称之为快照流。原理如下：

![Git文件管理机制](https://github.com/lxiopeng/image/raw/master/Git/gitbanbenkongzhi.png)

10.3Git分支管理机制

### 三、GitHub

#### 1.注册账号：Email地址，GitHub账号

#### 2.创建远程库：New Repository

#### 3.创建远程库地址别名

3.1查看当前所有远程库地址别名：git remote -v

3.2添加远程库地址别名：git remote add \[别名] [远程地址]

#### 4.推送：git push \[别名] [分支名]

#### 5.克隆

5.1git clone [远程地址]（完整的把远程库下载到本地，创建origin远程地址别名，初始化本地库）

#### 6.团队成员邀请

6.1github：Settings++>Collaborators++>选择仓库名++>Add collaborator++>Copy invite link++>发给要邀请的成员

#### 7.拉取（pull = fetch+merge）

7.1git fetch \[远程库地址别名] [远程库分支名]

7.2git merge [远程库地址别名/远程分支名]

7.3git pull \[远程库地址别名] [远程分支名]

#### 8.解决冲突

8.1如果不是基于 GitHub 远程库的最新版所做的修改，不能推送，必须先拉取

8.2拉取下来后如果进入冲突状态，则按照“分支冲突解决”操作解决即可

#### 9.跨团队合作

9.1Fork:复制项目到自己的远程库

9.2克隆到本地修改，然后推送到远程库

9.3Pull requests

9.4对话

9.5审核代码

9.6合并代码

9.7将远程库修改拉取到本地，解决冲突，重新提交到远程库

9.8widows 凭据管理

#### 10.SSH登录

10.1进入当前用户家目录：$ cd ~

10.2删除.ssh目录：$ rm -rvf .ssh

10.3运行命令生成.ssh密钥目录：$ssh-keygen-rsa -C 远程库登录的邮箱账号

10.4进入.ssh目录查看文件列表：$ cd .ssh	$ ls - lF

10.5查看id_rsa.pub文件：$ cat id_rsa.pub

10.6复制id_rsa.pub文件内容，登录GitHub，点击用户头像++>Settings-->SSH and GPG keys++>New SSH Key++>粘贴复制的密钥信息++>回到Git bash创建远程地址别名：git remote add origin_ssh 远程库的SSH地址（本地库名/.git文件）

### 四、eclipse&Git

#### 1.工程初始化为本地库

1.1工程++>右键++>Team++>Share Project++>Git++>勾选Use or create repository in parent folder of project++>选中项目++>Create Repository++>Finish

#### 2.eclipse忽略文件：https://github.com/github/gitignore

2.1忽略.classpath文件,.project文件,.settings目录下所有文件，还有target文件

2.2编辑本地.gitignore文件，文件名任意：Java.gitignore

2.3在.gitconfig文件中引入上述文件

[core]

​	excludesfile = C:/Users/Lenovo/Java.gitignore(必须是正斜线)

#### 3.高版本克隆操作

3.1File++>Import++>Projects from Git++>Clone Url(到远程库复制地址)++>++>指定工程导入方式：import as general project++>

项目右键++>config++>convert to

#### 4.低版本克隆操作

4.1导入项目是导入到工作空间以外的目录，剩下的操作一样

#### 5.解决冲突

5.1冲突文件→右键→Team→Merge Tool，修改完成后正常执行 add/commit 操作即可

#### 6.分支操作

6.1创建分支：右键++>Team++>Switch To++>New Branch++>填写分支名称Branch name（勾选check out new branch）

6.2切换分支审查代码：右键++>Team++>Switch To++>Other++>选择分支，点击Check out++>点击Check out as New Local Branch

6.3检出远程分支

6.4切换回master分支：右键++>Team++>Switch To++>master

6.5合并分支：Merge++>选择分支

6.6合并成功后推送到远程

#### 7.git相关图标

7.1黄色小圆柱，后面没有其他符号，表示没有未追踪文件
7.2黄色小圆柱，后面有一个>符号：表示含有未追踪文件
7.3蓝色问号，表示未追踪
7.4什么图标都没有表示忽略文件
7.5黑色星号图标表示添加到了暂存区
7.6绿色加号表示已经追踪的文件

### 五、Git工作流：在开发中使用Git的方式

#### 1.集中式工作流

像 SVN 一样，集中式工作流以中央仓库作为项目所有修改的单点实体。所有修改都提交到 Master 这个分支上。这种方式与 SVN 的主要区别就是开发人员有本地库。Git 很多特性并没有用到。

![集中式工作流](https://github.com/lxiopeng/image/raw/master/Git/jizhongshigongzuoliu.png)

#### 2.GitFlow工作流

Gitflow 工作流通过为功能开发、发布准备和维护设立了独立的分支，让发布迭代过程更流畅。严格的分支模型也为大型项目提供了一些非常必要的结构。

2.1分支种类

2.1.1主干分支 master，主要负责管理正在运行的生产环境代码。永远保持与正在运行的生产环境完全一致。

2.1.2开发分支 develop，主要负责管理正在开发过程中的代码。一般情况下应该是最新的代码。

2.1.3bug 修理分支 hotfix，主要负责管理生产环境下出现的紧急修复的代码。 从主干分支分出，修理完毕并测试上线后，并回主干分支。并回后，视情况可以删除该分支。

2.1.4准生产分支（预发布分支） release，较大的版本上线前，会从开发分支中分出准生产分支，进行最后阶段的集成测试。该版本上线后，会合并到主干分支。生产环境运行一段阶段较稳定后可以视情况删除。

2.1.5功能分支 feature，为了不影响较短周期的开发工作，一般把中长期开发模块，会从开发分支中独立出来。 开发完成后会合并到开发分支。

2.2GitFlow工作流举例

![GitFlow工作流](https://github.com/lxiopeng/image/raw/master/Git/gitflowgongzuoliu.png)

#### 3.Forking  工作流

3.1Forking 工作流是在 GitFlow 基础上，充分利用了 Git 的 Fork 和 pull request 的功能以达到代码审核的目的。更适合安全可靠地管理大团队的开发者，而且能接受不信任贡献者的提交。

![Forking工作流](https://github.com/lxiopeng/image/raw/master/Git/forkgongzuoliu.png)

#### 4.Gitlab服务器搭建

### 六、linux常用命令

1：ll	列出当前目录下所有文件

2：ls -lA	列出当前目录下所有文件（包括隐藏目录）

3：ls -l|less	管道操作，分屏查看

4：cd 目录名	进入某个目录

5：cd ..	进入上级目录

6：pwd	查看前一级目录

7：cat 文件名	打开文件

8：vim 文件名	创建/修改文件

9：vim编辑器中，点i键进入编辑模式

10：vim编辑中，点esc，输入:wq退出vim编辑器，输入set nu设置行号

11：git bash中选中即复制，shift+insert粘贴

12：mkdir 文件名	创建文件

### 七、提交 commit 书写规范

提交文件时，提交信息是必须要写的，要能看出来本次提交做了什么，格式如下：

- type(scope):subject
- type：用于说明提交（commit）的类别，规定为以下几种：

1. feat：新增功能；
2. fix：修复bug；
3. docs：修改文档；
4. refactor：代码重构，未新增任何功能和修复任何bug；
5. build：改变构建流程，新增依赖库、工具等（例如webpack修改）；
6. style：仅仅修改了空格、缩进等，不改变代码逻辑；
7. perf：改善性能和体现的修改；
8. chore：非src和test的修改；
9. test：测试用例的修改；
10. ci：自动化流程配置修改；
11. revert：回滚到上一个版本；

- scope：【可选】用于说明commit的影响范围
- subject：commit的简要说明，尽量简短