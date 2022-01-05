# 亚马逊面试体验|第 416 集(校内实习)

> 原文:[https://www . geesforgeks . org/Amazon-面试-体验-设置-416-校园-实习/](https://www.geeksforgeeks.org/amazon-interview-experience-set-416-campus-internship/)

**编码轮**
共有 2 道编码题(每道 10 分)和 20 道来自各种核心概念(OS、DS、算法、DB、C 语言等)的 MCQ 题。

*   **问题 1:**[https://www . geeksforgeeks . org/Given-a-string-print-all-可能-回文-partition/](https://www.geeksforgeeks.org/given-a-string-print-all-possible-palindromic-partition/) 给定一个字符串，找到给定字符串所有可能的回文分区。
*   **问题 2 :** [给你一大段，N 个字。你必须找到一个最小长度的段落分段，其中包含所有的 N 个单词在任何顺序。(不区分大小写)](https://practice.geeksforgeeks.org/problems/smallest-window-in-a-string-containing-all-the-characters-of-another-string/0)

22 名学生入围面试。

**面试第一轮**

面试官要求自我介绍，然后他要求详细解释我的[项目](https://www.geeksforgeeks.org/category/project/)，其中一个。然后他给了我 2 个编码问题

**问题 1 :** 给定一个排序的整数数组(可能包含重复项)，您应该编写一个返回元素第一个索引的函数。
例如 arr = [1，2，2，2，3，3，3，4]val = 3；ans = 4
**答案:** 这是一个基本的[二分搜索法](https://practice.geeksforgeeks.org/problems/who-will-win/0)除了你不仅要检查当前元素是否是 mid，还要检查它的前一个元素是否小于它(如果有前一个元素存在)，然后才返回 mid。
否则在左侧重复，直到满足上述条件。

**问题 2 :** 给定一棵二叉树检查它是不是二叉查找树？ [检查有无 BST](https://practice.geeksforgeeks.org/problems/check-for-bst/1)
在纸上写工整的代码很重要。面试官在代码上运行了几个例子。

**面试第二轮**
面试官问了我之前的面试及其问题。
后来他给我出了 2 道编码题。
**问题 1 :** 给定一个属性为 arr[j]–arr[j-1]或者是 1，0，-1 的整数数组和一个搜索值，提供一个高效的搜索机制。
**答案:** 天真的做法是执行线性搜索，也就是 O(n)。然后我按照二分搜索法的思路思考，但是，由于数组的属性，我们不能分割和重复。
过了一段时间，我想出了一个方法，从第一个元素开始，将每个元素与搜索值进行比较，并通过当前值和搜索关键字的绝对差值来增加其位置。
这是一种最坏情况下的 O(n)算法，但在一般情况下做得远远好于线性搜索。

**问题 2 :** [给定一个整数数组(允许重复)返回的是不是一组连续的整数？](https://practice.geeksforgeeks.org/problems/check-if-array-contains-contiguous-integers-with-duplicates-allowed/0)
输入:5，2，3，6，4，4，6，6 输出:是(因为它来自[2，3，4，5，6]的集合)
**回答:** 首先，我给了他一个基于哈希的方法。最初，对所有元素进行散列，然后选择第一个元素并以 1 递增，直到找到散列中不存在的值。类似地，从第一个值开始递减 1，得到计数。如果计数等于散列大小，则为真，否则为假。
是 O(n)时间复杂度和 O(n)空间复杂度。
他让我把空间复杂度提升到 O(1)。

我尝试了很多，但没有找到解决办法。然后，他通过给出提示简化了问题，并使其成为数组中的[重复检测问题，而不使用任何额外的空间，前提是数字在[ 0，长度 _ 数组-1 ]的范围内。](https://practice.geeksforgeeks.org/problems/find-duplicates-in-an-array/1)

这可以通过以 arr[j]%n 和 make arr[arr[I]]= arr[arr[I]]+n * arr[I]的形式访问索引 j 处的元素来实现。所以，如果在任何阶段，arr[j/n]是>的话，那就意味着我们之前已经去过了。他对这个解决方案很满意。

[DS](https://www.geeksforgeeks.org/data-structures/) 问题

1.  给出你更喜欢哈希表而不是 BST 的用例，反之亦然？
2.  哈希表和 BST 中重复插入的情况下会发生什么。它对搜索的复杂性有什么影响？

我回答了这些，他对答案很满意。
面试官很安慰，给出线索指导我们解决。