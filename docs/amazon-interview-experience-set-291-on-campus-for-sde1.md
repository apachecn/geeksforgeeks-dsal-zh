# 亚马逊面试体验|第 291 集(SDE1 的校内)

> 原文:[https://www . geesforgeks . org/Amazon-interview-experience-set-291-校园-for-sde1/](https://www.geeksforgeeks.org/amazon-interview-experience-set-291-on-campus-for-sde1/)

亚马逊参观了我们的 SDE 1 号校园。整个面试过程分为一轮编码和一套 4 人面对面面试。

**在线编码回合:**
这是一场 90 分钟的测试，22 道题(20 道 MCQs + 2 道编码)集合在 HackerRank 上。

编码题:
1。[将一串单词倒过来。](https://practice.geeksforgeeks.org/problems/reverse-words-in-a-given-string/0)
例:让输入字符串为“我很喜欢这个程序”。该函数应该将字符串更改为“非常像我这样的程序”

2.[给定和的子阵最大长度。](https://practice.geeksforgeeks.org/problems/subarray-with-given-sum/0)

MCQs 由操作系统、几何、基础数学、C、递归等主题组成。

至少解决了两个问题的人被选中参加面试。

 **【F2F 1(技术):**
他问我在海得拉巴微软印度开发中心的暑期实习项目，问我参与其中的几项技术，以及我为什么使用某些东西。
然后他转向两个技术问题。

1.[给定一个排序和旋转的数组，找到一个给你的元素。](https://practice.geeksforgeeks.org/problems/finding-number/0)
我给了他一个 O(logn)解决方案，找到支点，然后在两个半场都做二分搜索法。但是是 O(logn) + O(logn)，所以他让我修改成一个一 O(logn)的问题。给他解决方案后，他让我考虑所有的角落测试用例，编写生产级代码。

2.给定一个由一个班级的学生分数组成的英国标准分。发现所有连排名的学生都作弊了，所以我们从他们的分数中减少 k 分。修改 BST 以进行标记的更改，而不考虑在此操作后，BST 可能不再是 BST。

我给了他一个修改过的有序遍历，这样就可以对元素进行排序，并使用一个计数器变量进行求解。他让我修改它，既不使用静态计数器变量，也不使用传递给递归调用的指针。对于这两个问题，他还问了我时间和空间的复杂性。

**F2F 2(技术):**
他又问了一个关于我暑期实习的非常简短的想法。然后他又问了我两个问题。

1.[给定一个数组中 k 大小的窗口，在每个窗口中找到 max 元素。](https://practice.geeksforgeeks.org/problems/maximum-of-all-subarrays-of-size-k/0)
[https://www . geeksforgeeks . org/最大尺寸子阵列 k/](https://www.geeksforgeeks.org/maximum-of-all-subarrays-of-size-k/)

我和他讨论了很多关于可以使用哪种数据结构的问题，最后提出了一个队列解决方案。考虑到所有的角落情况，我被要求重新编码。

2.[使用堆栈通过操作](https://practice.geeksforgeeks.org/problems/queue-using-two-stacks/1)实现队列(入队、出队、空、大小)。
当我告诉他解决方案时，他甚至问我，当我做一个正常的队列时，我是更喜欢数组还是链表实现。

(两者的空间和时间复杂性)

 **【F2F 3(技术):**
他还让我简单介绍一下我的暑期实习项目。

他从数组和链表的优缺点开始。然后是一个关于数组的问题:

1.[给定一个数组，除了一个出现奇数次的元素外，所有的偶数元素都出现偶数次。找到那个元素](https://practice.geeksforgeeks.org/problems/find-the-odd-occurence/0)。

我从 XOR 解决方案开始，但是他告诉我 OS 不支持 XOR。于是，我给了他一个 HashMap <int>的解决方案。他继续要求我进一步优化。所以最后我得到了 O(k)的空间复杂度，其中 k=唯一元素的数量。
问我最优化解决方案的空间和时间复杂性。</int>

2。

```
 a)Increasing(1,2,3,4)
 b)Decreasing(4,3,2,1)
 c)Increasing-decreasing(1,2,3,4,7,6,5)
 d)Decreasing-increasing(7,6,5,1,2,3,4) 
```

给出四种阵型

在 O(1)中找到数组的类型，然后找到数组中的最大元素。

除了情况 c，最大元素是 O(1)。对于 c，我给出了二分搜索法解。他让我考虑到角落的情况来写代码。

**F2F 4(酒吧筹集者):**
他问我最喜欢的科目是什么。我跟 DS 说了，他就从 DS 问我。

1.使用带有入队和出队成员函数的数组实现编写一类循环队列。

2.[给定一个二元矩阵(仅填充 0 和 1)，其中 0 表示水，1 表示陆地。我们可以向上或向下或向左或向右穿越。给定一个来源和目的地，看看我们是否能到达目的地。](https://practice.geeksforgeeks.org/problems/find-whether-path-exist/0)
然后他修改了它，以找到所遵循的路径，然后找到可能的最小路径。
(代码不是必需的)

3.给定一系列构建项目的操作以及每个操作花费的时间。有些操作依赖于以前的操作。找到完成操作所需的最短天数。

我不太确定我在想的解决方案，所以他说没关系，并结束了采访。

**提示:**
1。继续和面试官分享你的想法，他会帮你很多。
2。不要放弃，多思考一点，你可能会想出一个绝妙的主意。

一定要记住:
“如果结局不好，那么很可能还没有结束”

我要感谢所有朋友的支持，并特别感谢极客网站。干杯！🙂

如果你喜欢极客博客并想投稿，你也可以写一篇文章并把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。

[All Practice Problems for Amazon](https://practice.geeksforgeeks.org/company/Amazon/) !

## 相关实践问题

[Subarray with given sum](https://practice.geeksforgeeks.org/problems/subarray-with-given-sum/0)