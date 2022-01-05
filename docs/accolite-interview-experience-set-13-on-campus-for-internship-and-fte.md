# Accolite 面试体验|第 13 集(校内实习和 FTE)

> 原文:[https://www . geesforgeks . org/acco lite-面试-体验-设置-13-校园实习和全时当量/](https://www.geeksforgeeks.org/accolite-interview-experience-set-13-on-campus-for-internship-and-fte/)

Accolite 参观了我们的校园，招聘全职员工和实习生。这个过程从预安置谈判开始，然后我们必须经历一个 5 轮的过程。

**第一轮:线上(30 分钟)**
第一轮线上进行，由 MCQ 的覆盖 [C](https://www.geeksforgeeks.org/quiz-corner-gq/) 、 [C++](https://www.geeksforgeeks.org/quiz-corner-gq/) 、 [OS](https://www.geeksforgeeks.org/quiz-corner-gq/) 、 [DBMS](https://www.geeksforgeeks.org/quiz-corner-gq/) 组成。我们必须回答 20 个问题，是的，每个错误的答案都有一个负分(-0.25)。
约 650 人参加线上考试，75 人入选下一轮。

**第 2 轮:纸张编码(1 小时)**
我们被要求在纸张上编码以下问题:
1。[打印最短路径在屏幕上打印字符串](https://practice.geeksforgeeks.org/problems/primitive-typing/0)
2。[查找要翻转的零，以便最大化连续 1 的数量](https://practice.geeksforgeeks.org/problems/maximize-number-of-1s/0)
3。[序列化和反序列化二叉树](https://practice.geeksforgeeks.org/problems/serialize-and-deserialize-a-binary-tree/1)

在参加这次考试的 75 人中，有 20 人入围。
第二天我们又进行了 3 次技术面试。

**第三轮:F2F 面试(2 小时)**
我是第一个入围的人，所以我被公司的高级技术总监面试了。她问我最喜欢的数据结构，我回答了树。所以她让我对一棵二叉树进行之字形水平顺序遍历。

1.  [螺旋形式的层级顺序遍历](https://practice.geeksforgeeks.org/problems/level-order-traversal-in-spiral-form/1)
2.  然后她给了一个编码形式的字符串，让我在不解码的情况下找到字符串中的第 k 个字符。
    **例如:**
    **输入:**编码字符串为“a9b21c5”，k=27
    **输出:**‘b’
3.  然后她给了我一个她上周面临的实时问题，并要求我提供一个解决方案并对其进行编码。
    场景:有一个从套接字接收数据的应用编程接口，该套接字是使用缓冲区获取的。无法保证通过套接字读取了多少数据(即第一次可以读取 5 个字符，第二次可以读取 20 个字符)。要读取的数据由 HTTP 头和要显示的消息组成。标题通过分隔符(这里是“000|”)与标题分开。我不得不编写一个代码来丢弃 HTTP 头并单独显示消息，因为没有办法找出套接字读取了多少字符。
    她最后问了我的项目。

**第 4 轮:F2F 面试(1.30 小时)**
面试要求我对以下问题进行编码:

1.  [收集雨水](https://practice.geeksforgeeks.org/problems/trapping-rain-water/0)
2.  [给定一个链表和一个整数‘k’，我不得不旋转链表。](https://practice.geeksforgeeks.org/problems/rotate-a-linked-list/1)(注:反转链表不同)
    输入:1->2->3->4->5->6->7->8->9->10 和 k=4
    输出:4->1->2->3->8->5->6->7->
3.  他给了我一个由二叉树表示的字符串(每个叶节点是一个字符)和一个随机函数，该函数可以交换二叉树的任意数量的内部节点(就像镜像一样)。我必须找出随机函数调用后返回的字符串(由树表示)是否是原始字符串的有效排列。
    Eg: **输入:**“金色”和“gloned”，其中 gloned 是调用随机化函数后返回的字符串。
    **输出:**真
    **输入:**【金色】【gnlode】
    **输出:**假

**第 5 轮:F2F 面试(1.30 小时)**
面试官给了我两个场景，让我两个都写一个算法。
**场景一:**
我必须从钦奈坐飞机到达巴黎。他想让我找到到达巴黎的最佳途径。我告诉他，我会使用基于距离的 [Djikstra 算法](https://practice.geeksforgeeks.org/problems/shortest-path-from-1-to-n/0)，一个基于时间的解，一个基于距离和时间的解(使用加权平均)。然后他让我尽量减少每个中间顶点要考虑的点数。我告诉他用经纬度找到目的地的方向，并据此考虑点。然后他让我在起点和终点之间画一条线，并让我只考虑在所画线 30 度倾角以内的点。我给他一个解决方案，他很满意。

**场景 2:**
他让我假设我所在的城市有 100 个机场，他让我给出一个算法，根据目的地和每个机场每个航班的时间选择机场。然后，他让我在从当前位置前往机场的过程中融入“交通”的重要性，并要求我进行相应的设计。他问我有没有问题要问他，我问了很多关于公司结构、客户和加入公司前需要学习的任何先决条件的问题。

晚上晚些时候公布了结果，我被选中了！！！

如果你喜欢极客博客并想投稿，你也可以写一篇文章并把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。

如果发现有不正确的地方，请写评论，或者想分享更多关于以上讨论话题的信息

[All Practice Problems for Accolite](https://practice.geeksforgeeks.org/company/Accolite/) !