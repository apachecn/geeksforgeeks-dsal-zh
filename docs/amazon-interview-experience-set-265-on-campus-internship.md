# 亚马逊面试体验|第 265 集(校内实习)

> 原文:[https://www . geesforgeks . org/Amazon-面试-体验-设置-265-校园-实习/](https://www.geeksforgeeks.org/amazon-interview-experience-set-265-on-campus-internship/)

亚马逊最近访问了我们的校园，招聘实习生进行 6 个月的实习。

**第一轮:线上测试**
第一轮是 90 分钟的线上测试。它被托管在黑客银行平台上。共有 20 道 MCQ 题和 2 道编码题。MCQ 问题每题 1 分。每一个错误的 MCQ 答案都有 0.25 的负面评分。MCQ 的问题来自数据结构、数据库管理系统、能力等。

编码问题是:
Q1。[反转给定字符串中的单词](https://practice.geeksforgeeks.org/problems/reverse-words-in-a-given-string/0)

Q2。[电话号码中可能出现的单词](https://practice.geeksforgeeks.org/problems/possible-words-from-phone-digits/0)

注意:至少做一个编码问题来清除这一轮非常重要。即使你把你的 20 个 mcq 都答对了，但是你没有做任何编码题，那么你被选中的机会是非常低的。我建议每个人在最初的 30 分钟内做所有能做的 mcq，然后用最后 60 分钟做编码题。

我做了 15 道 mcq 和 2 道编码题。我被选中参加下一轮。总的来说，有 19 名学生被选中参加下一轮。

**第二轮:面试**
面试官首先问了我一个我在简历中提到的项目。然后他问了我两个问题。

Q1。给我们一个映射:A 映射到 1，B 映射到 2，C 映射到 3……Z 映射到 26。给我们一个数字 n，我们必须用给定的映射来告诉这个数字 n 可以组成多少个不同的字符串。例如，

输入:121
输出:3

说明:我们可以把数字 n 读作 1、2 和 1。形成的字符串将是 ABA (1=A，2=B)。我们也可以把数字 n 读作 12 和 1。形成的字符串将是 LA (12=L，1=A)。我们也可以把数字 n 读作 1 和 21。形成的字符串将是 AU (1=A，21=U)。因此，我们可以使用给定的映射从数字 121 中形成最多 3 个不同的字符串。

我给出了一个递归解，面试官对我的解很满意。所以他让我把我的解决方案写在纸上。我编写了解决方案，然后他检查了我的代码。一旦他满意了，我们就继续下一个问题。

Q2。[https://www . geesforgeks . org/remove-BST-keys-超出给定范围/](https://www.geeksforgeeks.org/remove-bst-keys-outside-the-given-range/)

过了一会儿，入围名单公布了。10 名学生入围下一轮。我也入围了下一轮。

**第 3 轮:最终面试**
这是流程的最终面试。互联网浏览者首先让我自我介绍，然后他问我关于我的一个项目。然后他问了我几个问题，如下:

Q1。什么是二叉树？BT 中有哪些不同类型的遍历？这些旅行有什么不同？哪个遍历是基于 BFS 的，哪个是基于 DFS 的？

我恰当地回答了问题。他对我的回答很满意。

Q2。[螺旋形式的层级顺序遍历](https://practice.geeksforgeeks.org/problems/level-order-traversal-in-spiral-form/1)
有一次我给他解，他让我在纸上编码。他用一些测试用例手动检查了我的解决方案。一旦他满意了，我们就进入下一个问题。

Q3。什么是最大堆？什么是最小堆？堆在现实生活中有哪些应用？

Q4。如何在堆中插入？时间复杂度是多少？

Q5。如何从最小堆中删除最小元素？时间复杂度是多少？

Q6。给定一个 n 个数的数组，我如何从数组中构建一个最小堆。时间复杂度是多少？

我恰当地回答了他。我告诉他，我们可以用 O(n)时间复杂度解决上述问题。然后他让我证明复杂性是 O(n)。我用一个数组例子证明了这一点。他对我的回答很满意。

Q7。有一个不断的数字流从一些无限的数字列表中进入，从中你需要维护一个数据结构，以便在任何给定的时间点返回前 100 个数字。假设所有的数字都是整数。

索尔:我用最小堆给了他一个解决方案。我们可以创建 100 个元素的最小堆。前 100 个元素很容易处理。假设我们得到了列表中的第 101 个元素。如果这个数字小于二进制堆的根，那么我们就不需要做任何事情。如果这个数字大于二进制堆的根，那么我们需要用这个元素替换根元素，并在二进制堆的根上调用向下渗透过程。

我的面试官用这个问题结束了我的面试。

我建议每个人在他们的亚马逊选择过程之前，至少要经历 5 个来自 geeksforgeeks.com 的人的亚马逊面试经历。最后，我想说关注数据结构、操作系统、数据库管理系统和网络。在数据结构中，主要关注二叉树、二进制堆和链表。

如果你喜欢极客博客并想投稿，你也可以写一篇文章并把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。

## 相关实践问题

[Operations on Binary Min Heap](https://practice.geeksforgeeks.org/problems/operations-on-binary-min-heap/1)[Reverse each word in a given string](https://practice.geeksforgeeks.org/problems/reverse-each-word-in-a-given-string/0)[All Practice Problems for Amazon](https://practice.geeksforgeeks.org/company/Amazon/) !