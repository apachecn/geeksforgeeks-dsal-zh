# Accolite 面试体验|第四集(校内)

> 原文:[https://www . geesforgeks . org/accolite-面试-体验-设置-4-校园/](https://www.geeksforgeeks.org/accolite-interview-experience-set-4-on-campus/)

**第一轮(笔试)**
约有 140 名学生参加线下考试。

30 分钟内要完成 20 个 mcq，问题来自操作系统、数据库管理系统和数据结构。
在那一轮编码之后，有 3 个问题(纸质编码)，我们必须尝试任何 2 个(1 小时)

1.[编写自己的 sqrt()函数。](https://practice.geeksforgeeks.org/problems/count-squares/0)如果是完美平方，函数应该返回平方根，否则返回 floor(sqrt(x))
2。[给定一个包含正整数和负整数的数组。你必须找到最小的缺失正数。](https://practice.geeksforgeeks.org/problems/smallest-positive-missing-number/0)你的代码应该在 O(n)时间和 O(1)空间中运行。
3。[给定一个字符串数组，找出字符串是否可以链式连接形成一个圆。](https://practice.geeksforgeeks.org/problems/circle-of-strings/0)如果 x 的最后一个字符与 y 的第一个字符相同，则可以将一个 x 放在另一个 y 之前。

第一轮后，19 人入围面试。

**第 2 轮(技术)(1:30 小时)**
1。说说你自己吧。与此同时，他(面试官)看了我的简历，询问了我的项目。
我做了 3 个项目，所以他开始讨论 CUDA 和并行编程，以及你如何在图像上实现边缘检测和实现了多少增益系数。
其次，我做了一个关于在线投票系统的项目，所以他让我画 E-R 图、模式以及它们和它们的功能之间的关系。大约(25-30)分钟的讨论。

2.[给定一个 BST，你必须在 O(n)时间和 O(1)空间中找到其中的第 k 个最小元素](https://practice.geeksforgeeks.org/problems/find-k-th-smallest-element-in-bst/1)。

3.假设您有一个服务器，在时间 t1、t2 有多个请求，现在假设一个用户在任何特定的时间 t 点击服务器，那么服务器应该返回最后一个请求。你必须为其设计数据结构。
我建议我们可以使用堆栈来返回最后一个请求，然后他让我对最后 10 个请求做什么，然后我建议使用结构数组来存储请求号和时间戳。现在，在任何时间 t，我们都可以向后移动 10 个元素，但是他说，假设用户经常点击，那么每次我都必须一次又一次地来回遍历，因此时间复杂度会高得多，我同意并建议了另一个类似于 LRU 实现的解决方案，以便可以更快地处理频繁出现的请求。然后他修改了一个问题，用户想要最后 1 分钟的请求，他给出了一个提示，有必要存储所有请求吗？我们不能只存储每 1 分钟的请求，然后突然它点击了我，我建议使用 deque 60 秒。现在假设请求在第 61 秒到达，然后我们可以在后面添加它，从前面删除一个，保持 60 秒的窗口。他很满意，但他希望不应该有删除，所以我告诉他使用循环德奎，这样我们就可以取代以前的元素。他现在对这种方法完全满意。(大约 35 分钟。讨论)

4.[给定一个包含 30 天股价的数组。一个人有 1 份股票，他可以买卖任何次数，你必须找到可以赚取的最大利润。](https://practice.geeksforgeeks.org/problems/stock-buy-and-sell/0)
我建议一种方法，从左创建两个辅助数组 MIN，从右创建 MAX，如果 MAX[i]和 MIN[i]之间的差大于 maxDIff，则同时遍历这两个数组，然后更新 maxDiff 并存储当前索引，如果 index+1 不等于当前迭代索引，则添加到 sum，最后返回 sum。他对我的代码进行了一些测试，发现在某些情况下给出了错误的答案，然后他问我对动态编程的命令怎么样，我告诉他我只知道标准的，没有其他经验，然后他说这个问题是关于动态规划的，但是他很高兴看到我的方法。(大约 20-25 分钟。)

**第 3 轮(技术)(1:30 小时)**
1。她(面试官)问我笔试有没有尝试第三题，我说我只尝试了第一题和第二题，然后她给了我试卷，让我实施第三题。
我提出了一种使用两个结构数组(第一个字符和最后一个字符)的方法，这两个数组将包含布尔值来标记字符串中字符的存在及其索引。现在比较两个数组，看看这两个数组是否有相同的布尔值和所有第一个和最后一个字符的不同索引。如果是这样，那么字符串可以形成一个链，否则不行。她对我的解决方案有疑问，所以她找到了一个测试案例，我的代码给出了错误的答案，所以她告诉我寻找另一个解决方案，我想出了另一种方法，并告诉她我们可以从第一个和最后一个字符制作一个有向图，然后在 DFS 中遍历它， 现在假设再次访问被访问的节点，并且总被访问节点的计数与总节点数相同，那么我们可以说字符串将形成一个链，现在她对方法很满意，并要求我编写代码，现在由于我的图很弱，我很震惊，所以她说只编写伪代码。

2.[给定一个 BST，你要在 O(n)时间和 O(1)空间中找到其中第 kth 个最大的元素](https://practice.geeksforgeeks.org/problems/kth-largest-element-in-bst/1)。
我建议声明一个静态变量 count，如果节点按顺序被访问，它将增加 count，如果 count 变成 k，我将打印该节点的数据并返回。然后她问我静态是怎么工作的，全局和静态的区别。

3.[给定一个诺基亚手机的移动键盘和一个包含所有可以构成的有意义单词的字典，](https://practice.geeksforgeeks.org/problems/possible-words-from-phone-digits/0)假设现在用户键入一些数字(输入)，那么您的程序必须建议字典中存在的所有有意义的单词。在实现这个之前，她问我数据结构如何有效地存储字典，然后你将如何使用这个数据结构来编写代码。
首先，我建议我将字典存储在二维数组中，并按字典顺序对其进行排序，现在假设用户键入一个数字，在数组中搜索以该字符开头的字符串。她说要降低复杂度，因为字典可能包含 1000 个单词，后来我建议用 trie datastructure 来存储和搜索字符串，她现在很满意，让我解释这个概念。
4。[给定一个图的前序和后序，如何构造这个图。](https://practice.geeksforgeeks.org/problems/construct-tree-1/1)
当我听到这个问题时，我愣了 2 分钟，然后我说就图形而言，我不知道它，但是一个独特的树不能用前序和后序来构建，所以图形，所以需要有序，她很高兴并同意了答案。

**第 4 轮(技术)(2:30 小时)**
1。假设给定一个链表，并且有一个循环，你必须在 O(n)时间内找到孤立节点。孤立节点是循环之外的节点。

2.设计一个 BRTS 交通信号系统，这样就不会有两辆车发生冲突。请注意，BRTS 巴士将沿 BRTS 交通信号灯 B1、B2、B3、B4 分 4 个方向行驶，常规交通将仅沿常规交通信号灯 R1、R2、R3、R4 行驶。在输入中，仅给出了最大周期时间(该过程重复的时间)，检查所有弯道情况(交通灯只有两种状态(红色和绿色))。你必须在最大周期时间内告诉任何一种可能的交通灯组合。(约 1 小时讨论)。

3.[假设给定了一个链表，但是我们不知道节点的个数，你必须在不计算节点个数的情况下找到倒数第 k 个节点。](https://practice.geeksforgeeks.org/problems/nth-node-from-end-of-linked-list/1)
4。给定一个 n 个整数的数组，这样一些元素在 0 到 n-1 的范围内，一些超出范围的元素可能是负的。您必须重新排列数组，以便范围内的所有元素都出现在它们的索引中，其余的元素以排序的方式出现在不存在的索引中。这应该在 O(n)时间和 O(1)空间内完成。
Eg-假设 n=6，4 5 2 3 6 -3 输出= -3，6，2，3，4，5

5.你如何使用队列实现堆栈。
6。如何借助队列对元素进行排序？
我建议一个 O(n)时间解决方案和 O(n)额外空间。他要求在 O(1)空间做，所以我建议他去，他似乎很满意。

直到这一轮只有 4 个被选中(我就是其中之一)

**第 5 轮(酒吧加注者)(30 分钟)**

1.[求从索引 0 开始的字符串中最长回文的长度。](https://practice.geeksforgeeks.org/problems/longest-palindrome-in-a-string/0)
2。[查找字符串 B 中是否存在字符串 A。](https://practice.geeksforgeeks.org/problems/check-for-subsequence/0)
3。查找字符串中最长前缀的长度

在这之后，两个最终被选中，不幸的是，我不在其中，因为他们可能认为我压力不大。最后，我建议你的方法和概念必须是强有力的，因为它们总是给出有一些变化的问题。

如果你喜欢极客博客并想投稿，你也可以写一篇文章并把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。

Related Practice Problems[Smallest Positive missing number](https://practice.geeksforgeeks.org/problems/smallest-positive-missing-number/0)[Count Squares](https://practice.geeksforgeeks.org/problems/count-squares/0)[Circle of strings](https://practice.geeksforgeeks.org/problems/circle-of-strings/0)[Check for subsequence](https://practice.geeksforgeeks.org/problems/check-for-subsequence/0)[Stock buy and sell](https://practice.geeksforgeeks.org/problems/stock-buy-and-sell/0)[Longest Palindrome in a String](https://practice.geeksforgeeks.org/problems/longest-palindrome-in-a-string/0)

[**雅高**](https://practice.geeksforgeeks.org/company/Accolite/) **所有练习题！**