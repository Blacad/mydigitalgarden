---
{"dg-publish":true,"permalink":"/toollectures/lecture-5-command-line-environment/","dgPassFrontmatter":true}
---


# Source
---
- 中文[笔记](https://missing-semester-cn.github.io/2020/command-line/)
# 任务控制
---
## 结束进程
- 当我们输入 `Ctrl-C` 时，shell 会发送一个`SIGINT` 信号到进程
- 当我们输入`Ctrl-\`时，shell 会发送一个`SIGQUIT`信号到进程
- 尽管 `SIGINT` 和 `SIGQUIT` 都常常用来发出和终止程序相关的请求。`SIGTERM` 则是一个更加通用的、也更加优雅地退出信号。为了发出这个信号我们需要使用 [`kill`](https://www.man7.org/linux/man-pages/man1/kill.1.html) 命令, 它的语法是： `kill -TERM <PID>`
## 暂停和后台执行程序
- 当我们输入`Ctrl-Z` 会让 shell 发送 `SIGTSTP` 信号，`SIGTSTP`是 Terminal Stop 的缩写，它会让进程暂停
- 我们可以使用 [`fg`](https://www.man7.org/linux/man-pages/man1/fg.1p.html) 或 [`bg`](http://man7.org/linux/man-pages/man1/bg.1p.html) 命令恢复暂停的工作。它们分别表示在前台继续或在后台继续
- `jobs` 命令会列出当前终端会话中未完成的全部任务
- `&` 命令后缀可以让命令直接在后台执行
- `SIGHUP` 终端终止和后台进程终止
## 终端多路复用
- `tmux` 的继承结构
	- 会话
	- 窗口
	- 面板
## 别名
- `alias` 设置别名方便使用
## 配置文件(Dotfiles)

### 可移植性
## 远端设备

### 执行命令

### SSH密钥

#### 密钥生成
- `ssh-keygen` 
- 💡生成的密钥在`~` 中的配置文件`.ssh` 中 
#### 基于密钥的认证机制
#### 通过SSH复制文件
- `tee`
- `scp` 
- `rsync`
#### 端口转发
- 监听远程服务器的端口
#### SSH配置
## Shell & 框架
## 终端模拟器
---
# 本节作业
## 任务控制
- 💡1. 解答
- 💡2. 解答
	- 💡shell 中的while是根据后续命令的返回值判断，为0进入否则退出
	- shell 的while 结构 
		- while commands do ... done
## 配置文件
- 💡本任务看解答，有点用
	- 💡我现在常用的配置文件
		- `.zshrc` 这里采用的是 `oh my zsh` 官方文档README来[配置](https://github.com/ohmyzsh/ohmyzsh)，其中的插件配置参考的cs自学指南中的[配置](https://sourabhbajaj.com/mac-setup/iTerm/zsh.html)，插件在`custom/plugs`
		- `.vimrc` 这里采用的是 missing 课程中的该文件，其中的插件配置[参考](https://www.cnblogs.com/zhaodehua/articles/15108744.html)