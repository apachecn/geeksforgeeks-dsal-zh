# Paytm 面试体验|第 15 集

> 原文:[https://www . geesforgeks . org/paytm-面试-体验-设置-15/](https://www.geeksforgeeks.org/paytm-interview-experience-set-15/)

*   **第一轮**
    1.  Say millions of players are playing a game online and their scores keep changing. Every player is represented by ID and SCORE. How to implement the following queries
        *   (I)可以添加新玩家，输入将是 id 和分数
        *   (ii)现有玩家的分数可以随着游戏在线实时进行更新，输入将是 id 和分数
        *   (iii)任何时候玩家可以获得它的等级，输入的将是 id，返回等级
        *   (iv)任何时候你都应该给排名前 k 的玩家，其中 k 不是固定的，输入的是 k，返回一个有 id 和分数的排名前 k 的玩家列表

        我试图用大量的数据结构来解决这个问题，但是一个平衡的二叉查找树在当时对所有的查询来说都是最好的。他还要求处理玩家分数相同的情况。可以有两种情况:相同玩家的分数具有相同的等级，相同玩家的分数基于 id 具有不同的等级。

    2.  [从给定的列号中找到 Excel 列名](https://practice.geeksforgeeks.org/problems/excel-sheet/0)
*   **第二轮**
    1.  [Recursively remove all adjacent duplicates](https://practice.geeksforgeeks.org/problems/consecutive-elements/0)

        这个问题有模糊的输出。
        考虑输入:1 2 4 5 5 4 4 5 7 8
        如果您先移除前两次出现的 5，那么输出将是 1 2 5 7 8
        如果您先移除前两次出现的 4，那么输出将是 1 2 4 7 8

        面试官只说问题没有要求用递归什么的，所以我用堆栈不用递归解决了，但是花了很多时间。

    2.  [丑陋的数字](https://practice.geeksforgeeks.org/problems/ugly-numbers/0)
*   **第三回合**
    1.  Java 概念问题，需要适当的解释
    2.  [从左上角到右下角数出所有可能的路径](https://practice.geeksforgeeks.org/problems/count-all-possible-paths-from-top-left-to-bottom-right/0)T2】

如果你喜欢极客博客并想投稿，你也可以写一篇文章并把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。

[All Practice Problems for Paytm](https://practice.geeksforgeeks.org/company/Paytm/) !

## 相关实践问题

[Column name from a given column number](https://practice.geeksforgeeks.org/problems/column-name-from-a-given-column-number/0)[Recursively remove all adjacent duplicates](https://practice.geeksforgeeks.org/problems/recursively-remove-all-adjacent-duplicates/0)[Number that are not divisible](https://practice.geeksforgeeks.org/problems/number-that-are-not-divisible/0)[Excel Sheet | Part – 1](https://practice.geeksforgeeks.org/problems/excel-sheet/0)[Consecutive elements](https://practice.geeksforgeeks.org/problems/consecutive-elements/0)[Count all possible paths from top left to bottom right](https://practice.geeksforgeeks.org/problems/count-all-possible-paths-from-top-left-to-bottom-right/0)