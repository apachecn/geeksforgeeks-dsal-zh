# 无处不在的二分搜索法|第一集

> 原文:[https://www . geesforgeks . org/the-泛在-binary-search-set-1/](https://www.geeksforgeeks.org/the-ubiquitous-binary-search-set-1/)

我们都知道二分搜索法算法。二分搜索法是最容易得到正确答案的困难算法。我提出了一些我收集的关于二分搜索法的有趣问题。有人要求访问二分搜索法。

**请求大家遵守守则，“我真诚尝试解决问题，确保没有角落案例”。阅读完每个问题后，最小化浏览器并尝试解决它。**

**问题陈述:**给定 N 个不同元素的排序数组。使用最少的比较次数在数组中查找一个键。(您认为二分搜索法是在排序数组中搜索关键字的最佳选择吗？)

没有太多理论，这里是典型的二分搜索法算法。

```
// Returns location of key, or -1 if not found
int BinarySearch(int A[], int l, int r, int key)
{
    int m;

    while( l <= r )
    {
        m = l + (r-l)/2;

        if( A[m] == key ) // first comparison
            return m;

        if( A[m] < key ) // second comparison
            l = m + 1;
        else
            r = m - 1;
    }

    return -1;
}
```

理论上，在最坏的情况下，我们需要 *log N + 1* 比较。如果我们观察，除了在最后的成功匹配期间(如果有的话)，我们每次迭代都使用两个比较。在实践中，比较将是昂贵的操作，它不仅仅是原始类型的比较。最大限度地减少理论极限的比较更经济。

参见下图，了解下一个实现中的索引初始化。

![](img/ba95523e6bfec5a58c3308bcd9c2c341.png)

下面的实现使用较少的比较次数。

```
// Invariant: A[l] <= key and A[r] > key
// Boundary: |r - l| = 1
// Input: A[l .... r-1]
int BinarySearch(int A[], int l, int r, int key)
{
    int m;

    while( r - l > 1 )
    {
        m = l + (r-l)/2;

        if( A[m] <= key )
            l = m;
        else
            r = m;
    }

    if( A[l] == key )
        return l;
    if( A[r] == key )
        return r;
    else
        return -1;
}
```

在 while 循环中，我们只依赖一个比较。搜索空间收敛于放置 *l* 和 *r* 点两个不同的连续元素。我们还需要一个比较来追踪搜索状态。

可以看到样本测试用例[http://ideone.com/76bad0](http://ideone.com/76bad0)。( *C++11 代码*)

**问题陈述:**给定一个 N 个不同整数的数组，求输入‘key’的 floor 值。比方说，A = {-1，2，3，5，6，8，9，10}和 key = 7，我们应该返回 6 作为结果。

我们可以使用上面优化的实现来找到键的地板值。只要不变量不变，我们就一直将左指针向右移动。最后，左指针指向一个小于或等于键的元素(根据定义，是地板值)。以下是可能的角落案例，

—>如果数组中的所有元素都小于键，左指针会移动到最后一个元素。

—>如果数组中的所有元素都大于 key，则为错误情况。

—>如果数组中的所有元素都相等并且< = key，则这是我们实现的最坏情况输入。

这里是实现，

```
// largest value <= key
// Invariant: A[l] <= key and A[r] > key
// Boundary: |r - l| = 1
// Input: A[l .... r-1]
// Precondition: A[l] <= key <= A[r]
int Floor(int A[], int l, int r, int key)
{
    int m;

    while( r - l > 1 )
    {
        m = l + (r - l)/2;

        if( A[m] <= key )
            l = m;
        else
            r = m;
    }

    return A[l];
}

// Initial call
int Floor(int A[], int size, int key)
{
    // Add error checking if key < A[0]
    if( key < A[0] )
        return -1;

    // Observe boundaries
    return Floor(A, 0, size, key);
}
```

可以看到一些测试用例[http://ideone.com/z0Kx4a](http://ideone.com/z0Kx4a)。

**问题陈述:**给定一个可能有重复元素的排序数组。在*日志 N* 时间中查找输入‘键’的出现次数。

这里的想法是使用二分搜索法找到数组中最左边和最右边出现的键。我们可以修改 floor 函数来跟踪最右边的出现和最左边的出现。这里是实现，

```
// Input: Indices Range [l ... r)
// Invariant: A[l] <= key and A[r] > key
int GetRightPosition(int A[], int l, int r, int key)
{
    int m;

    while( r - l > 1 )
    {
        m = l + (r - l)/2;

        if( A[m] <= key )
            l = m;
        else
            r = m;
    }

    return l;
}

// Input: Indices Range (l ... r]
// Invariant: A[r] >= key and A[l] > key
int GetLeftPosition(int A[], int l, int r, int key)
{
    int m;

    while( r - l > 1 )
    {
        m = l + (r - l)/2;

        if( A[m] >= key )
            r = m;
        else
            l = m;
    }

    return r;
}

int CountOccurances(int A[], int size, int key)
{
    // Observe boundary conditions
    int left = GetLeftPosition(A, -1, size-1, key);
    int right = GetRightPosition(A, 0, size, key);

    // What if the element doesn't exists in the array?
    // The checks helps to trace that element exists
    return (A[left] == key && key == A[right])?
           (right - left + 1) : 0;
}
```

样本代码[http://ideone.com/zn6R6a](http://ideone.com/zn6R6a)。

**问题陈述:**给定不同元素的排序数组，数组在未知位置旋转。查找数组中的最小元素。

我们可以在下图中看到样本输入数组的图示。

![](img/c7413e33ca8f410a13a82b53beef46dc.png)

我们将搜索空间收敛到 *l* 和 *r* 点单元素。如果中间位置落在第一个脉冲中，条件 A[m] < A[r]不满足，我们将搜索空间收敛到 A[m+1 … r]。如果中间位置落在第二个脉冲中，条件 A[m] < A[r]满足，我们将搜索空间收敛到 A[1 … m]。在每次迭代中，我们检查搜索空间大小，如果它是 1，我们就完成了。

下面给出的是算法的实现。*能不能想出不同的实现方式？*

```
int BinarySearchIndexOfMinimumRotatedArray(int A[], int l, int r)
{
    // extreme condition, size zero or size two
    int m;

    // Precondition: A[l] > A[r]
    if( A[l] <= A[r] )
        return l;

    while( l <= r )
    {
        // Termination condition (l will eventually falls on r, and r always
        // point minimum possible value)
        if( l == r )
            return l;

        m = l + (r-l)/2; // 'm' can fall in first pulse,
                        // second pulse or exactly in the middle

        if( A[m] < A[r] )
            // min can't be in the range
            // (m < i <= r), we can exclude A[m+1 ... r]
            r = m;
        else
            // min must be in the range (m < i <= r),
            // we must search in A[m+1 ... r]
            l = m+1;
    }

    return -1;
}

int BinarySearchIndexOfMinimumRotatedArray(int A[], int size)
{
    return BinarySearchIndexOfMinimumRotatedArray(A, 0, size-1);
}
```

参见样品测试案例[http://ideone.com/KbwDrk](http://ideone.com/KbwDrk)。

**练习:**

1.名为*符号(x，y)* 的函数定义为:

```
signum(x, y) = -1 if x < y
             =  0 if x = y
             =  1 if x > y
```

您是否遇到过任何指令集，其中的比较行为类似于*符号*函数？它能使二分搜索法的第一次实施达到最佳吗？

2.实现天花板功能复制地板功能。

3.与你的朋友讨论“二分搜索法是最佳的吗(比较次数最少的结果)？为什么不对排序数组进行三元搜索或插值搜索？比起二分搜索法，你更喜欢三元搜索还是插值搜索？”

4.画一个二分搜索法的树形图(相信我，它可以帮助你理解二分搜索法的很多内部结构)。

**敬请关注，我将在接下来的文章中介绍几个更有趣的使用二分搜索法的问题。欢迎您的评论。**

–by**[文基](http://www.linkedin.com/in/ramanawithu)** 。如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。