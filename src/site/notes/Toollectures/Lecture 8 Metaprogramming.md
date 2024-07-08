---
{"dg-publish":true,"permalink":"/Toollectures/Lecture 8 Metaprogramming/","dgPassFrontmatter":true}
---


# Source
---
- 中文[笔记](https://missing-semester-cn.github.io/2020/metaprogramming/)
---
# 构建系统

- 本节主要讲如何构建一个项目系统
- 构建系统
	- make 与 Makefile
---
# 依赖管理

- 本节主要在讲包管理
- 版本控制与版本号
- 锁文件与`vendoring` 
---
# 持续集成系统

- 本节主要介绍持续集成和相关工具
- 持续集成，`CI` 是一种雨伞术语
- 我感觉就是优化了修改代码到重新发行的过程
---
# 测试简介

- 本节主要讲述了测试相关的概念
---
# 本节作业

- 💡1. 见解答，很详细
	- 💡[参考](https://www.gnu.org/software/make/manual/html_node/Phony-Targets.html)`.phony` 的作用主要有两个：
		- 避免同名文件，如果有同名文件就是`clean` , 那么我们需要声明 `.phony:clean` ，否则会出现问题，一旦我们声明，那么 `make clean` 命令一定会执行
		- 提高性能，该部分的功能没用过
- 💡2. 构建系统的例子，解答
- 💡3. Git 的一个小用法，hooks的用法初见端倪，其实也是一种持续集成系统，见解答
- 💡4. 基于 git-hub 的持续集成系统初试，见解答
	- ❓GitHub Pages 怎么用
		- GitHub Pages，由于终端的 `github` 鉴权太过于麻烦和一些莫名的错误，我直接用`github Desktop` 来处理本地与远端的推送和拉取等
		- 在使用这个功能的过程中，我[参考](https://docs.github.com/en/pages/setting-up-a-github-pages-site-with-jekyll/about-github-pages-and-jekyll)和[参考](https://jekyllrb.com/docs/installation/#requirements)`Jekyll` 创建了个人网站，但是这个个人网站并不好看，于是我决定从头再来，利用下面这个
		- 为了实现更好的个人博客网站，我参考了这位前辈的[网站](https://linhandev.github.io/posts/Github-Page/)，但是这个说的其实很模糊，于是我就按照[官方文档](https://github.com/cotes2020/jekyll-theme-chirpy)来做了
		- 我感觉在构建个人主页的过程中，已经很好地锻炼了这些能力
		- 随后，我认为之前的对我来说即使构建了也没什么大用，于是我选择了最后一种[方式](https://b23.tv/VjZwEc1),此方法相当于是obsidian原生的方法，`github` 只是用来存储，`netlify` 才是部署者，相当于没用`github` 提供的路由
		- 💡5. 与4类似，见解答
- 本节作业都挺重要的