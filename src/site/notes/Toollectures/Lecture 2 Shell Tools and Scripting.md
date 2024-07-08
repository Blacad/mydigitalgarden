---
{"dg-publish":true,"permalink":"/toollectures/lecture-2-shell-tools-and-scripting/","dgPassFrontmatter":true}
---


# Source
---
- 英文课程[笔记](https://missing.csail.mit.edu/2020/shell-tools/)
- 中文课程[笔记](https://missing-semester-cn.github.io/2020/shell-tools/)
# Shell Scripting
---
- shell 脚本能够针对shell命令进行优化，也更加方便实现命令的批处理，本文主要以bash为例
- 💡在bash中为变量赋值的语法是`foo=bar`，访问变量中存储的数值，其语法为 `$foo`。 需要注意的是，`foo = bar` （使用空格隔开）是不能正确工作的，因为解释器会调用程序`foo` 并将 `=` 和 `bar`作为参数。 总的来说，在shell脚本中使用空格会起到分割参数的作用，有时候可能会造成混淆，请务必多加检查。
- 💡Bash中的字符串通过`'` 和 `"`分隔符来定义，但是它们的含义并不相同。以`'`定义的字符串为原义字符串，其中的变量不会被转义，而 `"`定义的字符串会将变量值进行替换。
``` shell
foo=bar
echo "$foo"
# 打印 bar
echo '$foo'
# 打印 $foo
```
- bash中的if、case、for流程和函数，以及一些常用参数
- bash中处理错误返回和条件判读的执行逻辑，条件判断执行逻辑与C相同
- bash中接受返回值，$(CMD)
- bash语言中的语法细节很多，详见笔记
```bash
#!/bin/bash

echo "Starting program at $(date)" # date会被替换成日期和时间

echo "Running program $0 with $# arguments with pid $"

for file in "$@"; do
    grep foobar "$file" > /dev/null 2> /dev/null
    # 如果模式没有找到，则grep退出状态为 1
    # 我们将标准输出流和标准错误流重定向到Null，因为我们并不关心这些信息
    if [[ $? -ne 0 ]]; then
        echo "File $file does not have any foobar, adding one"
        echo "# foobar" >> "$file"
    fi
done
```
- 通配符、花括号
- shebang与env
- shell函数与脚本的不同之处
# Shell Tools
---
## 查看命令的用法
- 常见的策略是man命令和网页搜索，但是这样的效率太低
- 本文档用`npm install -g tldr`下载了tldr程序（前提是配好了node.js的环境），能够更好地展示命令的用法
## 查找文件
- find 命令
- fd 命令
- locate 命令
- 💡这里的查找文件命令可以在查找相应文件的基础上，完成一些对同类文件重复的工作
## 查找代码
- grep 命令
## 查找shell命令
- 按“向上键”可以迭代的找到上一条shell命令
- history 命令
## 文件夹导航
- `fasd` 和 `autojump` 命令来查找最近使用的文件夹，这两个程序我都没下载
- 其他的一些命令
---
# 本节作业
- ❓bash函数编写
	- 详见笔记解答,很有意思
	- source 载入
- ❓bash脚本编写
	- 详见笔记解答
	- shell 对格式的要求非常严格
```shell
if [[ $? -ne 43 ]]; then
...
fi
```

```shell
while true
do
...
done
```

```shell
n=$(($RANDOM%100))
n=$((n+1))
```