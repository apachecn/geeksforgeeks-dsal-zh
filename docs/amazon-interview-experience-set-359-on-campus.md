# 亚马逊面试体验|第 359 集(校内)

> 原文:[https://www . geesforgeks . org/Amazon-面试-体验-设置-校园 359/](https://www.geeksforgeeks.org/amazon-interview-experience-set-359-on-campus/)

20 个 MCQs 混合了简单的 Quants、logical、其他技术 CS 概念(TOC、DS、DBMS、NETWORKS)

2 道编程题(我都解决了)

1.  **[Maximum nonadjacent subsequence](https://practice.geeksforgeeks.org/problems/stickler-theif/0)**

使用 max(前一个元素的独占+ arr[i])的想法。如果需要，请查看极客视频或图沙罗伊视频。

2.  **Profit sorting (finding the number of elements in a given range)**

(在做的

**o(n)** 对于每个查询，由正常进行循环遍历

**o(log(n))**对于每个查询，通过排序和使用二分搜索法我们可以传递 TLE (Time Limit Error)然后最后，我使用 Hashing 解决了它然后像 **一样进行计数排序** 算法所以

**o(1)** 对于每个查询(因为问题的最大空间复杂度为 **256MB** 所以不会有问题)MOST OPTIMAL ONE。

<u>**面对面访谈:**</u>

**4 总计= 3 个技术，1 个技术+酒吧加注轮次**

**首轮:(1 小时)**

*   Tell me about yourself?
*   How are your resettlement preparations?
*   How was your previous company interview?
*   Which DS is comfortable for you? (Some panels are tricky, just ask other DS)
*   [Merge the two sorted linked lists into one sorted](https://practice.geeksforgeeks.org/problems/merge-two-sorted-linked-lists/1) (further optimized code)
*   By covering all Edge cases (avoiding wild pointers)
*   A modified DFS with recursion problem
*   Do you want to ask any questions?

**第二轮:(40 分钟)**

*   What is your passion for technology?
*   Write code to connect the leaf nodes of binary tree like a doubly linked list (use Post Order or arbitrary traversal to track the previous nodes and check whether they are leaf nodes. Note: Avoid dangling or wild pointers when writing code, and initialize variables to null)
*   Do you want to ask any questions?

**第三轮:(1:20 小时。)**

**(PROBLEM solution+有点像 STRESS INTERVIEW)**

*   U has two <sup>N</sup> players. They compete with each other and each player has a ranking. Can you tell us what the winner is like?

(问题和这个一样，我问了很多澄清(收到压力然后回答)并尝试了 Graphs，根据 Ranking 对玩家进行排序他说不需要，要求高效一然后我用 **比武树**(2<sup>n</sup>是使用比武树的线索)他很满意。

*   Write a code to convert a palindrome number into the next directly higher number, which is also a palindrome, for example, 1221 = > 1331 (consider the edge cases like 99 and 191 before encoding, which will reduce the number of hits on the paper, and in the case of 9, U must be carried to the next element)

为了更好地理解，也请评论您附近的代码。

*   What is the scheduling algorithm? What is your computer using? (Multiple feedback queue) He doesn't accept round robin.

**速射轮:**

(这些很有挑战性，因为他希望回答得更快！)

*   Why should I hire you?
*   What books have you read recently?
*   What is your biggest mistake?
*   What is your strength?
*   What is your weakness? How did you overcome it?
*   What do you want **to change in Amazon** ?
*   Why was your ICICI project rejected at the next level?

**最后一轮(1 小时)测试 BASIC CS 概念更多**

*   First of all, I received a compliment from the interviewer on my fast paper coding skills (previous panel review).
*   Do you like Android or iOS? Me: Android! Then take your mobile phone and write a code to **to simulate Android mode lock** , take my mobile phone and understand what mode is possible, and then

(我用递归和回溯进行了求解和编码)

矩阵可以是 N×N 模式框。

<u>2 个子问题:</u>

1。检查给定图案是否可能(使用角度 90°或 180°)

2。打印给定长度和起点的所有可能图案

边角箱要盖好！

*   Tell me about the project?
*   Is your forum (project) hosted in your college?
*   Why did you use NoSQL in your project?
*   Why can't I use MySQL? Where is it used?

(使用 BookMyShow app 确切解释了 ACID 属性)

*   What happens when you start the computer? (from the BIOS stage)
*   What is the kernel?

我解释了我知道的一切，最后我也解释了安卓手机内核。他印象深刻，喜欢停止进一步的简单问题。

*   How does the computer perform things? Program counter. Explain more.
*   How are variables stored? Depending on the register or main memory. Explain more.
*   When you have secondary memory, why is it main memory or register?
*   How does the program run (step)? Explain programs like C to assembly language to binary code.
*   Program vs process (I tried to explain the thread, he stopped me and then the next one)
*   **Design a DS** problem

你有一个单词词典( **不一定** 按照我们英语词典给出的顺序)

你将如何搜索单词(使用拓扑排序并解释了 **为什么** 和 **如何工作** 他确信)

*   What is the difference between abstraction and encapsulation?
*   Why use ER diagram? (I gave a clue to normalization, which leads to the next question)
*   Then why should we normalize it?
*   Take an example **Abnormal** If we don't normalize, I will use an example database to explain.
*   How do threads communicate? Files, pipes, etc.
*   Have you participated in any coding contest?
*   Do you want to ask any questions?

都是一天搞定的。我非常感谢极客们，极客们帮我做了安置准备。它过去和现在都非常有帮助！！

如果你喜欢 GeeksforGeeks 并且想投稿，你也可以用[contribute.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。

如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。