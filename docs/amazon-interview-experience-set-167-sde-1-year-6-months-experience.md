# 亚马逊面试经验|第 167 集(SDE I 为 1 年 6 个月经验)

> 原文:[https://www . geesforgeks . org/Amazon-面试-经验-设置-167-sde-1 年-6 个月-经验/](https://www.geeksforgeeks.org/amazon-interview-experience-set-167-sde-1-year-6-months-experience/)

**第一轮:在线编码第一轮**
共有 4 道编码题。被要求回答 4 个中的 2 个。
1) [给定一个 N 个硬币的列表，它们的值(V1、V2、…、VN)和总和 S。找出总和为 S 的硬币的最小数量(我们可以使用任意多的一种类型的硬币)，或者报告不可能以它们总和为 S 的方式选择硬币。](https://practice.geeksforgeeks.org/problems/number-of-coins/0)
示例:给定值为 1、3 和 5 的硬币。
和 S 之和为 11。
输出:3，3 的 2 个硬币，5 的 1 个硬币。

2) [给定两个矩形，找出给定两个矩形是否重叠](https://practice.geeksforgeeks.org/problems/overlapping-rectangles/0)

3) [给定 string1 和 string2 两个字符串，高效地找到 string1 中包含 string2 所有字符的最小子串。](https://practice.geeksforgeeks.org/problems/smallest-window-in-a-string-containing-all-the-characters-of-another-string/0)
例如:
输入字符串 1:“这是一个测试字符串”
输入字符串 2:“保存者”
输出字符串:“t stri”

4)我不记得这个问题了。

**第 2 轮:F2F 技术(Hyd)**
1) [印刷树之字形](https://practice.geeksforgeeks.org/problems/zigzag-tree-traversal/1)

2) [给定字符串的最长回文子序列。](https://practice.geeksforgeeks.org/problems/longest-palindromic-subsequence/0)
被要求写完整的代码。

 **第 3 轮:F2F 技术(hyd)**
1)对我的项目有很多疑问。
因为我的项目与多处理有关，所以有很多问题被问到为什么是多处理/为什么不是多线程、差异、什么是线程/进程、生产者消费者问题等等。

2)在 Linux 中设计一个文件结构。

3)我被要求为在排序链表中插入一个元素编写完美的代码，该代码应该覆盖所有的角情况。

 **round 3:F2F Technical(hyd)**
1)[给定一个单词数组，将所有的字谜打印在一起](https://practice.geeksforgeeks.org/problems/k-anagrams-1/0)。

2) [你有一个数组，它的 ith 值是给定股票当天的价格。你只能买一股股票，卖出一股。设计一个算法来寻找买卖的最佳时机。他还让我给出开始日期和结束日期。](https://practice.geeksforgeeks.org/problems/stock-buy-and-sell/0)
3)图题:
关键节点:如果一个节点只通过一个节点到达另一个节点。
例:A-C-B 和 A-E-B 是关键节点。(A 通过一个节点即 C 或 E 到达 B)
如果 A 通过多个节点到达 B，则它们不是关键节点。
1) A-C-B
A-D-E-B (A 通过 C 到达 B，这可能会导致关键节点，但 A 通过 D 和 E 有另一条通往 B 的路径，因此它们不是关键节点)。
2) X-Y-Z
X-A-Z (X 和 Z 为关键节点)
现在查找所有关键节点。

 **第 4 轮:F2F 技术(hyd)**
1)关于我的项目有很多问题。他让我为我的一个项目写伪代码。

2) Outlook:
服务器接收来自多个发件人的会议对象。会议对象包含会议时间、发送时间、收件人、发件人 id 等。当收件人来检查服务器时，他/她应该根据会议时间而不是发送时间来获取请求。关于空间复杂性和时间复杂性的许多讨论。
Eg:

```
12 PM      From: A  To: B,C,D   meeting time: 4 PM   meeting Id: 1
12.30 PM   from: A  To C,D      meeting time : 2 PM   meeting Id:2
1:PM       From B   To: C       meeting time: 1.30PM  meeting Id:3
```

当 C 请求服务器时，C 应该得到 ID3 作为第一次会议，ID2 作为第二次会议，ID1 作为第三次会议。

3)许多行为问题。

我要感谢 geeksforgeeks 帮我破解了面试。

如果你喜欢极客博客并想投稿，你也可以写一篇文章并把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。

[All Practice Problems for Amazon](https://practice.geeksforgeeks.org/company/Amazon/) !