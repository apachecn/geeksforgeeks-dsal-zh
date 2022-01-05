# 常见算法面试问题|第 1 集

> 原文:[https://www . geesforgeks . org/common-question-algorithm-interview-questions-set-1/](https://www.geeksforgeeks.org/commonly-asked-algorithm-interview-questions-set-1/)

***什么是算法？***
非正式地说，算法是任何定义明确的计算过程，它以某个值或一组值作为输入，并产生某个值或一组值作为输出。因此，算法是将输入转换为输出的一系列计算步骤。(来源:[CLRS 算法导论第三版](http://www.flipkart.com/introduction-algorithms-3rd/p/itmczynzhyhxv2gs?pid=9788120340077&affid=sandeepgfg))

***二分搜索法的时间复杂度是多少？***
二分搜索法的时间复杂度是 O(Logn)。详见[二分搜索法](https://www.geeksforgeeks.org/binary-search/)。

***二分搜索法可以用于链表吗？***
由于链表不允许随机访问，所以我们无法在 O(1)时间内到达中间元素。因此，二分搜索法不可能出现链表。还有其他方法，例如参考[跳过列表](https://www.geeksforgeeks.org/skip-list/)。

***如何发现两个给定的矩形是否重叠？***
如果下列条件之一成立，两个矩形不会重叠。
1)一个矩形位于另一个矩形的上边缘上方。
2)一个矩形位于另一个矩形左边缘的左侧。
详见[查找两个矩形是否重叠](https://www.geeksforgeeks.org/find-two-rectangles-overlap/)。

***如何在给定时间找到时针和分针的夹角？***
这个想法是以一个参考点为 12。找到时针和分针移动的角度，减去两个角度，找到它们之间的角度。详见[时针和分针的角度](https://www.geeksforgeeks.org/calculate-angle-hour-hand-minute-hand/)

***快速排序最坏的情况什么时候出现？***
在[快速排序](https://www.geeksforgeeks.org/quick-sort/)中，我们选择一个枢轴元素，然后通过将枢轴元素放置在排序数组中的正确位置来围绕枢轴元素对给定数组进行分区。
当分区后的一部分包含所有元素，另一部分为空时，出现快速排序的最坏情况。例如，如果对输入数组进行排序，并且选择最后一个或第一个元素作为透视，则出现最差的情况。详见[https://www.geeksforgeeks.org/quick-sort/](https://www.geeksforgeeks.org/quick-sort/)。

***一个排序后的数组在某个未知点旋转，如何高效地搜索其中的一个元素。***
一个简单的方法是使用线性搜索，但是我们可以在 O(Logn)时间内使用[二分搜索法](https://www.geeksforgeeks.org/binary-search/)进行搜索。有关更多详细信息，请参见[在排序和旋转数组](https://www.geeksforgeeks.org/search-an-element-in-a-sorted-and-pivoted-array/)中搜索元素。
这个问题的其他变体，如[在排序和旋转的数组](https://www.geeksforgeeks.org/find-minimum-element-in-a-sorted-and-rotated-array/)中找到最小元素或最大元素。

***给定一大串字符，如何高效地找到其中的第一个唯一字符？***
有效的解决方法是在计数数组中使用字符作为索引。遍历给定的字符串，存储每个字符第一次出现的索引，也存储出现的次数。然后遍历计数数组，找到计数为 1 的最小索引。详见[查找第一个唯一字符](https://www.geeksforgeeks.org/given-a-string-find-its-first-non-repeating-character/)。

***如何统计排序数组中的逆序？***
数组 arr[]中的两个元素 arr[i]和 arr[j]如果 a[i] > a[j]和 i < j，就形成一个逆序。如何计算一个未排序数组中的所有逆序。所有方法见[计数阵列中的反转](https://www.geeksforgeeks.org/counting-inversions/)。

***给定一个大阵，如何高效地找到*** **第 kth** ***最大的元素在其中？***
对此可以有很多解决方案。最好的解决方案是使用最小堆。我们建立一个前 k 个元素的最小堆 MH。对于每个元素，在第 k 个元素(arr[k]到 arr[n-1])之后，将其与 MH 的根进行比较，如果元素大于根，则将其设为根，并为 MH 调用 heapify，否则忽略它。最后，MH 有 k 个最大的元素，MH 的根是第 k 个最大的元素。详见 [k 最大(或最小)元素](https://www.geeksforgeeks.org/k-largestor-smallest-elements-in-an-array/)。

***给定一个大小为 n 的数组，其中*** **一个** ***的数字范围从 1 到 n+1。数组不包含任何重复，缺少一个数字，找到缺少的数字。***
可以有很多方法解决。其中最好的是使用异或。详见[查找缺失编号](https://www.geeksforgeeks.org/find-the-missing-number/)。这个问题有很多变体，比如[找两个重复的数字](https://www.geeksforgeeks.org/find-the-two-repeating-elements-in-a-given-array/)、[找一个缺失的和一个重复的数字](https://www.geeksforgeeks.org/find-a-repeating-and-a-missing-number/)等。

***如何写出一个高效的方法来计算 x*** **把** ***提升到 n 次方？***
思路是用[这里的分治](https://www.geeksforgeeks.org/divide-and-conquer-set-1-find-closest-pair-of-points/)在 O(Logn)时间内完成。详见[编写 C 程序计算幂(x，n)](https://www.geeksforgeeks.org/write-a-c-program-to-calculate-powxn/) 。

***给定一个输入字符串和一个单词字典，找出输入字符串是否可以被分割成一个用空格分隔的字典单词序列。***
思路是用动态规划。详见[断字问题](https://www.geeksforgeeks.org/dynamic-programming-set-32-word-break-problem/)。

***给定一排价值 v1 的 n 枚硬币。。。vn，其中 n 是偶数。我们轮流和对手比赛。在每一回合中，玩家从该行中选择第一枚或最后一枚硬币，将其从该行中永久移除，并获得硬币的价值。确定如果我们先行动，我们肯定能赢的最大可能金额。***
这也是一个动态规划问题。详见[游戏最佳策略](https://www.geeksforgeeks.org/dynamic-programming-set-31-optimal-strategy-for-a-game/)。

***给你一个任意语言的排序单词数组，你需要找到语言中的顺序(或者字符的优先顺序)。*** 例如，如果给定的数组是{“baa”、“abcd”、“abca”、“cab”、“CAD”}，那么字符的顺序是‘b’、‘d’、‘a’、‘c’。请注意，单词是经过排序的，在给定的语言中，“baa”位于“abcd”之前，因此在输出中“b”位于“a”之前。同样，我们可以找到其他订单。
这可以通过两个步骤来解决:首先通过处理给定的一组单词来创建一个图，然后对创建的图进行[拓扑排序](https://www.geeksforgeeks.org/topological-sorting/)，更多细节参见[本](https://www.geeksforgeeks.org/given-sorted-dictionary-find-precedence-characters/)。

你可能也喜欢

*   [常见数据结构面试问题|第 1 集](https://www.geeksforgeeks.org/commonly-asked-data-structure-interview-questions-set-1/)

*   练习各种算法主题的[测验](https://www.geeksforgeeks.org/quiz-corner-gq/ Mock Tests)
*   [最后一分钟笔记](https://www.geeksforgeeks.org/lmns-algorithms-gq/)–Algo

如果发现有不正确的地方，请写评论，或者想分享更多关于以上讨论话题的信息