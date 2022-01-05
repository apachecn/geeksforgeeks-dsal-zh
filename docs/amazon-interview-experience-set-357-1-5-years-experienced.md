# 亚马逊面试体验|第 357 集(针对 2.5 年经验)

> 原文:[https://www . geesforgeks . org/Amazon-面试-经验-设置-357-1-5-年-经验/](https://www.geeksforgeeks.org/amazon-interview-experience-set-357-1-5-years-experienced/)

不久前，我参加了 Amazon.com 参加 SDE 一号角色的面试，以下是我帮助其他有志之士的经验:

**Written–Pen&Paper Rounds**
必须用我选择的任何编程语言编写生产级代码，涵盖所有边缘情况，并清楚地提到我的代码的复杂性。

1.  [二叉查找树最低的共同祖先](https://practice.geeksforgeeks.org/problems/lowest-common-ancestor-in-a-bst/1)
2.  [删除最少数量的字符，使两个字符串成为字谜](https://practice.geeksforgeeks.org/problems/anagram-of-string/1)
3.  Given an array, print the Next Just Greater Element for every element. The Next just greater Element for an element x is the just greater element on the right side of x in array. Return the same element if there is no greater element present on right side, or if same element is present again on right side (in case of duplicates)

    ```
    For e.g. given input array : 3,5,8,4,2,6,3
    output should be : 3,6,8,6,3,6,6

    ```

    **解决方案** : [极客论坛链接](https://practice.geeksforgeeks.org/problems/next-larger-element/0)
    使用二叉查找树解决了它

**面对面回合？**
面试官非常乐于助人，专注于方法，他们会先问基本的暴力解决方案，然后问最优解决方案，之后他们可能会稍微增加问题的复杂性，如果你能令人满意地解释你的方法，然后会要求你用你选择的任何编程语言编写生产级代码，用纸和笔覆盖所有边缘情况:

1.  在未排序的数组中找到一个元素，这样所有左边的元素都变小，所有右边的元素都变大。
    **解决方案**:需要[geeks forgeeks Link](https://practice.geeksforgeeks.org/problems/unsorted-array/0)
    O(n)时间复杂度解决方案。
2.  在行方向列方向排序矩阵中寻找第 k 个最小元素。讨论了最小堆和最大堆方法及其复杂性。
    **解决方案** : [极客论坛链接](https://practice.geeksforgeeks.org/problems/kth-element-in-matrix/1)
3.  如果矩阵中有重复的元素，我们必须将所有重复的元素视为一个位置，即如果矩阵包含像 3，6，4，3，5，4，7 这样的元素，那么
    第一个最小元素是 3
    第二个最小元素是 4
    第三个最小元素是 5
    第四个最小元素是 6，不管发生了什么
    我问我是否可以使用哈希，但是他在寻找空间复杂度更低的东西，无法进一步回答这个特定的事情。
4.  [螺旋形式的层级顺序遍历](https://practice.geeksforgeeks.org/problems/level-order-traversal-in-spiral-form/1)
5.  找出给定二叉树中任何子节点和父节点组合之间的最大差异。这里子节点可以是父节点以下的任何级别，但应该在从父节点开始的同一子树中。使用递归、自下而上的方法求解，将最大差值和最小节点值返回到当前节点，返回到每一级的上节点。
    **解决方案** : [极客论坛链接](https://practice.geeksforgeeks.org/problems/maximum-difference-between-node-and-its-ancestor/1)
6.  关于项目的详细讨论，我设计的新东西，为什么这样，为什么不这样等等，我的团队如何工作，完整的过程，我个人的角色，责任和贡献。代码中是否有 bug，如何改正。让你的代码中的任何错误都进入生产。工作之外做什么，有没有开源贡献等。
7.  给定二叉树中的任意两个节点，找到从第一个节点到另一个节点的路径，并判断该路径是直线，还是线上有转弯，找到转弯数。
    **解决方案** : [极客论坛链接](https://practice.geeksforgeeks.org/problems/number-of-turns-in-binary-tree/1)
8.  详细讨论了 java hashmap、hashset 及其内部工作和复杂性。
9.  许多行为问题，比如，最复杂的事情，你是如何做的，你面临什么挑战，你收到的负面反馈，你是如何改进的，以及更多交叉问题。

对准备购买亚马逊产品的会员的建议:

1.  首先要对基本的数据结构概念有很好的理解，可以参考 geeksforgeeks.org 的 section wise 或者任何像 Narasimha Karamunchi 这样的书(我参考了这本书)，不要光看书，而是实现东西。
2.  阅读《破解编码面试》一书，学习如何回答行为问题。这些问题非常有限，但对于亚马逊来说是必须的。
3.  练习并解决最后 40 次亚马逊面试体验，从[practice.geeksforgeeks.org](https://practice.geeksforgeeks.org)

我希望这些信息对你们所有人都有帮助，祝你们一切都好。

如果你喜欢极客博客并想投稿，你也可以写一篇文章并把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。

[All Practice Problems for Amazon](https://practice.geeksforgeeks.org/company/Amazon/) !