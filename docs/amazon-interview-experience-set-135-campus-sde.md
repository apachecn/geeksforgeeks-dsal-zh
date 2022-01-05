# 亚马逊面试体验|第 135 集(SDE 校内)

> 原文:[https://www . geesforgeks . org/Amazon-面试-体验-设置-135-校园-sde/](https://www.geeksforgeeks.org/amazon-interview-experience-set-135-campus-sde/)

最近，亚马逊参观了我们的校园，我被面试了 SDE 的职位。以下是我的面试经历:

**线上回合:(时长–90 分钟)**
20 道 MCQs 和 2 道编码题。MCQs 涉及算法、时间复杂性、定量能力、概率、操作系统、图表、数据结构、递归输出等。
编码题:
1。在亚马逊的一个履行中心，有许多空盒子保持连续递增的顺序。Kiva 机器人被设计成将产品放在盒子里。给出了产品尺寸。设计一个程序，为给定的产品尺寸找到最合适的盒子。第一行包含空盒子的数量，下一行包含有空格的盒子的大小。下一行包含给定产品的尺寸。输出显示最适合的盒子大小，否则显示-1。

```
For example, Input: 6
                  2 7 9 11 13 16
                           12
            Output: 13 
```

2.[你要在二维数组中找到一个字符串。输入包含二维字符数组和给定字符串](https://practice.geeksforgeeks.org/problems/find-the-string-in-grid/0)。你可以朝八个方向中的一个移动。如果完全找到字符串，输出包含字符串首字母的位置，否则返回-1。如果可能，接受多个答案中的任何一个。
例如，输入:
b t g
p a d
r k j

串:鼠
输出:(2，0)

**F2F 第一轮:**
简单介绍一下我自己和我的项目。
1。[给定一个正负整数数组，在 0(n)时间内重新排列正负数字。](https://practice.geeksforgeeks.org/problems/array-of-alternate-ve-and-ve-nos/0)
首先，我用 2 个数组来求解，每个数组为正整数和负整数，并将数组的元素放在这 2 个数组中，然后通过从每个数组中取一个元素来组合它们。然后他告诉我没有多余的空间。然后我用 quicksort 分离了正负元素。

2.检查字符串是否相互旋转的程序。我走近如下:

然后他告诉不用 strstr 就能解决。我用天真的搜索方法。

**F2F 第 2 轮:**
简介和一些行为问题。
[给定一个 BST 和一个 key 和，设计一个算法来寻找所有和等于 key 的整数对。](https://practice.geeksforgeeks.org/problems/find-a-pair-with-given-target-in-bst/1)
我首先使用一个数组，并以有序的方式将元素放入其中，然后找到配对。他告诉我原地做，我用 2 次遍历(中序和反序)解决。

**F2F 第 3 轮:**
基于 CS 基础，也对我的实习项目进行了 15 分钟的讨论。
1。当我们输入 Amazon.com 时会发生什么？
2。如果我们想从一个账户转到另一个账户，请详细描述交易过程。也为它设计模式。
3。服务器端在接收 HTTP 请求时会发生什么，操作系统如何交互，以及与线程、线程池、同步、散列等相关的讨论。
4。详细描述 ACID 属性。

**酒吧募捐轮:**
1。给定一棵二叉树，full_path_sum 是路径中从根到叶的所有节点的总和。给定一个最小和值，如果 path 的 full_path_sum 小于 min_sum，则删除节点。删除所有此类节点。例如，

```
Given min_sum =8        
        1
    2        3
 4          5       6           7
So we delete 4.
```

2.[如何在 BST 中找到 kth-最小元素？](https://practice.geeksforgeeks.org/problems/find-k-th-smallest-element-in-bst/1)

谢谢极客们在我准备期间给了我很多帮助。

如果你喜欢极客博客并想投稿，你也可以写一篇文章并把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。

[All Practice Problems for Amazon](https://practice.geeksforgeeks.org/company/Amazon/) !