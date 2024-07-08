---
{"dg-publish":true,"permalink":"/Toollectures/Lecture 4 Data Wrangling/","dgPassFrontmatter":true}
---


# Source
---
- 中文[笔记](https://missing-semester-cn.github.io/2020/data-wrangling/)
# 数据管理
---
- less 命令
- sed 命令
	- s 命令
## 正则表达式
- 正则表达式通常以`/` 开始和结束
- 正则表达式一些常见的模式
- perl 命令
- 正则表达式检测[网站](https://regex101.com/r/qqbZqh/2)
- 弄清楚正则表达式，`sed -E 's/.*Disconnected from (invalid |authenticating )?user .* [^ ]+ port [0-9]+( \[preauth\])?$//'
	- ❓user之前的问号有什么用
		- 此处的问号表示前面的部分出现0次或1次，即有或没有都行
		- 问号还可以与 * 和 + 合用，转换为非贪婪模式
	- ❓之后的 \[preauth\]为什么要转义
		- 转义的原因是正则表达式中有中括号的语法，表示匹配中括号中的任意一个字符，但是这里需要匹配的是整个中括号和里面的字符，将其视作匹配的文本，因此需要转义
	- 💡`[^a]` 表示匹配任意非空且非a的字符
- 捕获组
## 回到数据整理
- sort 命令
	- uniq -c
	- head 与 tail
- awk 命令
	- paste
## awk 编程语言
- 语言知识[网址](https://backreference.org/2010/02/10/idiomatic-awk/)
## 分析数据
## 确定参数
## 整理二进制数据
---
# 本节作业
- 1.正则表达式[学习网址](https://regexone.com/)，做了遍
- 💡2. 
	- 匹配正则表达式是指字符串的子串符合正则表达式
		- grep 也可以搭配正则表达式使用，grep -E 得到匹配的 ， grep -E -v 去掉匹配的(-E 是为了支持一些正则表达式)
	- sed的正则表达式主要用来替换匹配字符串的相应子串或者用于分组操作匹配字符串的相应子串，不适合筛选字符串，grep 更适合筛选字符串，==看本题解答可能更加理解这条==
	- tr 可以管理字母大小写
	- 💡{m,n}{n}的用法很多元
		- 可以 `a{3}` 指包含3个连续的a，`a{1,3}`指包含1到3个连续的a
		- `（[^a]*a){3}` 指包含3个a
		- 💡我认为`{}` 本质上讲就是将前一组重复到表达式中m到n次
- 3. sed 进行文件内容替换时，会先将后面的文件清空
- 💡6. 清洗获取网页的数据，看解答很详细，但是解答的网页下载不下来，主要是知道这个具体的用法，这应该是它的实用之处