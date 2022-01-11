# 亚马逊面试体验|第 414 集(针对 SDET-1)

> 原文:[https://www . geesforgeks . org/Amazon-interview-experience-set-414-sdet-1/](https://www.geeksforgeeks.org/amazon-interview-experience-set-414-sdet-1/)

我通过员工推荐申请了 SDET 一号职位。我在亚马逊钦奈(SP Infocity)接受了采访。我面对了 5 轮面对面的比赛。

10 月 11 日，我面对的是第一轮，主要是解决问题和编码。

**第 1 轮:问题解决和编码第 1 轮(1 小时)**

面试官只是从一个正式的问题开始，即自我介绍。然后她问我关于我最后一年的项目，我清楚地解释了，并在黑板上画了草图。

然后她问了我两个编码问题。

1.  Simulate an Android mode lock.
2.  [Generate all words](https://practice.geeksforgeeks.org/problems/possible-words-from-phone-digits/0) that can be formed in the given pattern. The keyboard specification is mobile keyboard. I will explain it clearly.

如果给定的输入是 2 3 6。

2 对应于 abc。3 对应于 def。6 对应 mno。

假设如果我们必须生成 2，3，6 的所有组合，那么输出应该是一组字符串

ADM DNA A0 bdm bdn BD 0 ...-什么

我给出了一个递归和迭代的解决方案来打印组合。

然后面试官稍微修改了一下问题。她让我用字典验证生成的字符串。

我给出了两种维护字典的方法。首先，我提出了一种哈希表方法，它采用 O(1)平均时间复杂度进行插入删除和搜索操作。

然后，由于生成的字符串有共同的前缀，我建议字典使用 trie 方法。

面试官对我的解决方案很满意，要求我完整地对解决方案进行编码。

几天后，我进行了两轮面对面的比赛。

**第 2 轮:测试和自动化轮(1 小时)**

面试官刚开始问我以前是否了解测试和测试环境，我回答没有。然后我们讨论了测试的类型和不同的阶段以及与之相关的测试程序。然后她问了我两个简单的测试用例生成问题。

1.  [Generate all possible test cases for an addition function that takes two strings as input and returns an integer, which is the sum of two numbers given as string input](https://practice.geeksforgeeks.org/problems/key-pair/0) .

我为这个问题给出了大约 10 个测试用例，因为它非常直接。我通过使用 JUnit 测试编写了一些代码，这非常简单。

2.给定编辑器中的打开文件模块，打开文件模块可能会出现哪些错误。

我给了一个案例列表，我们清楚地讨论了每个案例的来龙去脉。

这一轮很容易，因为我前一天准备了测试部分。

**第 3 轮:数据结构和算法第 1 轮(1 小时 15 分钟)**

这一轮有两个人采访了我。我们刚刚开始正式介绍。然后他们问了我两个问题。

1.  [Knight's position problem](https://practice.geeksforgeeks.org/problems/steps-by-knight/0) .

给定一个 n*n 棋盘和一个放置在任意一个角上的骑士，生成骑士可以覆盖所有方格的所有可能路径。

我从使用 BFS 的方法开始。但是在我的方法中有一个缺陷，那就是如果骑士能从给定的点出发的所有可能的点都在前面被探索过，他就不会从一个细胞中逃脱。

然后我给出了一个使用回溯的解决方案。

从一个角落开始。对于骑士可以到达的每一个可能的点，使用简单的 For 循环对其进行递归调用。一旦计数达到 n*n(例如在 8*8 的棋盘中，如果计数是 64)，打印出可以很容易地在数组中维护的遍历路径。这解决了我以前的方法中的缺陷，因为如果到达一条死胡同，我们能够回到另一种可能性。

面试官对我的方法很满意，让我为解决方案编码。我把它编码了，然后我们继续下一个问题。

2.[给定一个链表，找到两个链表的交点，这两个链表汇聚在一个公共点](https://practice.geeksforgeeks.org/problems/intersection-point-in-y-shapped-linked-lists/1)。

我首先给出了一个强力 O(n^2 方法，然后将其优化为 O(n)时间和 O(n)空间方法。然后我通过求两个列表长度的绝对差，最终给出了一个 O(n)时间 O(1)空间的解。然后他们让我编写一个非常简单的解决方案。

在此之后，我在 10 月 31 日进行了最后两轮比赛。

**第 4 轮:招聘经理轮次(1 小时)**

面试官让我简单介绍一下自己。然后我们在开始的几分钟里就确定了我的项目，然后面试官问了我之前参加的面试，以及这个过程是如何进行的。然后，他开始询问测试以及与一些给定场景对应的测试的使用。经过几分钟的讨论，他问了两个关于数据结构的问题。

1.  [Given a set of integers, print pairs that add up to the given sum.](https://practice.geeksforgeeks.org/problems/key-pair/0)

我首先给出了一个 O(nlogn)方法来找到配对并打印它们。这种方法是对数组进行排序，并保持左右两个索引(在每一端)，找出加起来是否等于给定总和的对，并打印它们，直到左右指针交叉。

然后他问我能不能进一步优化。我给出了一个使用哈希的 O(n)方法。我维护了一组整数。将第一个数字放入散列集中，从第二个元素开始，对于数组中的每个数字，检查散列集中是否存在(给定总和–当前元素)。如果是这样，打印该对。

2.[给定一棵二叉树打印它的底视图](https://practice.geeksforgeeks.org/problems/bottom-view-of-binary-tree/1)。

经过几分钟的思考，我想出了一个方法，利用节点到根的水平距离。当使用水平顺序遍历时，我们必须记录特定水平距离的最后一个节点。我使用了一个哈希表来存储每个水平距离上最后访问的节点。

这种方法使用 O(n)时间和 O(n)空间。

然后他问了一个难题。

在一个 30 人的房间里，找到唯一的握手次数，条件是房间里的每个人都应该和每个人握手。

我只是用了一个简单的逻辑。在两个人的房间里，只有一次独特的握手(第一个人有一次独特的握手，而第二个人没有)。如果我们考虑三个人，n = 3 (A，B，C)

a 有两个唯一的握手 B，c(n-1 次握手)

b 有一个唯一的握手 c(n-2 次握手)

c 没有任何独特的握手方式。

握手总数= n-1 + n-2 = 2n-3 = 3。(这是前两个自然数的总和)

同样，对于 n 个人，唯一的握手将是前 n-1 个自然数的和。

对于 n = 30，唯一握手的总数是 29*30/2 = 29*15 = 435。

结束了。他对我解决问题的方式很满意。

他问我有没有问题要问他。我询问了亚马逊的文化和工作环境。

**第 5 轮:酒吧募捐轮(1 小时)**

两个成员走进房间，做了自我介绍，我们开始了我的介绍和我的项目。

他们问我在当前一轮之前有多少轮。他们刚开始只是问了几个关于测试的问题。然后他们问了两个编码问题。

1.  [Given a binary tree, print the Kth largest element](https://practice.geeksforgeeks.org/problems/kth-largest-element-in-bst/1) .

我只是立即开始了一个蛮力解决方案，通过寻找树的有序遍历。然后对数组进行排序，找到排序后的数组中第 k 个最大的元素，也就是从数组的起始索引开始的第(n-k)个元素，其中 n 是树中的节点总数。这使用了 0 时间和 0 空间。

他们让我进一步优化。

我给出了一个 O(nlogn)时间和 O(1)空间的解，通过将二叉树转换成双链表，然后在双链表中找到第 k 个最大的，这可以在 O(nlogn)时间内完成。

但是有一个更好的解决办法，这是我在面试时想不到的。只需构造一个 k 个元素的 minheap，使用任意遍历方式遍历树，将元素插入堆中。

如果堆根元素小于树中的当前节点，则从堆中移除根元素，并将新元素插入堆中。最后，在完成树的遍历后，第 k 个最大的元素将位于堆的根。这使用了 O(nlogk)时间和 O(k)空间。

但是他们对我的方法很满意，因为他们让我通过空间或时间来优化它。我给出了一个恒定的空间方法，所以他们很满意。

2.[给定一个有向图，找出是否存在循环。如果它确实存在，打印出来。](https://practice.geeksforgeeks.org/problems/detect-cycle-in-a-directed-graph/1)

我用 BFS 给出了一个解决方案。我在队列中放了一个节点，然后添加了从当前节点可以到达的所有可能的节点。当我们遍历节点时，我们只是在 hashmap 中将节点标记为已访问，以避免节点之间无限循环。他们对我的方法很满意。

最后他们问 HashMap 是如何实现的，它是如何工作的(尤其是 hashcode 和 index 是如何计算的)。我设计了自己的散列函数，并解释了 get 和 put 函数在 hashmap 中的工作方式。他们对我的解释很满意，然后他们问在发生冲突的情况下如何修改散列函数，并简要讨论了冲突处理技术。

他们问我有没有问题要问他们。我只是问了和上一轮一样的问题。

页（page 的缩写）对于每个问题，我们都必须写清楚代码。不要直接进入编码部分，清楚地解释你的方法。要有信心，他们不想要问题的优化解决方案，他们会看到候选人如何处理问题。