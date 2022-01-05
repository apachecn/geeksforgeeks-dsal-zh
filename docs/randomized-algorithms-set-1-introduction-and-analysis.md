# 随机化算法|集合 1(介绍和分析)

> 原文:[https://www . geesforgeks . org/随机化-算法-集合-1-介绍-分析/](https://www.geeksforgeeks.org/randomized-algorithms-set-1-introduction-and-analysis/)

## **什么是随机化算法？**

使用随机数来决定逻辑中下一步要做什么的算法称为随机化算法。例如，在随机快速排序中，我们使用一个随机数来选择下一个枢轴(或者我们随机洗牌)。而在[卡尔格算法](https://www.geeksforgeeks.org/kargers-algorithm-for-minimum-cut-set-1-introduction-and-implementation/)中，我们随机选取一条边。

## **如何分析随机化算法？**

一些随机化算法具有确定性的时间复杂度。比如[这个](https://www.geeksforgeeks.org/kargers-algorithm-for-minimum-cut-set-1-introduction-and-implementation/)实现的卡尔格算法有时间复杂度是 O(E)。这种算法被称为[蒙特卡罗算法](https://www.geeksforgeeks.org/randomized-algorithms-set-2-classification-and-applications/)，更容易分析最坏的情况。
另一方面，其他随机化算法(除了拉斯维加斯)的时间复杂度取决于随机变量的值。这种随机算法被称为[拉斯维加斯算法](https://www.geeksforgeeks.org/randomized-algorithms-set-2-classification-and-applications/)。通常对这些算法进行预期最坏情况的分析。为了计算最坏情况下所需的预期时间，需要在最坏情况下考虑所用随机变量的所有可能值，并且需要评估每个可能值所需的时间。所有评估时间的平均值是预期的最坏情况时间复杂度。以下事实通常有助于分析此类算法。
[期望的线性](https://www.geeksforgeeks.org/linearity-of-expectation/)
[直到成功的预期试验次数。](https://www.geeksforgeeks.org/expected-number-of-trials-before-success/)

例如，考虑下面快速排序的随机版本。

一个**中心枢轴**是一个枢轴，它以这样一种方式划分阵列，即一侧至少有 1/4 个元素。

```
// Sorts an array arr[low..high]
randQuickSort(arr[], low, high)

1. If low >= high, then EXIT.

2. While pivot 'x' is not a Central Pivot.
  (i)   Choose uniformly at random a number from [low..high]. 
        Let the randomly picked number number be x.
  (ii)  Count elements in arr[low..high] that are smaller 
        than arr[x]. Let this count be sc.
  (iii) Count elements in arr[low..high] that are greater 
        than arr[x]. Let this count be gc.
  (iv)  Let n = (high-low+1). If sc >= n/4 and
        gc >= n/4, then x is a central pivot.

3\. Partition arr[low..high] around the pivot x.

4\. // Recur for smaller elements
   randQuickSort(arr, low, sc-1) 

5. // Recur for greater elements
   randQuickSort(arr, high-gc+1, high) 

```

在我们的分析中重要的是，步骤 2 所花费的时间是 O(n)。

**循环运行多少次后才能找到中心枢轴？**
随机选择的元素为中心枢纽的概率为 1/n

因此，while 循环运行的预期次数为 n(详见[本](https://www.geeksforgeeks.org/expected-number-of-trials-before-success/)

因此，步骤 2 的预期时间复杂度是 O(n)。

**最坏情况下的整体时间复杂度是多少？**
在最坏的情况下，每个分区划分数组，使得一边有 n/4 个元素，另一边有 3n/4 个元素。递归树的最坏情况高度是 Log <sub>3/4</sub> n，也就是 O(Log n)。

```
T(n) < T(n/4) + T(3n/4) + O(n)
T(n) < 2T(3n/4) + O(n)

Solution of above recurrence is O(n Log n) 

```

请注意，上述随机化算法不是实现随机化快速排序的最佳方式。这里的想法是简化分析，因为它很容易分析。
通常，随机快速排序是通过随机选取一个枢轴(无循环)来实现的。或者通过打乱数组元素。该算法的预期最坏情况时间复杂度也是 O(n Log n)，但分析是复杂的，麻省理工学院教授本人在他的讲座[中也提到了这一点](https://www.youtube.com/watch?v=852wJdsgl2I)。

[随机化算法|集合 2(分类和应用)](https://www.geeksforgeeks.org/randomized-algorithms-set-2-classification-and-applications/)

**参考文献:**
[http://www . TCS . tifr . RES . in/~ workshop/nitrkl _ igga/随机化-讲座. pdf](http://www.tcs.tifr.res.in/~workshop/nitrkl_igga/randomized-lecture.pdf)

本文由 **Ashish Sharma** 供稿。如果你发现任何不正确的地方，请写评论，或者你想分享更多关于上面讨论的话题的信息