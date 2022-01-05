# 亚马逊面试体验|第 384 集(FTE 校内)

> 原文:[https://www . geesforgeks . org/Amazon-面试-体验-设置-384-校园-fte/](https://www.geeksforgeeks.org/amazon-interview-experience-set-384-campus-fte/)

**在线编码轮次:**
平台:黑客帝国
时间:1.5 小时
试题格式:20 道 MCQs + 2 道编码题
MCQs 基于数据结构、OS、网络等。
编码问题:
1) [找到最大 j-i，使得 arr[j] > arr[i]](https://practice.geeksforgeeks.org/problems/maximum-index/0)
预期时间复杂度:O(n)
2) [找到数组中每个窗口大小的最小值的最大值](https://practice.geeksforgeeks.org/problems/maximum-of-minimum-for-every-window-size/0)
只有使用堆栈的优化解决方案(O(n))能够通过所有测试用例。

大约有 37 名学生从编码轮中被挑选出来，并被要求进行进一步的面试。

**Round1(面对面):**
时间:45 分钟
面试官很酷。她让我自我介绍，简单介绍一下我做过的项目。然后，她转向数据结构部分。
一个问题是，给定一个包含相同数量的正元素和负元素的数组，排列数组时，每个正元素后面都跟一个负元素。我告诉她 O(n)方法，首先以 0 为支点分离正负元素，然后交替排列。她让我写涵盖所有角落的代码。
第二个问题很简单[在给定 k 大小的组中反向链表。](https://practice.geeksforgeeks.org/problems/reverse-a-linked-list-in-groups-of-given-size/1)
她让我为此写代码。

**Round2(面对面):**
时间:45 分钟
面试官很酷，也很配合。他问我前一轮怎么样。然后他继续提问。
一个问题很简单[求二叉树的边界遍历。](https://practice.geeksforgeeks.org/problems/boundary-traversal-of-binary-tree/1)他让我写代码。
第二个问题是[在矩阵](https://practice.geeksforgeeks.org/problems/path-in-matrix/0)中找到最小成本路径。我告诉他使用 BFS 的方法，然后最终用带记忆的递归来解决它。然后他要求把我的方法写在纸上。他对我这一轮的表现印象深刻。

**第三回合(酒吧揭牌):**
时间:60 分钟
面试官是经理，也是小组成员的负责人。他让我自我介绍，我最喜欢的科目是什么。他问我解决了哪个我觉得很难的问题，以及在处理这个问题时出现了什么问题。然后他继续提问。
给了一个 n 元树的问题，对于树的每个第 k 层，从左边开始计数，打印该层的第 k 个节点，如果第 k 个节点不可用，则打印该层的最后一个节点。我告诉他使用级别顺序遍历的显而易见的方法。他让我写涵盖所有角落的代码。
另一个问题是股票只买卖一次。然后他把问题改成[多次买卖，最终利润最大化。](https://practice.geeksforgeeks.org/problems/stock-buy-and-sell/0)他不断通过修改问题约束来迷惑我。然后，他最终接受了我的解决方案，并要求我对该代码进行试运行。

**第 4 轮(面对面):**
时间:1.5 小时
这一轮主要是基于问题解决和各种 CS 科目如 OS、DBMS、OOP 等。他首先让我介绍我的项目，这是一个安卓应用程序。他问我这个应用的核心思想，布局等。他问我用什么在数据库中存储各种信息，我告诉他我用 MySQL 和 MySQL 语句，MySQL 语句是用 java 中的 URL 编码机制从 PHP 脚本中调用的。他问我在我的项目中面临的困难，以及我是如何解决这些问题的。然后他继续提问。
一个问题的陈述类似于[手机键盘问题。](https://practice.geeksforgeeks.org/problems/possible-words-from-phone-digits/0)但是有一个小小的变化，字典里的单词也是和一个数字一起给出的，我必须找到字典里的所有单词，只要按下这个数字就可以得到。我告诉他使用回溯的通常方法。他让我优化我的方法。他给了我一个暗示，可以通过使用一些空间来完成。最后，我找到了优化的解决方案，将单个字母与数字进行映射，通过按数字生成字母，就像按 2 可以生成字母 a、b 或 c 一样，因此将 a、b 和 c 与 2 进行映射。然后遍历字典中的每个单词，看看它是否是可能的解决方案。
第二个问题是[为每个元素在数组中寻找下一个更高的元素。](https://practice.geeksforgeeks.org/problems/next-larger-element/0)我告诉他 O(n^2 的蛮力之一)时间的复杂性。他让我优化一下。我用 BST 试了一下，但是没有通过所有的测试用例。然后经过一些提示，我终于找到了使用堆栈的解决方案。
他让我为井字游戏设计一个类，给定的棋盘大小是变量 n，让我通过检查任意矩阵大小 n 的全 1 或全 0 的所有行、列和对角线来实现成员函数 findWin()，
他问了我一些基于 OOP 的问题，比如抽象类、接口、它们的区别等。而在 OS 中，他问我关于互斥、信号量、它们的区别等，并详细描述了软件的生命周期。最后，回合结束了。
9 名学生进入第 4 轮，其中 5 人入选。我是其中之一。🙂
感谢 GeeksforGeeks 帮助我做准备。

如果你喜欢 GeeksforGeeks 并想投稿，你也可以用[contribute.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。

如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。

[All Practice Problems for Amazon](https://practice.geeksforgeeks.org/company/Amazon/) !

## 相关实践问题

[Maximum of minimum for every window size](https://practice.geeksforgeeks.org/problems/maximum-of-minimum-for-every-window-size/0)[Positive and negative elements](https://practice.geeksforgeeks.org/problems/positive-and-negative-elements/0)