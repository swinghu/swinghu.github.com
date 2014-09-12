---
layout: post
title: git中的merge命令式如何实现和工作的？
description: visual studio 快捷键 shortcut key
category: blog
---


How does Git merge work?
Git的merge操作是如何实现的？

想象一下有如下情形：代码库中存在两个分支，并且每个分支都进行了修改，最后你想要将其中的一个分支合并到其他的分支中。

那么要问合并的处理过程是怎么样的呢？Git是对每个分支，依据分支的历史数据按照序列化操作，还是它只是合并每个分支里文件的最后版本？这是一个问题，我想对git的merge操作有必要进行分析一下。

回忆一下，我们知道Git的版本库内部结构是以有向无环图（directed acyclic graph）组织起来的：每一次commit都会生成一个版本树的快照（snapshot），并且该快照保存了一个指向其父节点（该分支的最近上一次的提交快照）的引用（通常当前提交只有一个父节点，但是初试提交快照没有父节点，而一次合并（merge）操作有2个或多个父节点）。就像这样，每次提交都递归的建立某些节点集指向父节点的引用。有时候，当我们考虑提交的父节点提交树和当前节提交节点树做差异比较时（diff），将一次提交想象成一次修补补丁（patch）是有助于我们理解git 的工作机理。按照这种方式，我们可以这样认为，提交树就是集成应用了所有父节点的补丁修补。一颗在两个分支上做merge操作的树，因此就可以认为是两个分支应用了其各自所有的父节点修补补丁程序，然后做一次联合操作Union。

但是那不是git merge 的真正执行方式，原因是，首先，如果以那样工作的话，执行会非常的慢！，并且在执行过程中它要再一次重新处理所有的之前合并时造成的冲突。如此，git merge 真正是如何操作的呢？

我喜欢用数学的思维方式思考：给定两个提交 \[A\]和 \[B\] ，合并提交（commit）操作  就可以描述为： 这里的 是 和 的合并共有项(最近提交树祖先共同含有的部分)，我们必须要“减去” ，因为如果不这样的话，我们就会有两个 。这个操作 被叫做三向合并。你可以认为执行路径为将 应用到 上，或者s 应用到 上。

事实上diff和patch操作并没有字面上按照上面的的操作行事，相反而是使用了：最长公共子序列算法来实现。x-w和序列x,序列w的差异就是我们知道的在求最长公共子序列时的赋值（中间可能要去除到两个序列的公共部分）。为了构造三向合并x+y-w,我们对x和w在求公共子序列的时候进行赋值，对y和w在求公共子序列的时候赋值，然后输出每个要么：
	
	三个序列的共有部分，或者
	在x 中出现，但是在y 和 w中不存在的部分，或者
	在y中出现，但是在x和w中没有出现的部分
同时我们要删除那些序列，要么：
	
	出现在y 和 w但是在x中没有出现，或者
	出现在x和w中但是在y中没有出现。
举个栗子：

1	x:      w:      y:      ↦ merged:
2	milk    milk    milk      milk
3	juice                     juice
4	flour   flour   flour     flour
5	                sausage   sausage
6	eggs    eggs    eggs      eggs
7	        butter  butter

在x,y与w的行序可能仅仅说明了一种在三向合并的输出行上的一种偏序关系，如果是这样的话，由于同样的块w,在x,y 之间以不同的方式被编辑-因此我们说那就是一个合并冲突，将会输出该信息，让用户手动解决。

当git 向你显示合并冲突的时候，默认情况下，你将会看到x和的冲突块：

1. <<<<<<< x
1. I had one egg and three sausages for breakfast.
1. =======
1. I had two eggs and two sausages for breakfast.
1. >>>>>>> y


然而，冲突块会变得更容易解决，当你能够看到合并基准w的时候。我建议打开开关：
~/.gitconfig
通过设置merge.conflictstyle 为diff3，则
1. git config --global merge.conflictstyle diff3
1. <<<<<<< x
1. I had one egg and three sausages for breakfast.
1. ||||||| w
1. I had one egg and two sausages for breakfast.
1. =======
1. I had two eggs and two sausages for breakfast.
1. >>>>>>> y
1. 
现在你可以看到解决方式为：
I had two eggs and three sausages for breakfast.

（注意，这个操作会对称性的（with regard to with reference to0 关于w和结果进行交换，因此你真正需要的是查看w）
这里有另外两种其他的案例需要考虑：可能行为：
	出现在x和y中，但是在w中没有出现
	出现在w中，但是没有在x 和y 中出现

某些三向合并算法经常将这样的行标记为冲突行。然而Git,将会优雅的输出或者直接删除该行，依次，假定该行没有改变。这种效果叫做意外清理合并。偶尔某些情形在实际应用中很有用，尤其是用户把版本搞砸了，各自合并同一个补丁的两个不同的版本。但是我认为掩盖这种错误不是一种好的行事方式，我希望这种行为可以并关闭。尽量避免因为他所能带来的这种优点而使用它吧。

如果你仔细，很有观察力，你可能已经发现我在上述说明中存在的一个漏洞了：由于commit A和B可能各自又包含commit,他们最近的共同祖先可能不是唯一的！一般，他们最有可能的情形是，最近的共同祖先是 ，在这种情况下，git merge 操作将会递归的执行：它首先构造合并 ，并以此作为三向合并 的基础（base）。这就是为什么Git的默认合并策略并称为递归的。

假定两个分支如下图所示，A,B,C,D,E是master分支的历史快照（snapshot）;A,B,X,Y,Z是feature分子的历史快照。


1 A -- B -- C -- D -- E
2	\                  
3          -- X -- Y -- Z


命令	
git merge feature
首先查找“master”（当前分支）和“feature”的共同祖先。它或多或少的等价于以下命令：
git merge-base master feature
在我们的举的例子里，他们的共同祖先是B。
如果在C,D,E和X,Y,Z提交中没有冲突，git 将会创建一次“merge commit ” merge commit会有两到多个父亲。
新的图将会是下面这个样子。




A -- B -- C -- D -- E -------- M
      \                        /
        -- X -- Y -- Z -------


每一次git commit 提交都会生成一棵树，一到多个“父亲节点”，作者的名字，email,日期和提交者的姓名，email,日期。

merge提交和普通的提交的唯一区别就是祖先的数量。

在第二幅图中，merge commit提交被以“M”标注出来了。

如果提交存在冲突，用户就会被要求解决冲突，并手动创建合并提交，在冲突解决后

git commit -a

将会创建合并提交。这条命令没什么特殊的语法。Git 已经知道了用户已经在进行合并了（已经在尝试合并）。


数学公式：

\\( 1/x^{2} \\)
\\[ \frac{1}{n^{2}} \\]

\\[A\]

\\[B\]
