---
title:  "SAT Solver总结"
date:   2022-12-22 20:05:30 +0800
categories: 
  - Formal Method
tag:
  - sat
---
## 6个solver
其不同点在于分支选择策略，在Github[一个cdcl实现](https://github.com/sukrutrao/SAT-Solver-CDCL)的基础上进行改写。  
### 关于cdcl
[这篇文章](https://cse442-17f.github.io/Conflict-Driven-Clause-Learning/)很生动，有互动HTML（？）分步演示了这些概念：
- Boolean Constraint Propagation(Unit Propagation)
- DPLL
- Conflict Driven Clause Learning及其中的
- Clause Learning过程。  
### 关于vsids
[这个pdf](https://baldur.iti.kit.edu/sat/files/2019/l08.pdf)的介绍很清楚：  
- VSIDS: Variable State Independent Decaying Sum
    - General approach: Compute score for each variable, select variable with highest score  
    - 一般准则：计算每个变量分数，选得分最高的  
    - Initial variable score is number of literal occurrences  
    - 变量的初始分数为literal出现次数  
    - New conflict clause c: Score is incremented for all variables in c
    - 新冲突子句c：c中的所有变量分数增加  
    - Periodically, divide all scores by a constant
    - 周期性地，所有变量的得分以常数比例衰减  
- First presented in SAT solver Chaff, 2001

> [SAT - Benchmark](https://www.cs.ubc.ca/~hoos/SATLIB/benchm.html)  

## 过程中用到的一些技术
### C++程序编译
沿袭Github的那个实现，C++ build system采用make和Makefile: [一个GitHub的tutorial](https://makefiletutorial.com/)  

### Shell Script调用另一个Script
有[三种方法](https://stackoverflow.com/questions/8352851/shell-how-to-call-one-shell-script-from-another-shell-script)，
- bash: 将脚本作为另一个进程执行
- source：将另一个脚本作为子进程调用  
> [Difference between sh and Bash](https://stackoverflow.com/questions/5725296/difference-between-sh-and-bash)

### Linux命令Time
- 使用：`time ls`  
- real, user, sys[区别1](https://cloud.tencent.com/developer/article/1491229)/[区别2](https://www.orchome.com/539)
    *  real —— 程序从开始到结束所用的时钟时间。这个时间包括其他进程使用的时间片和进程阻塞的时间（比如等待 I/O 完成）。  
    * user —— 进程执行用户态代码（核心之外）所使用的时间。这是执行此进程所使用的实际 CPU 时间，其他进程和此进程阻塞的时间并不包括在内。在垃圾收集的情况下，表示 GC 线程执行所使用的 CPU 总时间。  
    * sys —— 进程在内核态消耗的 CPU 时间，即在内核执行系统调用或等待系统事件所使用的 CPU 时间。  
- time 结果输出到文件：`(time ls) &>> output.log` 

### Linux前台后台
- [Linux如何让正在运行的程序放到后台运行
](https://viencoding.com/article/177)：`^z` ;; `jobs -l`;; `bg 1`;; `disown -h %1`  
- [关闭终端，程序后台运行](https://www.51cto.com/article/625426.html)：  

```bash
$ nohup sh test.sh &  
# 直接关闭当前终端，再打开一个查看  
$ ps -few|grep test.sh 
```

> [mac zsh要加%](https://stackoverflow.com/questions/32614648/weird-jobs-behavior-within-zsh): `bg %1`  
> [nohup:ignoring input and appending output to 'nohup.out'
](https://stackoverflow.com/questions/24646320/nohupignoring-input-and-appending-output-to-nohup-out)：`nohup php server1.php </dev/null &>/dev/null &`


### others
- MAC输入法：[mac自带简易教程](https://www.zhihu.com/question/40883993/answer/94983392)  
- [MAC 用命令行更新](https://stackoverflow.com/questions/42538171/how-to-update-xcode-command-line-tools)：`softwareupdate --list`  
- [Linux随机删除一个幸运文件
](https://www.cnblogs.com/whtjyt/p/16317637.html)
