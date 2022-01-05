# 亚马逊面试体验|第 303 集(校内)

> 原文:[https://www . geesforgeks . org/Amazon-面试-体验-设置-校园 303/](https://www.geeksforgeeks.org/amazon-interview-experience-set-303-on-campus/)

**第 0 轮:(笔试):20 道 MCQs + 2 道编码题**

MCQs–主题: [OS](https://www.geeksforgeeks.org/quiz-corner-gq/) 、 [DS](https://www.geeksforgeeks.org/quiz-corner-gq/) 、[DBMS](https://www.geeksforgeeks.org/quiz-corner-gq/)–(序列化等。)，[资质](https://www.geeksforgeeks.org/quiz-corner-gq/)(简单[拼图](https://www.geeksforgeeks.org/category/puzzles/)种类。)
编码问题:

*   [给定一个字符串输出反向字符串](https://practice.geeksforgeeks.org/problems/reverse-words-in-a-given-string/0)(字符串可以在单词之间有多个空格)。
    例:
    i/p:我是一个骄傲的印度人。
    o/p:
    印度骄傲的我是一个
*   [Given a no in string format output another string which is the biggest no formed from using same digits , otherwise print -1:](https://practice.geeksforgeeks.org/problems/next-permutation/0)

    ```
    i/p:
    0000
    132
    4312
    11
    o/p: 0
    321
    432
    -1

    ```

    所以解决办法是:给定一个整数数组，用数组的数字来找到最大的数字

**第 2 天:(面试回合)**

**第 1 轮(技术面试–约 45 分钟。)**
采访从他的介绍开始，他的部门是什么，他们是做什么的等等。

*   [给定一个 0 和 1 的链接列表，对其进行排序，使所有的 0 都在开头，1 在结尾。](https://practice.geeksforgeeks.org/problems/given-a-linked-list-of-0s-1s-and-2s-sort-it/1)必须到位。
    你不能只交换指针的值。将保持 0 和 1 的顺序。我必须在检查所有边界条件的情况下，为此编写生产级代码！
*   再给定一个 0 和 1 的数组和一个变量 k，打印包含精确 k ^ 0 的最小窗口的大小。
    *   关于最佳优化方法的讨论。
    *   我通过存储所有 0 的索引并计算每 k 个元素的最小差异 b/w 来解决这个问题。

**第 2 轮(技术面试-约 1 小时。)**
面试官让我先自我介绍，然后是我的项目。

*   [一个人要过马路，每走一步他要么获得一些能量，要么失去一些(这个信息是以数组的形式提供的)。找出他应该开始的最小能量，以便在任何水平上他的能量不小于 1)。](https://practice.geeksforgeeks.org/problems/minimum-energy/0)
    简单的题做在 O(n)上。
*   如何求解(a*b)%m，其中 a，b，m 都是 10^15.的阶模的分配性质是一回事。
    建议的第一种方法是打破二进制的否定，例如:[(2^5+2^3+2^0)*(2^5)]%[(2^3+2^2+2^0)]是可行的，但他想要更快的方法。
    我建议使用分治法(递归求解)的 O(lg b)方法。
*   他问我是否知道数据结构 [Trie](https://www.geeksforgeeks.org/trie-insert-and-search/) ，我听说过它和它的使用，但从未实现过。他简单解释了一下它是什么，然后告诉我对它的结构和功能进行编码(寻找/添加一个新单词)。
    然后问了几个关于它的问题，一些它会动摇的情况，一些关于它的更多讨论。

**谢谢极客们！结果–选定🙂**

如果你喜欢极客博客并想投稿，你也可以写一篇文章并把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。

如果发现有不正确的地方，请写评论，或者想分享更多关于以上讨论话题的信息

[All Practice Problems for Amazon](https://practice.geeksforgeeks.org/company/Amazon/) !