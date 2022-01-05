# 带递归函数的辅助空间

> 原文:[https://www . geesforgeks . org/辅助-空间-递归-函数/](https://www.geeksforgeeks.org/auxiliary-space-recursive-functions/)

先决条件:[递归](https://www.geeksforgeeks.org/recursion/)
程序使用的内存有时与运行时间一样重要，尤其是在移动设备等受限环境中。
例如，如果我们需要创建一个大小为 n 的数组，它将需要 O(n)个空间。如果我们需要一个大小为 n×n 的二维数组，它将需要 O(n <sup>2</sup> )。
递归调用中的堆栈空间也算作程序所需的额外空间。
例如:

## 卡片打印处理机（Card Print Processor 的缩写）

```
int sum(int sum)
{
   if (n <= 0)
       return 0;
   return n + sum(n-1);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
static int sum(int sum)
{
   if (n <= 0)
       return 0;
   return n + sum(n - 1);
}

// This code is contributed by Pratham76
```

## C#

```
static int sum(int sum)
{
   if (n <= 0)
       return 0;
   return n + sum(n - 1);
}

// This code is contributed by rutvik_56
```

## java 描述语言

```
<script>

function sum(sum)
{
   if (n <= 0)
       return 0;
   return n + sum(n - 1);
}

</script>
```

在上面的示例函数中，每次调用都会给堆栈增加一个新的级别。

```
     Sum(5)
    ->sum(4)
            ->sum(3)
            ->sum(2)
                ->sum(1)
                       ->sum(0)
```

这些调用中的每一个都被添加到调用堆栈中，并占用实际内存。所以像这样的代码需要 O(n)个时间和 O(n)个辅助空间。
然而，仅仅因为你总共有 n 个调用，并不意味着它需要 O(n)个空间。考虑下面的函数，它添加了 0 到 n 之间的相邻元素:
示例:

## 卡片打印处理机（Card Print Processor 的缩写）

```
// A non-recursive code that makes n calls
// but takes O(1) extra space.
int pairSumSequence(int n)
{
    int sum = 0;
    for (int i=0; i<n; i++)
        sum += pairSum(i, i+1);
    return sum;
}

int pairSum(int a, int b)
{
    return a + b ;
}
```

在这个例子中，大约有 O(n)个对 pairSum 的调用。然而，那些调用并不同时存在于调用栈中，所以我们只需要 O(1)空间。
本文由**巨然·活女神**供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。