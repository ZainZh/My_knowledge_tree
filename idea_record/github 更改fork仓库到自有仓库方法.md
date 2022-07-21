#! https://zhuanlan.zhihu.com/p/544372221
# github将fork得到的仓库更改到自有仓库方法并在主页显示contribution
创建自己的github账号也有半年多的时间了，很喜欢这个社区，也希望自己能够掀起一些浪花。
这半年多的时间，也做了一些项目，不过有一天突然发现自己主页里的contribution竟然很多天都是空的。
![Image](https://pic4.zhimg.com/80/v2-d4cb0989937ada6c528f15623f7d17a9.png)
这就让我很疑惑了。
所以我翻看了Github文档，找到了关于[contribution](https://docs.github.com/cn/account-and-profile/setting-up-and-managing-your-github-profile/managing-contribution-settings-on-your-profile/why-are-my-contributions-not-showing-up-on-my-profile)的显示方式。其中有一条是
>The commits were made in a standalone repository, not a fork.

不过我的项目最初为了方便学习，再加上对git规则不是很了解，确实是基于IsaacGym的公有库fork下来的。但是github本身并没有提供切断fork库联系的功能。网上这方面的资料很少，因为需求很少吧，估计很少人会像我一样这么在意这个绿格子。但是经过查找尝试，终于搞明白了如何解决这个问题，记录一下。
1. 第一步将你原来的仓库里所有的分支都存在本地（如果本地没有的话）。
![Image](https://pic4.zhimg.com/80/v2-e0217457ea779bc994f93cc7899885e3.png)
1. 第二部是删去所有的本地仓库里远程仓库
> $ git remote remove origin
> 
> $ git remote remove upstream
> 
3. 将本地仓库改个名字重新传到github上去
4. 最后一步也是最重要的一步，在github desktop上分别选一下你已经有的分支，在将他们创立成新的repo的branch。你就得到了一个新的，和原来无联系但是又保留了所有branch commit记录的库。在选一个main库（contribution只会显示main分支上的更新记录。大功告成！！