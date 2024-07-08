---
{"dg-publish":true,"permalink":"/toollectures/lecture-7-debugging-and-profiling/","dgPassFrontmatter":true}
---


# Source
- 中文[笔记](https://missing-semester-cn.github.io/2020/debugging-profiling/)
---
# 调试代码
## 打印调试法与日志

- Printf 调试大法
	- 在可能有问题的地方采用标准输出来寻找问题
- 日志法
## 第三方日志系统
- Mac 一般都会在系统日志中，可以用`logger` 来写入系统日志
- 💡我个人感觉，打印法和日志法其实是不太想整体调试的时候使用的，应用场景比较局限
## 调试器
- gdb, lldb, pdb
## 专门工具
- 调试二进制黑盒程序时，我们可以追踪某些系统调用，在 Mac 上可以用 dtrace 或 dtruss 来追踪系统调用（由于 SIP 保护协议，我没管这个）
- 分析网络数据包分析工具，像Wireshark等，这个用过
- web开发可以用浏览器自带的开发者工具
## 静态分析
- 有些问题是您不需要执行代码就能发现的。例如，仔细观察一段代码，您就能发现某个循环变量覆盖了某个已经存在的变量或函数名；或是有个变量在被读取之前并没有被定义。 这种情况下 [静态分析](https://en.wikipedia.org/wiki/Static_program_analysis) 工具就可以帮我们找到问题。静态分析会将程序的源码作为输入然后基于编码规则对其进行分析并对代码的正确性进行推理。
- 💡静态分析的工具挺多的，一般编译器都会自带，比如 vscode 会在你C代码末尾没写`;`时提醒你错误，这个过程称为 code linting
- 有些工具能够对代码进行风格检查和代码格式化
	- 💡在我的实践中就接触过 C 的格式化工具 clang-format 和 markdown 的格式化工具
---
# 性能分析

- 💡过早的优化是万恶之源，过早优化（PrematureOptimization） 被定义为在我们知道需要进行优化之前进行优化，因为这是耗时的，并且是局部的
- 由上，我们可以在写完程序后，采用性能分析和监控工具来查找程序中找到最耗时的部分
## 计时
- 💡通常就是在待测代码块开始时记录时间，最后用结束时间 - 开始时间得到代码块消耗的时间，但是这个算出来的执行时间或叫真实时间（wall clock time） 可能会误导您，因为在代码跑的过程中，电脑可能还在运行其他程序导致测得的时间不准确，所以我们的工具需要区分：
	- 真实时间 - 从程序开始到结束流失掉的真实时间，包括其他进程的执行时间以及阻塞消耗的时间（例如等待 I/O或网络）
	- User - CPU 执行用户代码所花费的时间
	- Sys - CPU 执行系统内核代码所花费的时间
	- 💡最后两部分时间之和才是我们需要的
## 性能分析工具（profilers）
### cpu
- cpu 性能分析工具
	- 追踪分析器（tracing），记录程序的每次函数调用
	- 采样分析器（sampling），只会周期性检测程序并记录程序堆栈
- 大多数的编程语言都有一些基于命令行的分析器，我们可以使用它们来分析代码。它们通常可以集成在 IDE 中，但是本节课我们会专注于这些命令行工具本身。
	- 行分析器
	- Python 的 cProfile 分析器
### 内存
- C 与 C++ 这样的语言由于使用完内存后不去释放它，很容易发生内存泄漏，为了应对内存类Bug，我们可以用Valgrind工具
- Python 等具有垃圾回收机制的语言，内存分析器也有用武之地，因为只要有指针还指向它，它就不会回收，`memory-profiler` 就是分析Python的一种好用的工具
### 事件分析
- perf 命令
### 可视化
- 火焰图
	- 在 Y 轴显示函数调用关系
	- 在 X 轴显示其耗时的比例
- 调用图和控制流图，Python中调用 `pycallgraph` 来生成这些图
	- 💡下载和使用 python 第三方库的时候，我发现`pip` 的包管理和 `brew` 的包管理发生了冲突，以下是几种解决方法：
		- `pipx` 可以无冲突地下载 python 的第三方库并且可以全局使用，原理就是虚拟环境和环境共享，但是在程序中需要添加依赖注释，[详情见](https://github.com/pypa/pipx/blob/main/docs/examples.md)（偷懒小程序可以用这个）
		- 使用`brew`直接下载python 第三方库，便可以全局使用，坏处是有些python第三方库在其中找不到（尽量不用，除非是很常用的第三方库）
		- 采用局部的虚拟环境 `virtualenv`, 它相当于为每个项目单独地开一个虚拟环境，然后在该虚拟环境中安装一些依赖并使用，其中`pip`命令能正常使用，不会共享到全局，有很好的封闭性[详细用法见](https://sourabhbajaj.com/mac-setup/Python/virtualenv.html) （一般情况用这个）
		- 利用 `Pycharm` 创建 Python 项目时就采用的是最后一种方法，我们平常用的时候最好就用最后一种方法
### 资源监控
- 通用监控
- I/O 操作
- 磁盘使用
- 内存使用
- 打开文件
- 网络连接和配置
- 网络使用
### 专用工具
- 对黑盒程序进行快速的基准测试
---
# 本节作业
## 调试作业
- 有些我们就不管了，因为一般都用编译器自带的方法
- 3. 💡[shellcheck](https://www.shellcheck.net/) 有个检测的在线检测网址
	- 💡在vim中安装插件，基于 vim-plug，我参考的[教程](https://www.cnblogs.com/zhaodehua/articles/15108744.html)
	- ❓每次在 shell 中运行`souce ~/.vimrc` 都会报错，但是确实重新载入了
		- 解决方法是在vim中使用`:source ~/.vimrc` 
		- [解答来源](https://stackoverflow.com/questions/8457599/warning-message-when-sourcing-vimrc)
- 4. 💡反向调试概念，能够追溯到过去（并再次前进）以检查程序状态。本质上，**它们使开发人员能够通过让开发人员倒带代码来在程序中前后移动，从而解决谋杀之谜**。 - UDB
## 性能分析作业
- 1.💡有意义的分析各种排序算法的时间，可以看解答很详细
	- 💡`perf` 命令是 Linux 的， Mac 没有这个命令，但是有替代的app `Instruments.app`，[原因参考](https://stackoverflow.com/questions/23200704/install-perf-on-mac)，[用法参考](https://blog.csdn.net/u014600626/article/details/78010376?ops_request_misc=&request_id=&biz_id=102&utm_term=Mac%20上instruments使用&utm_medium=distribute.pc_search_result.none-task-blog-2~all~sobaiduweb~default-6-78010376.142^v100^pc_search_result_base2&spm=1018.2226.3001.4187)，这个工具还是不太会用，在左上角可以选择目标可执行文件分析，但是似乎只能分析可执行文件，因此我还[参考](https://juejin.cn/post/7132357317827739656)学了生成 `python` 可执行文件
- 2. 试过了
- 3. 💡有点意思
- 4. 💡看解答