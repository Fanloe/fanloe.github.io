---
title:  "工具：Vim，Git，SSH, Grep/Sed/Awk, Pandoc"
date:   2022-07-15 11:05:30 +0800
categories:
  - Linux
tag:
toc: true
toc_sticky: true
---
## Vim
> vim自带参考：vimtutor | :help  
> vim参考文档：[github/star list](https://github.com/stars/Fanloe/lists/vim-learning): [vim learning/repository](https://github.com/iggredible/Learn-Vim) | [zhihu/专栏](https://www.zhihu.com/column/learn-vim)   
> vim相关设置：[vimrc最小通用设置](https://github.com/wsdjeg/vim-galore-zh_cn/blob/master/contents/minimal-vimrc.vim)  

### tag
- 跳至tag：ctrl+]  
- 返回tag：ctrl+T  

### registers
- 设置寄存器："a+  
- 查看寄存器：:registers    

### markers
- 添加标签：m+
- 跳至标签：' / \`  
- 查看标签：:marks  

### completion
- 填充/下一项：ctrl n  
- 上一项：ctrl p  

### buffers, windows, tabs
buffers:  
- :buffers  
- :bn :bp  
- :b+number  
- :b+filename  

windows:  
- :split :vsplit  
- :new  
- :close  
- :quit  

## Git
- [git官网](https://git-scm.com)
- [git & github](https://www.cnblogs.com/schaepher/p/5561193.html)
- [将本地项目关联到github远程仓库](https://zhuanlan.zhihu.com/p/88246764)
- ==[深入理解git原理](https://www.cnblogs.com/mamingqian/p/9711975.html)==
- [learn git branching](https://learngitbranching.js.org/?NODEMO=&locale=zh_CN)

## SSH登陆远程服务器的三种方式
> [ssh的两种登陆方式：密码登陆与免密登陆](https://blog.csdn.net/qq_43551263/article/details/114834360?spm=1001.2101.3001.6650.2&utm_medium=distribute.pc_relevant.none-task-blog-2%7Edefault%7ECTRLIST%7ERate-2-114834360-blog-90231433.pc_relevant_aa&depth_1-utm_source=distribute.pc_relevant.none-task-blog-2%7Edefault%7ECTRLIST%7ERate-2-114834360-blog-90231433.pc_relevant_aa&utm_relevant_index=5)  
> [SSH连接服务器 本地记住用户名及密码](https://blog.csdn.net/persist_xyz/article/details/90231433)  

1. 密码登陆  
- `ssh -p 22 root@47.33.22.103`  
- 然后输入密码。  
2. 免密登陆（在第一种的基础上无需输入密码
- 本地生成本机的公私钥：`ssh-keygen -t rsa`  
- 在`~/.ssh`目录下查看两个公私钥文件  
- 将公钥发送到服务器：  
`ssh-copy-id root@47.33.22.103`  
或`scp ~/.ssh/id_rsa.pub root@39.97.170.231:～/.ssh/authorized_keys`  
- `ssh -p 22 root@47.33.22.103`  
- 不用输入密码。  
3. 记住用户名（在第二种的基础上无需输入ip  
- 本地保存服务器信息：在`~/.ssh`目录下新建config文件，写入：  
```
Host xyz
Hostname 57.33.22.99
Port 22
User root
IdentityFile /Users/xxx/.ssh/id_rsa
```
- 服务器端需设置自动检验：在`/etc/ssh/sshd_config`中去注释：  
```
PubkeyAuthentication yes
AuthorizedKeysFile .ssh/authorized_keys
```

## Grep/Sed/Awk
- [grep sed awk](https://zhuanlan.zhihu.com/p/110983126)
- [regexp](https://www.princeton.edu/~mlovett/reference/Regular-Expressions.pdf) 

## Pandoc
> [神奇Pandoc安装与使用](http://zhouyichu.com/misc/Pandoc/)  
> [Pandoc with Chinese](https://github.com/jgm/pandoc/wiki/Pandoc-with-Chinese)  
> [Where do I get the pdflatex program for Mac?](https://superuser.com/questions/1038612/where-do-i-get-the-pdflatex-program-for-mac)  

Install pandoc on Mac: `brew install pandoc`  
MD to html: `pandoc file.md -o file.html`  
MD to pdf: `pandoc file.md -o file.pdf`  
MD to doc: `pandoc file.md -o file.docx`  
P.S.  
For Chinese: `pandoc in.md -o out.pdf --latex-engine=xelatex`. If not working like:  
[![xcjnQ1.png](https://s1.ax1x.com/2022/10/22/xcjnQ1.png)](https://imgse.com/i/xcjnQ1)
Use `pandoc in.md -o out.pdf --pdf-engine=xelatex`.   
If not working like:  
[![xcj8Fe.png](https://s1.ax1x.com/2022/10/22/xcj8Fe.png)](https://imgse.com/i/xcj8Fe)
Add main font: `pandoc in.md -o out.pdf --pdf-engine=xelatex -V mainfont="SimSong"`  
Also, you can add in md file beginning with yaml as metadata in md:  
```
---
mainfont: SimSong
---
```
