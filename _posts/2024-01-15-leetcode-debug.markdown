---
title:  "Leetcode二刷"
date:   2024-01-15 20:05:30 +0800
categories: 
  - Coder
tag:
  - leetcode
---
## 算法
- KMP: [28. Find the Index of the First Occurrence in a String](https://leetcode.cn/problems/find-the-index-of-the-first-occurrence-in-a-string) - [如何更好地理解和掌握 KMP 算法?](https://www.zhihu.com/question/21923021/answer/281346746)
> PMT(partial matched table)部分匹配表：字符串每个位置前缀和后缀相同的子串长度
- 贪心算法: 
> 跳跃游戏
- map
### Random
> [Leetcode 380. Insert Delete GetRandom O(1)](https://leetcode.cn/problems/insert-delete-getrandom-o1/?envType=study-plan-v2&envId=top-interview-150)
```
#include <random>
//1. 伪随机数引擎
//2. 概率分布
std::default_random_engine e;
std::uniform_int_distribution u(min, max);
{
  e.seed(0);
  //e.seed(time(0));
  cout<<u(e); //随机数

}
```
### String split
```
void stringSplit(string s, char delimiter, vector<string> words){
  istringstream iss(s);
  string token;
  while(getline(iss, token, delimiter)){
    words.push_back(token);
  }
}
```
### 函数参数传递
1. 值传递
> 指针形参
```
void flatter(TreeNode* root){
  //root不重要，root原本指向的结点才重要
}
```
2. 参数传递
### DFS深度优先算法：pre in post Order traverse
- 递归 改 循环（Recursion to Iteration）
```
Struct TreeNode{
  int val;
  TreeNode *left;
  TreeNode *right;
  TreeNode():val(0), left(nullptr), right(nullptr){}
  TreeNode(int v): val(v), left(nullptr), right(nullptr){}
  TreeNode(int v, TreeNode* l, TreeNode* r): val(v), left(l), right(r){}
}
void inOrderTraverse(TreeeNode *root){
  inOrderTraverse(root->left);
  cout<<root->val;
  inOrderTraverse(root->right);
}
void inOrderTraverse(TreeNode *root){
  stack<TreeNode *> nodes;
  TreeNode *cur = root;

  while(!nodes.empty()||cur!=nullptr){
    while(cur!==nullptr){
      nodes.push(cur);
      cur = cur->left;
    }

    cur = nodes.top();
    nodes.pop();
    cout<<nodes->val;
    
    cur = cur->right;
  }
}
```
## Debug
### size_type
[c++ vector 返回值](https://zhuanlan.zhihu.com/p/473209606)
> c++中无符号类型溢出后会在取值范围中循环取值，有符号类型溢出会导致未定义值。vector随机访问的下标和size函数返回的类型都是vector类内定义的size_type类型，它是一个无符号整型，在不同的机器上可能会有不同的长度，一般可以理解为unsigned int

### AddressSanitizer
> [AddressSanitizer](https://github.com/google/sanitizers/wiki/AddressSanitizer)

- heap-buffer-overflow: [堆内存溢出](https://www.zhihu.com/question/634293619)
> 数组越界

- stack-buffer-overflow: 栈内存溢出，循环不终止导致调用函数栈溢出[leetcode中错误](https://blog.csdn.net/lijianyi0219/article/details/111510086)

- [c++ 在for循环里面return的问题](https://blog.csdn.net/wwwzzzfffq/article/details/112861137)
$return {}$
