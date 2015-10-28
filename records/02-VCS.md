## Web系统概论培训记录（2）

## 版本控制系统（2015.10.26）

记录人：李政邦

### 1. MarkDown介绍
* MarkDown 软件介绍
    * 马克飞象
    * 作业部落
* MarkDown 用处
    * 写简历
    * 写博客
    * 幻灯片

### 2. 前端进阶路程
* 前端基础（HTML，CSS，Javascript）
* 后端基础（如PHP、Python）
* 业界公认的常用开源库(jQuery、bootstrap等)
* 更高级的技术（nodejs等）

### 3. 版本控制系统（VCS）

#### 3.1 为什么使用版本控制系统
* 记录所有版本，易于维护。
* 方便团队协作开发，共享代码。
* 追踪产品的改动历史，便于管理。

[了解更多](http://pm.readthedocs.org/zh_CN/latest/vcs/understanding.html)

#### 3.2 版本控制系统的发展
* 原始VCS：人为管理版本控制 
* 本地VCS

![](http://ww4.sinaimg.cn/large/e62cb413jw1exgodaz2hpj20a30580sn.jpg)

由图，本地有一个版本控制系统，与工作目录关联，有改动都会被记录到版本控制系统中。这在单人工作的时候可以满足需求，但是当项目越来越大，一个人无法完成的时候，在多人开发的背景下，这种本地VCS系统就显得十分鸡肋了。
     
* 集中式VCS（SVN）
    
 ![](http://ww1.sinaimg.cn/large/e62cb413jw1exgogul3rnj20cz09074j.jpg)

上面提到本地VCS无法满足多人作业，这时候，VCS系统做了个小小的调整，把代码仓库从本地提取到服务器端，多人共享服务器，这样就做到了共享代码，而集中式VCS的代表就是SVN。SVN的工作流程就是，Client从Server中检出(checkout)代码，与本地的工作目录关联，然后在本地工作，加代码，修改代码，然后commit，Server中都有详细的记录，而别人修改的代码提交到服务器后本地也可以通过update来把别人的代码加进本地。而如果别人修改的代码和你在本地中修改的代码是同一行，这时候会出现一个冲突(conflict)。此时由本地来决定到底保留哪个修改。

这么一看，似乎整个系统已经基本完善，但是这种架构十分依赖服务器，若服务器崩溃，会导致所有人都无法工作，即使可能会有备份服务器，但是也还是会有局限。
     
* 分布式VCS（Git）

![](http://ww3.sinaimg.cn/large/e62cb413jw1exgohd29h2j20dw0940sx.jpg)

由于集中式分布式过于依赖服务器，这时候分布式VCS系统就出现了，这里没有依赖服务器，当服务器无法正常工作时，Client可以在本地commit，然后在服务器修复后继续commit代码，这是分布式和集中式的本质区别，典型的产品就是Git，Git主要的指令有`status`、`add`、`commit`、`push`、`pull`，工作流程和SVN差不多，先从服务器clone或pull代码，然后在本地修改和commit之后push到服务器，出现conflict的时候也是依据本地来决定保留哪一块。
    
### 4. 交作业的方式
* 进入[FE-Study](https://github.com/ITEC-ELWG/FE-Study)查看里面的部署说明，完成初级任务传送门的任务1。
