### vim
**有四种模式：**
1. 普通模式
2. 插入模式
3. 底层模式
4. 模式

##### 普通模式下
进行搜索：
- 输入`/` 加搜索关键字，`enter`，从前到后查找，按`n`查找下一个，按`N`查找上一个；
- 输入`?` 加搜索关键字，`enter`，从后到前查找，按`n`查找下一个，按`N`查找上一个；
- 输入`/`或`?`后 上下键可出现搜索历史
- 大小写敏感：
	- 想要忽略大小写，在 Vim 命令行中输入`:set ignorecase` 或者 `:set ic`。你还可以在你的`~/.vimrc`文件中添加默认选项，来设置忽略大小写。

想要修改回大小写敏感，输入`:set noignorecase`或者`:set noic`。

强制忽略大小写的方式就是在搜索样式后面添加`\c`。例如，`/Linux\c`将会在搜索时忽略大小写敏感。搜索样式后面添加大写的`\C`，会强制要求大小写敏感。

删除整行：`dd`
复制整行：`yy`
粘贴：`p`


https://zhuanlan.zhihu.com/p/68111471