# Adobe 面试体验|第 36 集(校外驾车)

> 原文:[https://www . geesforgeks . org/adobe-面试-体验-设置-36-校外-开车/](https://www.geeksforgeeks.org/adobe-interview-experience-set-36-off-campus-drive/)

**线上笔试:**
智能选择题和编程 2 编码题。

**F2F R1**
1)给定任意长度的字符串。打印字符串长度 k 的所有可能组合
提示使用递归

2)给定矩阵，按螺旋顺序打印。

3)验证给定的树是否为 BST。
已经按照方法 3[https://www . geeksforgeeks . org/a-program-to-check-if-a-binary-tree-is-BST-or-not/](https://www.geeksforgeeks.org/a-program-to-check-if-a-binary-tree-is-bst-or-not/)
解决了然后他自己从同一个链接口头介绍了方法 1，并让我为同样的方法写代码，并找出方法的错误。

**F2F R2**
1)给定一个节点，使得

```
Node x {
   boolean ifFile;
   int[] children;	
} 
```

必须打印从根目录到文件的所有路径。如果没有文件，不要打印任何东西。
注意:这里不是树，也不是图。
结构类似 windows 文件系统，层次可以任意长。所以递归会导致堆栈溢出。不用递归求解

2)给定一个排序数组，其中一个数字具有任意数量的副本
对于 eg [1，2，3，4，4，5，6]
，求副本元素第一次出现的索引。
所以对于上面的例子，你的函数应该返回 3。
提示:使用二分搜索法

3)到达终点的最小跳跃次数
给定一个整数数组，其中每个元素代表从该元素向前可以进行的最大步数。
写一个函数，返回到达数组末尾的最小跳转次数(从第一个元素开始)。
如果一个元素是 0，那么就不能穿过那个元素。
示例:
输入:arr[] = {1，3，5，8，9，2，6，7，6，8，9}
输出:3 (1- > 3 - > 8 - > 9)

**F2F R3**
讨论简历和工作项目。
1)给定一个二进制流，说明该数在任何时间点是否能被 3 整除
讨论了 2-3 种方法。
2)讨论了实现字典的各种方法。
3)给定一个集合，打印所有可能的子集。

**F2F R4(导演轮，最后一个)**
也讨论了我的工作项目和大学项目。
讨论了阵列旋转问题的各种方法和复杂性。

如果你喜欢极客博客并想投稿，你也可以写一篇文章并把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。

如果发现有不正确的地方，请写评论，或者想分享更多关于以上讨论话题的信息

[All Practice Problems for Adobe](https://practice.geeksforgeeks.org/company/Adobe/) !

## 相关实践问题

[Minimum number of jumps](https://practice.geeksforgeeks.org/problems/minimum-number-of-jumps/0)