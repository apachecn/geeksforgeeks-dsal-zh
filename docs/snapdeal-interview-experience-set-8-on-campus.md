# Snapdeal 面试体验|第八集(校内)

> 原文:[https://www . geesforgeks . org/snapdeal-面试-体验-设置-校园 8/](https://www.geeksforgeeks.org/snapdeal-interview-experience-set-8-on-campus/)

上周一月，Snapdeal 在我的校园里为软件开发人员进行了一次安置活动。资格-所有 CSE(无指针标准)

**在线测试-**

1 小时内 21 (MCQ) +2(编码)。在黑客银行上进行测试

21 MCQ 有将近 10 个能力倾向和 11 个基于 C 输出的问题。
优先考虑编码问题。试着解决这两个问题(通过其中一个问题的所有测试用例，并尝试另一个问题(即使暴力也能通过许多测试用例)
智能不能在一分钟内解决。先解决基于 C/o/p 的问题。

提问-
1。[叠画，找到能看清楚的画的数量，给出画的极端坐标。绘画的排序很重要。](https://practice.geeksforgeeks.org/problems/overlapping-rectangles/0)(假设所有画的高度都一样，给出开始和结束坐标)

```
E.g.
5
1 4
2 6
3 4
8 10
7 10

XXXX
   XXXXXX
      XX
           XXX   简单的 O(N^2)解决方案。从最右边的绘画开始，检查它是否完全隐藏了任何绘画或不基于开始和结束坐标。(区间选择问题的修改)2- [给定两条线段 A(x1，y1 x2，y2) & B(x3，y3 x4，y4)的点，求这 2 条线段是否相交。](https://practice.geeksforgeeks.org/problems/check-if-two-line-segments-intersect/0) 
更简单的方法(短代码)-
[http://community.topcoder.com/tc?module=Static&D1 =教程&D2 =几何# line _ line _ 交集](http://community.topcoder.com/tc?module=Static&d1=tutorials&d2=geometry2#line_line_intersection)长度/复杂 soln-
[https://www . geeksforgeeks . org/check-if-two-给定线段-intersect/](https://www.geeksforgeeks.org/check-if-two-given-line-segments-intersect/) 预期截止- 
第二题我解决了，第一题通过了 1 个测试用例(在线轮的时候误会题了！！:p)并解决了 4 个 MCQ 唯一的(全是侥幸)
所以我的建议是，务必在最后 15 分钟内解决编码问题和 C o/p 问题**第 1 轮–F2F 技术**T2 平均 20-30 分钟。22 入围
我的持续 1 小时到 1 小时 15 分钟基于讨论的实习(20-30 分钟)。基于云、虚拟化、网络
 Q1-给定 N，从从 2 到 N 的所有数字中找出 LCM。给出以质数< = n 的形式表示的复杂度。在复杂度方面必须非常精确(质数因子、最大重现、每次重现)。关于复杂性的长时间讨论。不要说任何你无法证明的方法。(例如，说我可以使用筛子埃拉托斯特尼进行预处理将导致问题是 o( log logn ),被证明是微不足道的。)所以避免使用这样的 q3- spring hibernate java 告诉他只工作 c c++。没有经验 Q2-type sql-no SQL 和 SQL(关系型 dbms)为什么需要 nosql-大数据分析如何设计 snapdeal 网站的 shoe 部分。现在如果想进一步将其细分为运动休闲 db 或者增加另一个实体呢？完整的证明最初用多级索引结构存储来回答。无法回答第二部分的问题。他问知否知否 dbms。跳过已结束的面试。高级实验室我目前在毕业前学习的课程。**第 2 轮-编码回合(2 小时)
 10 入围
 Q1- [将图像旋转 90 度](https://practice.geeksforgeeks.org/problems/rotate-by-90-degree/0) 
 Q2- [给定一个单词序列，将所有字谜打印在一起](https://practice.geeksforgeeks.org/problems/k-anagrams-1/0) 
 Q3- [找到一个和给定值](https://practice.geeksforgeeks.org/problems/triplet-sum-in-array/0)** **相加的三元组我是第一个在大约 45 分钟内解决所有 3 个问题的人，然后去参加下一次面试。入围标准-1 小时内 2 个问题–1 小时 15 分钟，尽管他们说我们有 2 小时来解决所有 3 个问题！！** **第 3 轮- F2F 技术** 
第 4 轮入围。自从我最早解决第二轮的问题以来，这一轮对我来说持续了将近 1 小时 45 分钟- 2 小时。其他 3 人接受了将近 45 分钟的采访。

 Q1-变异的
 [从电话号码中打印所有可能的单词](https://practice.geeksforgeeks.org/problems/possible-words-from-phone-digits/0) 
给定一个单词字典和一个数字 n，找出字典中所有可以由给定数字 n 组成的单词的个数
我从指数解开始，并将其简化为多项式。我们讨论了各种方法，尝试了各种方法，经过 1-1.5 小时的讨论，最终得出了一个带有一些预处理开销的 O(1)解决方案。在达到 O(1)时间复杂度后，他要求进一步优化空间复杂度。
特里尔/ TST 的用法。哈希结构的内部实现，并使用 Trie / TST 替换哈希机制。

Q2——给定一个元素数组。我们只能执行以下操作——增加一个数组元素。操作成本是每个数组元素的增量。现在对于给定的 H，我们需要以最小的代价使数组的任意 H(不一定是连续的)元素相等。

例如
 N=6，H = 4
2 3 5 6 4

T35】变更为->4 4 5 6 4
成本为(4-2+4-3 = 3)T38】N = 6，H = 3
2 3 5 6 4T41】变更为->2 4 5 6 4
成本为(4-3 = 1 

我要感谢 geeksforgeeks 提供了一套详尽的面试问题和关于数据结构-算法的学习材料。

如果你喜欢 GeeksforGeeks，愿意投稿，也可以写一篇文章，把文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。

   [所有练习题为 snapdate](https://practice.geeksforgeeks.org/company/Snapdeal/)！   

## 相关练习题

  [将字谜组合在一起](https://practice.geeksforgeeks.org/problems/k-anagrams-1/0) =>->
```